# Owner checklist

What the Owner of the organisation's Claude Team plan sets up before a newcomer follows [guide.md](guide.md), and a test run to do once on your own account.

## Set up

1. **Seat.** Organization settings → Members: invite the person's work address. A standard seat includes Claude Code and the connectors; a premium seat only adds usage.
2. **Connectors for the organisation.** Organization settings → Connectors: add Gmail, Google Calendar, Google Drive, Google Docs, Google Sheets, Google Slides, Slack, Notion and Granola, so members see **Connect** rather than **Request**. The Google ones are built by Google and can write as well as read (drafts and sending, events, sharing, edits).
3. **Slack.** The Slack connector needs the Slack workspace admin to approve the integration.
4. **Google.** If Google Workspace restricts third-party apps (Admin console → Security → API controls), the Claude connectors need to be allowed.
5. **Notion for guests.** Notion's connector refuses guest accounts. For each guest, a Notion workspace admin creates an internal integration, gives the guest its token, and connects it to the pages they work on; guide step 4 covers the rest. For members, Claude sees exactly what their Notion access allows.
6. **Remote Control** (optional). Claude Code admin settings: turn on Remote Control so members can continue a desktop session from claude.ai/code or the mobile app.
7. **"Ask [organisation]"** (optional). In the claude.ai sidebar, finish its setup ("Set up for your org") with a documents connector (Google Drive) and a chat connector (Slack), plus Gmail; members then connect their own accounts to it.

## Test run on your own account

Do this once before newcomers start; note anything that doesn't match the guide.

1. Install or update the desktop app, sign in with your work account, and check the account menu shows the organisation.
2. Open the Code tab in a new folder. Note the folder picker's exact wording.
3. Connect Gmail, Calendar, Drive, Docs, Sheets, Slack and Notion, then ask "which connectors do you have in this session?" All should be listed.
4. In Manual mode, run the first prompt in [prompts.md](prompts.md). Check that Claude asks before each tool call and that the summary is right.
5. Ask "draft a reply to [a recent email] in my Gmail drafts". Check it appears in Drafts and wasn't sent.
6. Notion through a token: install Node.js, add the block from guide step 4 with an integration token, quit and reopen, and ask Claude to open a page connected to that integration. Note whether the Settings → Developer → Edit Config path matches.
7. Create a recurring briefing as a local scheduled task, click **Run now**, choose "always allow" for each tool, and check that a second run doesn't stop to ask.
8. Optional: `/remote-control` in a session, then open it from the Claude mobile app.
9. Optional: send this repository's address to a fresh Code session with "Read SETUP-FOR-CLAUDE.md in this repository and set me up", and check Claude follows it.
