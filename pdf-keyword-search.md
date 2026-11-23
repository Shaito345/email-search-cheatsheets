# How to Search Keywords in a PDF With Acrobat, Browsers and Command Line

Three tools search a PDF well: Adobe Acrobat, a browser or viewer and a command line tool. Scanned PDFs need text recognition first. This guide lists the steps and shows which ones we tested.

*Last reviewed 23 November 2026.*

## Check That the PDF Has Searchable Text

Adobe says a scanned paper document saved as PDF holds only image data and no searchable text. Adobe also says the quickest check is to try to select or highlight text. If you cannot, you are likely dealing with a scanned PDF.

Scanned files need the OCR steps near the end of this guide.

## Search One PDF in Adobe Acrobat

Adobe documents these steps for the Find toolbar.

1. Press Ctrl+F on Windows or Command+F on macOS.
2. Type your word. Acrobat suggests matching words with the number of matches. Selecting a word highlights every match.
3. Select the ellipsis next to the search box to set options.

| Option | What it does |
|---|---|
| Whole words | Finds exact matches only |
| Case sensitive | Matches capital letters |
| Include bookmarks | Adds bookmark text to the search |
| Include comments | Adds comment text to the search |

## Search a Folder of PDFs With Advanced Search

Adobe says to use the desktop app and not a web browser.

1. Open the Find toolbar and select the ellipsis, then select **Advanced Search**.
2. Enter your text.
3. Select **All PDF Documents in**, then **Browse for Location** and choose the folder.
4. Select **OK**, then **Search**.

Results can be sorted by Relevance Ranking, Date Modified, Filename or Location. The save icon offers **Save results to PDF** and **Save results to CSV**.

Adobe also says encrypted PDFs cannot be searched in a multi document search. Open those one at a time.

## Search a PDF in a Browser or Viewer

Chrome Help says Ctrl+F on Windows, Linux and ChromeOS, or Command+F on a Mac, finds a word or phrase on a page. Chrome Help covers web pages. We did not confirm in Chrome Help that the same shortcut works inside the PDF viewer, and we did not test it. Try it on a sample file first.

The GNOME Evince help says to press Ctrl+F or the slash key, then type. It also says some PDF documents are not searchable because their text is stored as an image.

## Search With the Command Line

The `pdftotext` tool comes from the Poppler package. Its manual page says it converts PDF files to plain text, and that a text file name of `-` sends the text to standard output. That lets you pipe the text to `grep`.

We ran these commands on a three page fake PDF with pdftotext 24.02.0.

```
pdftotext sample.pdf - | grep -n -i "budget"
```

The command listed the matching line with its line number. The `-i` option ignores capital letters.

To find the page number, use `pdftotext` on one page at a time. The manual page says `-f` sets the first page and `-l` sets the last page.

```
for p in 1 2 3; do pdftotext -f $p -l $p sample.pdf - | grep -qi "budget" && echo "page $p"; done
```

In our test the loop printed `page 2`, the only page with the word.

The manual page adds a limit. Some PDF files hold fonts whose encodings are mangled, and the manual says there is no way to extract text from them short of OCR.

## Scanned PDFs Need OCR First

Adobe says Acrobat can add a searchable text layer. In Acrobat, select **All tools**, then **Scan & OCR**, then **Recognize text**. Choose the page range and the language, then select **Recognize Text**.

For a free command line option, we ran Tesseract 5.3.4 on a page image.

```
pdftoppm -r 150 -png -f 2 -l 2 sample.pdf page
tesseract page-2.png ocr pdf
pdftotext ocr.pdf - | grep -n -i "budget"
```

The first command saved page 2 as `page-2.png`. The second command made `ocr.pdf` with a text layer. The third command found the word. Before OCR, the image only PDF gave `pdftotext` no text at all in our test.

OCR on a real scan can miss or misread words. We tested on clean fake text only. Check the results on your own files.

## Sources

- [Adobe: Search in PDFs](https://helpx.adobe.com/acrobat/using/searching-pdfs.html)
- [Adobe: Recognize text in scanned documents](https://helpx.adobe.com/acrobat/desktop/create-documents/scan-documents-to-pdfs/recognize-text.html)
- [Adobe: OCR a PDF](https://www.adobe.com/in/acrobat/online/ocr-pdf)
- [Google Chrome Help: Search within a page](https://support.google.com/chrome/answer/95440)
- [GNOME Evince help: Find text in a document](https://help.gnome.org/evince/finding.html)
- [Debian manual page: pdftotext](https://manpages.debian.org/trixie/poppler-utils/pdftotext.1.en.html)
- [Tesseract OCR on GitHub](https://github.com/tesseract-ocr/tesseract)

## Related Reading

[How To Search For Keywords in PDF With Guide to Find Multiple Terms](https://www.mailxaminer.com/blog/search-keywords-in-pdf/?utm_source=github&utm_medium=repo&utm_campaign=email-search-cheatsheets&utm_content=pdf-keyword-search) is our article on the MailXaminer site. It covers viewer search, Acrobat Advanced Search and OCR, and adds a way to search many terms across many PDFs.

## Related Guides

- [Outlook Search Syntax Cheat Sheet for Keywords and Fields](outlook-search-syntax.md)
- [Gmail Search Operators Cheat Sheet](gmail-operators.md)
