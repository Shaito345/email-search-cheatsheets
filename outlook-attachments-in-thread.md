# How to Find Attachments in an Outlook Email Thread

Outlook attaches a file to one message, not to the thread. You have three ways to find it. You can search with a keyword, use a built in filter or change how the thread shows. This guide lists the steps Microsoft documents for every way and marks the Outlook version they apply to.

*Last reviewed 21 November 2026.*

## Why a Thread Hides Attachments

Outlook groups messages that share a subject line into a conversation. Microsoft describes a conversation as all messages in the same thread with the same subject line. The message list shows one line for the thread, so you open it to see the messages inside.

The paperclip appears on the message that carries the file. A reply that does not repeat the file has no paperclip, even when an earlier message does. This is our note and not a Microsoft quote.

## Search With a Keyword

Microsoft says Outlook scans email messages and many types of attachments for the words you type. Type a word from the file name or the message, then add an attachment keyword.

| Outlook version | What to type | Source article |
|---|---|---|
| Classic Outlook | `hasattachments:yes` in the search box at the top of the message list | Find all messages with attachments in Outlook |
| Outlook on the web | `HasAttachment:yes` | Find email, contacts and events in Outlook on the web |
| New Outlook | Type a keyword, then select **Files** | Find all messages with attachments in Outlook |

Microsoft's example for the web version is `blue hasattachment:yes`. It returns only messages that contain the word "blue" and have attachments. A search for `HasAttachment:no` returns messages without attachments.

If you do not remember the sender or the file name, select **Files** on its own in new Outlook. Microsoft says this lists every email that has attachments.

## Use a Built In Filter in New Outlook

New Outlook has four options in Microsoft's article.

1. Select the filter button on the right side of the search box, then check the **Attachments** box.
2. Enter a search term, then select **Has attachments** in the **Refine** group.
3. Select **Sort**, then choose **Has files**. This shows only messages with attachments in the current view.
4. Select **Back** next to your search term, or select a folder like **Inbox**, to clear the results.

## Change How the Thread Shows

Conversation view puts many messages under one line. Switching it off lists every message on its own line, so you can see which one carries the paperclip. Microsoft documents the switch like this.

| Outlook version | Steps |
|---|---|
| Classic Outlook | On the **View** tab, select **Show as Conversations**. Choose **This folder** or **All mailboxes**. Clear the same option to stop using Conversation view. |
| New Outlook and Outlook on the web | On the **View** tab, select **Conversations** in the Messages group. Select **Group into conversations**, or select **Show each message separately** to stop. |

Microsoft's conversation article also says that when you add most account types to Outlook, messages show in Conversations by default.

## Quick Checks When the File Is Missing

These checks are ours. They follow from the steps above and are not copied from Microsoft.

- Open every message in the thread. The file can sit on an earlier message.
- Search the file name without the extension. Outlook scans attachment content, so a word inside the file can also work.
- Try both `hasattachments:yes` and `hasattachment:yes`. Microsoft's classic article uses the first spelling and its web article uses the second.

## When Search Is Not Enough

Outlook search has limits. Large archives and cases that need a record of every attachment can call for other tools. [Find Attachments in an Outlook Email Chain](https://www.mailxaminer.com/blog/find-attachments-in-outlook-email-chain/?utm_source=github&utm_medium=repo&utm_campaign=email-search-cheatsheets&utm_content=outlook-attachments-in-thread) is our article on the MailXaminer site. It covers the same steps and adds notes for investigations.

## Sources

- [Microsoft: Find all messages with attachments in Outlook](https://support.microsoft.com/en-us/outlook/find-all-messages-with-attachments-in-outlook)
- [Microsoft: Find email, contacts and events in Outlook on the web](https://support.microsoft.com/en-us/office/find-email-contacts-and-events-in-outlook-on-the-web-189276e4-3cc6-411f-b49b-b43ffd31fb9f)
- [Microsoft: How to search in Outlook](https://support.microsoft.com/outlook/getstarted/how-to-search-in-outlook)
- [Microsoft: View email messages by conversation](https://support.microsoft.com/office/0eeec76c-f59b-4834-98e6-05cfdfa9fb07)

## Related Guides

- [Outlook Search Syntax Cheat Sheet for Keywords and Fields](outlook-search-syntax.md)
- [Gmail Search Operators Cheat Sheet](gmail-operators.md)
