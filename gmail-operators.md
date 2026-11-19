# Gmail Search Operators Cheat Sheet

Gmail search operators narrow a mailbox to the messages you need. Type them in the search box at the top of Gmail. Google lists them on its help page. The sample queries in the tables come from that page.

*Last reviewed 19 November 2026.*

## Core Operators

| Operator | What it finds | Sample query |
|---|---|---|
| `from:` | Emails sent from a specific person | `from:amy@example.com` |
| `to:` | Emails sent to a specific person | `to:john@example.com` |
| `subject:` | Emails with a word or phrase in the subject line | `subject:anniversary party` |
| `has:attachment` | Emails that include an attachment | `has:attachment` |
| `filename:` | Emails with an attachment of a certain name or file type | `filename:pdf` or `filename:homework.txt` |
| `older_than:` | Emails older than a time period | `older_than:1y` |
| `newer_than:` | Emails newer than a time period | `newer_than:2d` |
| `size:` | Emails by their size | `size:1000000` |
| `larger:` | Emails above a size | `larger:10M` |

Use `d` for days, `m` for months and `y` for years with the two date operators.

## Join and Exclude Terms

| Operator | What it does | Sample query |
|---|---|---|
| `OR` | Finds emails that match one or more criteria | `from:amy OR from:david` |
| `{ }` | Same job as `OR` in a shorter form | `{from:amy from:david}` |
| `AND` | Finds emails that match all criteria | `from:amy AND to:david` |
| `-` | Excludes emails from the results | `dinner -movie` |
| `( )` | Groups several terms together | `subject:(dinner movie)` |
| `" "` | Finds an exact word or phrase | `"dinner and movie tonight"` |

## Find Words Close Together

`AROUND` finds emails where two words sit close together. The number sets how many words apart they can be.

```
holiday AROUND 10 vacation
```

Put the search in quotes to keep the first word first.

```
"secret AROUND 25 birthday"
```

## Search by Label, Place and Status

| Operator | What it finds | Sample query |
|---|---|---|
| `label:` | Emails under one of your labels | `label:friends` |
| `in:anywhere` | Emails across Gmail, including Spam and Trash | `in:anywhere movie` |
| `in:archive` | Archived messages | `in:archive payment reminder` |
| `in:snoozed` | Emails you snoozed | `in:snoozed birthday reminder` |
| `is:important` | Emails marked important | `is:important` |
| `is:starred` | Starred emails | `is:starred` |
| `is:unread` | Unread emails | `is:unread` |
| `is:read` | Emails already opened | `is:read` |
| `is:muted` | Emails you muted | `is:muted subject:team celebration` |

## Two Notes From Google

Negative operators can leave surprises. Google says conversations with excluded criteria can still appear, because Gmail finds matching messages first and then shows the conversation they belong to.

Numbers split at spaces and dashes. Google says a space or a dash separates a number and a dot makes a decimal, so 01.2047-100 counts as two numbers.

## Combined Queries to Try

These three queries are ours. They join the operators above with spaces. We have not copied them from Google. Test them in your own mailbox before you rely on them.

```
from:amy@example.com has:attachment filename:pdf
from:john@example.com newer_than:2d -subject:invoice
{from:amy from:david} older_than:1y has:attachment
```

## Related Guides

- [Google: Search operators you can use with Gmail](https://support.google.com/mail/answer/7190)
- [Email Header Cheat Sheet](https://github.com/Shaito345/email-header-cheatsheet)
