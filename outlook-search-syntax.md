# Outlook Search Syntax Cheat Sheet for Keywords and Fields

Outlook search keywords narrow a mailbox to one sender, one subject or one date. Type a keyword, a colon and a value in the search box. Microsoft documents the keywords in separate articles for Outlook for Windows and Outlook on the web. This sheet joins them and marks where they differ.

*Last reviewed 20 November 2026.*

## Fields You Can Search

| Keyword | What it searches | Sample query | Documented in |
|---|---|---|---|
| `from:` | Sender | `from:"bobby moore"` | Both articles |
| `to:` | Recipient | `to:bobby` | Both articles |
| `cc:` | Cc line | `cc:bobbymoore@contoso.com` | Both articles |
| `bcc:` | Bcc line | `bcc:bobby` | Both articles |
| `subject:` | Subject line | `subject:"bobby moore"` | Both articles |
| `received:` | Date received | `received:1/15/2026` | Both articles |
| `category:` | Category name | `category:red` | Both articles |
| `hasattachment:yes` | Messages with attachments | `hasattachment:yes` | Both articles |
| `participants:` | To, Cc and Bcc together | `Participants:JerriFrye` | Web article |
| `body:` or `content:` | Message body | `Body:report` | Web article |
| `sent:` | Date sent | `Sent:01/01/2017` | Web article |
| `isflagged:` | Flagged or unflagged messages | `report IsFlagged:no` | Web article |
| `messagesize:` | Message size | `messagesize:>5 MB` | Windows article |
| `read:no` | Messages you have not opened | `read:no` | Windows article |
| `hasflag:true` | Messages flagged for follow up | `hasflag:true` | Windows article |

Search is not case sensitive, so `From:` and `from:` work the same. Leave no space after the colon. Microsoft says `to: JerriFrye` searches for JerriFrye as a plain word, not as a recipient.

## Join Words and Exclude Terms

| Syntax | What it does | Sample query |
|---|---|---|
| `AND` | Finds items with both terms | `bobby AND moore` |
| `OR` | Finds items with one term or both | `bobby OR moore` |
| `NOT` | Leaves out items with a term | `bobby NOT moore` |
| `" "` | Finds an exact phrase | `subject:"product plan"` |
| `( )` | Groups words for one keyword | `Subject:(product plan)` |
| `-` | Excludes a field value | `-from:"Jerri Frye"` |
| `*` | Matches the end of a word | `cat*` |

Write `AND`, `OR` and `NOT` in capital letters. Microsoft says they must be in uppercase.

The Windows article documents `NOT`. The web article documents `( )`, `-` and `*`.

The web article says a space between two terms works like `AND`. It also says `Subject:product plan` looks for "product" in the subject and "plan" anywhere, while `Subject:(product plan)` looks for both words in the subject.

## Search by Date

Both articles show a plain date and relative words.

```
received:1/15/2026
received:"this week"
```

Put multi word dates in quotes. The web article says dates use the MM/DD/YYYY form and that two dots (`..`) set a range.

## Where Outlook for Windows and Outlook on the Web Differ

| Topic | Outlook for Windows article | Outlook on the web article |
|---|---|---|
| Attachment keyword | `hasattachment:yes` | `HasAttachment:yes` |
| Day and month names in dates | Says they are no longer supported | Says they are supported |
| Size keywords | `messagesize:` with sizes like `>5 MB` | Not listed |
| Extra keywords | `due:`, `followupflag:`, `read:` | `participants:`, `body:`, `sent:` |
| Wildcards | None documented. Words match from their start, so `ray` finds Raymond | Only at the end of a word, as in `cat*` |

Microsoft's classic Outlook filter article shows the attachment keyword as `hasattachments:yes`. The other two articles drop the final "s". Try both spellings if one returns nothing.

## Search Limits

The Windows article and the web article both say Outlook returns only the first 1,000 results. Narrow the query when the message you need is missing.

The Windows article adds three more facts. Punctuation is ignored, numbers shorter than five digits are ignored and the `messagesize:` words tiny, small, medium, large, verylarge and enormous do not work in new Outlook for Windows.

## Combined Queries to Try

These three queries are ours. They join Microsoft's keywords with spaces and the capital letter operators. We have not copied them from Microsoft. Test them in your own mailbox before you rely on them.

```
from:"bobby moore" hasattachment:yes
subject:"product plan" received:"this week"
from:bobby AND subject:report NOT category:red
```

## Sources

- [Microsoft: How to search in Outlook](https://support.microsoft.com/en-us/outlook/getstarted/how-to-search-in-outlook)
- [Microsoft: Search Mail and People in Outlook on the web](https://support.microsoft.com/en-us/outlook/search-mail-and-people-in-outlook-on-the-web)
- [Microsoft: Use Outlook's built-in search filters](https://support.microsoft.com/en-gb/office/use-outlook-s-built-in-search-filters-86fe4399-fba1-42e1-8057-6a5d7f99a230)

## Related Guides

- [Gmail Search Operators Cheat Sheet](gmail-operators.md)
- [Exact Phrase Search in Gmail With Quotes and Filters](gmail-exact-phrase.md)
