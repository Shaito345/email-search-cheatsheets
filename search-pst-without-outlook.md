# Search PST Files Without Outlook, Four Methods

Four methods search a PST file when Outlook is not on your computer. Webmail import needs an admin, a free viewer needs Windows, a conversion needs a command line and a forensic platform needs setup time. This guide lists the limits of every method and says which ones we tested.

*Last reviewed 27 November 2026.*

## Short Answer

Convert the PST with `readpst` and search the output files. That is the one method we tested from start to finish.

The other three methods are listed with the limits the vendors state. We could not test them on our Linux test machine.

## Method 1, Import the PST Into a Webmail Account

Microsoft and Google both let an admin import a PST file into a cloud mailbox. You then search with the search box in the webmail.

Microsoft Purview has an Import service for Exchange Online mailboxes. Microsoft says you need the Mailbox Import Export role and the Mail Recipients role, or a global administrator account. Microsoft also says no role group holds the Mailbox Import Export role by default.

Microsoft lists these limits.

- A PST file must be 20 GB or smaller. Larger files can slow the import.
- Items over 150 MB are skipped.
- Public folders are not supported.
- Import speed is about 24 GB a day for one mailbox, and Microsoft does not guarantee it.

Network upload uses the AzCopy.exe tool, and Microsoft lists it as free. Microsoft sends end users to a separate article for importing a PST into their own mailbox. We did not review that article.

Google Workspace Migration for Microsoft Exchange (GWMME) imports PST files for a Workspace admin. Google says you need a super administrator account, a top level folder with one folder per user and PST files with password protection off.

Google also says the Outlook version on the GWMME client machine must be the same as or newer than the version that created the PST file. We take that as a sign Outlook must be on that machine, but the page does not say so outright. Google lists the Outlook desktop app and not the web version for its user tool, GWMMO.

We did not test either import. Both need a Microsoft 365 or Google Workspace account with admin rights.

## Method 2, Open the PST in a Free Viewer

XstReader is an open source viewer for Outlook mail files. Its README says it needs only .NET Framework 4 and has no dependency on Microsoft Office components, so Outlook does not have to be installed.

XstReader opens PST and OST files, shows a three pane mail view and exports messages as text, HTML or RTF. The README says the main app works on Windows. A separate command line tool, XstPortableExport, is built on .NET Core 2.1 and works on Windows, Mac and Linux.

The limit for keyword work is search. The README describes a search through message headers and through Cc and Bcc names, and it does not describe a full body search. Check this on your own file before you rely on XstReader for keywords.

We did not test XstReader because our test machine uses Linux and the main app is a Windows program.

## Method 3, Convert the PST and Search the Files

Two free command line packages convert a PST file. `readpst` comes from libpst and `pffexport` comes from libpff. Both open the PST without Outlook.

We tested both on Ubuntu with `readpst` 0.6.76 and `pffexport` 20180714. The test file was `testPST.pst`, a 2.3 MB public sample from the Apache Tika project.

### Convert to MBOX With readpst

The readpst manual says `-r` creates folders named as in the PST file and puts the emails in a file called `mbox` inside the folder. The manual also says the output directory must already exist.

```
mkdir out
readpst -r -o out sample.pst
```

In our test `readpst` printed `8 items done, 0 items skipped` and wrote one `mbox` file with 7 messages. We did not find out what the eighth item was.

Search the file with `grep`. The `-i` option ignores capital letters.

```
grep -n -i "keyword" out/*/mbox
```

We searched for `featuregenerator` and `grep` matched 3 lines. The lines do not tell you which message they belong to.

### Convert to EML With readpst

The manual says `-e` saves every email as a separate file with the `.eml` extension.

```
readpst -e -o out sample.pst
```

In our test the command wrote 7 numbered `.eml` files. This command lists the files that hold a word.

```
grep -rli "keyword" out
```

The word `featuregenerator` was found in 2 of the 7 files.

### Search the Decoded Text With Python

A plain `grep` sees the raw text of a message. One of our 7 files holds an attachment stored as base64 text, so `grep` sees encoded characters and not the words inside the attachment.

The script below decodes the body of every message in an MBOX file and prints the date and subject of the messages that hold your word. The script searches the subject and the body. The script does not search attachments.

```
import mailbox
import sys
from email import message_from_binary_file, policy


def parse(f):
    return message_from_binary_file(f, policy=policy.default)


box = mailbox.mbox(sys.argv[1], factory=parse)
word = sys.argv[2].lower()

for i, msg in enumerate(box, start=1):
    body = msg.get_body(preferencelist=("plain", "html"))
    text = body.get_content() if body else ""
    if word in text.lower() or word in str(msg["subject"]).lower():
        print(i, msg["date"], msg["subject"])
```

Save it as `search_mbox.py` and start it with the MBOX path and your word.

