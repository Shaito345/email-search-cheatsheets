# Exact Phrase Search in Gmail With Quotes and Filters

Quotes tell Gmail to look for an exact word or phrase. Google lists this on its Gmail search help page. The notes below come from that page.

*Last reviewed 19 November 2026.*

## How Quotes Work

Put the words in double quotes and Gmail looks for that exact phrase.

```
"dinner and movie tonight"
```

## Add Filters to a Quoted Phrase

Filters narrow the search to a sender, a date or a place. Combine a quoted phrase with the operators in the [Gmail operators cheat sheet](gmail-operators.md).

These three queries are ours. We built them from Google's operators and have not copied them from Google. Test them in your own mailbox before you rely on them.

```
"dinner and movie tonight" from:amy@example.com
"dinner and movie tonight" newer_than:2d
"dinner and movie tonight" in:anywhere
```

The last query adds `in:anywhere`, which Google says searches across Gmail including Spam and Trash.

## When Results Look Wrong

Google's help page describes four behaviors worth knowing when a search looks wrong.

1. **Excluded words still show up.** Conversations with excluded criteria can still appear, because Gmail finds matching messages first and then shows the full conversation.
2. **Numbers split.** A space or a dash separates a number, so 01.2047-100 counts as two numbers.
3. **One word needs an exact match.** Google says the `+` operator finds emails that match a single word exactly.
4. **Word order changes with `AROUND`.** Quotes keep the first word first, as in `"secret AROUND 25 birthday"`.

We list only what the help page says.

## Source

- [Google: Search operators you can use with Gmail](https://support.google.com/mail/answer/7190)

## Related Guides

- [Gmail Search Exact Phrase Not Working](https://www.mailxaminer.com/blog/gmail-search-exact-phrase-not-working/?utm_source=github&utm_medium=repo&utm_campaign=email-search-cheatsheets&utm_content=gmail-exact-phrase) is our article on the MailXaminer site. It explains why standard Gmail search misses messages and attachments and lists fixes.