```
python3 search_mbox.py out/FOLDER/mbox keyword
```

In our test the word `featuregenerator` gave two messages, numbers 1 and 3, and the word `couchbase` gave message 6. A word that is not in the file printed nothing.

### Export Items With pffexport

The pffexport manual says the tool exports items stored in a PST, OST or PAB file. The `-t` option sets the base name of the target folder, and pffexport adds `.export` to it.

```
pffexport -t out/sample sample.pst
grep -rli "keyword" out
```

In our test pffexport made one folder for every message, named `Message00001` and so on. The folders hold `Message.txt`, `InternetHeaders.txt`, `Recipients.txt`, `OutlookHeaders.txt` and `ConversationIndex.txt`. The `grep` command found `featuregenerator` in two `Message.txt` files.

The sample PST used French folder names, and pffexport kept them. Expect folder names in the language of the PST.

### Limits of the Conversion Method

- You need a command line and basic comfort with it.
- Search covers the text you point at. Attachments need their own text step.
- The libpff project page lists its status as alpha.
- The readpst manual lists `-D` to include deleted items. We did not test it.

## Method 4, Use a Forensic Search Tool

A forensic platform opens the PST, indexes the messages and searches them for you. This is the right fit when you need reports, many PST files or proof of how you searched.

Autopsy is a free forensic platform from The Sleuth Kit. Its documentation says the Email Parser module finds MBOX, EML and PST files by file signature, extracts the emails and adds the results to the Blackboard. We did not install or test Autopsy.

Paid forensic and eDiscovery tools also exist. Ask these questions before you choose one.

- Does the tool open PST and OST files, and does it handle your largest file?
- Does keyword search cover message bodies, headers and attachments?
- Can you export the hits and a report?
- Does the tool work on your operating system and on a copy of the evidence?
- Does the license fit the size of your project?

## Which Method Fits

| Method | Needs an admin | Search you get | Tested here |
|---|---|---|---|
| Webmail import | Yes | Webmail search box | No |
| Free viewer | No | Header search, per the README | No |
| Convert and search | No | Text search with grep or a script | Yes |
| Forensic tool | No | Tool search across messages | No |

## Check the Result Before You Rely on It

1. Work on a copy of the PST file. Keep the original untouched.
2. Check the file type with `pffinfo sample.pst`. In our test it printed the file size, the content type Personal Storage Tables (PST) and the file type 64-bit.
3. Record a hash before you start and compare it after. Our `sha256sum` value for the sample file was the same after conversion.
4. Compare the message count. Our `readpst` output counted 8 items and wrote 7 messages, so we kept a note of the gap.
5. Search for a word that you know is in one message, and confirm that the tool finds it.

## Our Notes

These points are ours and are not quotes from the sources.

- A keyword hit shows that a word appears in a message. It does not show who wrote the message or why.
- Search on a converted copy and not on the only copy of the evidence.
- Attachments hold words that a plain `grep` cannot see.
- Test every method on a PST file that you know before you use it on a real case.

## Legal and Privacy Note

This note is general information and not legal advice. Check the rules in your country before you collect or search email, and search only mail that you own or are authorized to search.

A PST file can hold private messages from many people. Keep the files in a secured folder and share hits only with people who need them.

## Sources

- [Microsoft Learn: Learn about importing PST files](https://learn.microsoft.com/en-us/purview/pst-import-overview)
- [Microsoft Learn: FAQ about importing PST files](https://learn.microsoft.com/en-us/purview/pst-import-faq)
- [Google Workspace Admin Help: Migrate data from PST files](https://knowledge.workspace.google.com/admin/migrate/migrate-data-from-pst-files)
- [Google Workspace Help: About GWMMO](https://support.google.com/a/users/answer/12288424)
- [XstReader on GitHub](https://github.com/Dijji/XstReader)
- [Ubuntu manual page: readpst](https://manpages.ubuntu.com/manpages/lunar/man1/readpst.1.html)
- [Ubuntu manual page: pffexport](https://manpages.ubuntu.com/manpages/noble/man1/pffexport.1.html)
- [libpff on GitHub](https://github.com/libyal/libpff)
- [Autopsy User Documentation: Email Parser Module](https://sleuthkit.org/autopsy/docs/user-docs/4.23.0/email_parser_page.html)
- [Apache Tika test file testPST.pst](https://github.com/apache/tika/blob/main/tika-parsers/tika-parsers-standard/tika-parsers-standard-modules/tika-parser-microsoft-module/src/test/resources/test-documents/testPST.pst)

## Related Guides

- [Outlook Search Syntax Cheat Sheet for Keywords and Fields](outlook-search-syntax.md)
- [How to Search Keywords in a PDF With Acrobat, Browsers and Command Line](pdf-keyword-search.md)
- [Email Search Cheat Sheets](README.md)
