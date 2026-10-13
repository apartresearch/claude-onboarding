# Instructions for Claude: set this person up

You are running in the Code tab of the Claude desktop app, and the person you're helping has asked you to set them up from this repository. They are probably not a developer. Work through the steps below in order, one at a time: do the parts marked **you**, and for the parts marked **them**, tell them exactly what to click, then wait for them to say it's done before moving on. Keep each message short and in plain language. [guide.md](guide.md) has the same steps written for a person; read it for details.

## Rules

- Never ask for a token or password in the chat. If the person pastes one anyway, use it, and tell them it is now in this conversation's history.
- Never send, reply, forward, share, invite or delete anything during setup. Drafts are fine.
- Before editing any existing file, make a copy of it next to the original.
- If a step fails, say what you saw and what you'd try next; don't guess silently.

## Steps

1. **Check the account (them).** Ask them to confirm the account menu shows their organisation, not a personal plan.

2. **Check the connectors (you, then them).** List the claude.ai connectors available in this session. For each of Gmail, Google Calendar, Google Drive, Google Docs, Google Sheets, Google Slides, Slack and Notion that is missing, tell them: select **+** next to the message box → **Connectors** → **Connect** next to it, and sign in with their work account. If one shows **Request** instead of **Connect**, tell them to ask their Claude Team Owner. Granola only if they record meetings in Granola.

3. **Notion (you, then them).** Ask whether Notion connected in step 2. If it refused them as a guest, set up the token route:
   1. Check whether Node.js is installed (`node --version`). If not, tell them to install the LTS version from https://nodejs.org and tell you when it's done.
   2. Open the desktop config file (`~/Library/Application Support/Claude/claude_desktop_config.json` on a Mac, `%APPDATA%\Claude\claude_desktop_config.json` on Windows), copy it as a backup if it exists, and add this entry under `"mcpServers"` (create the file and the section if missing), keeping everything else as it is:

      ```json
      "notion": {
        "command": "npx",
        "args": ["-y", "@notionhq/notion-mcp-server"],
        "env": { "NOTION_TOKEN": "paste-your-token-here" }
      }
      ```

   3. Tell them to open that file (or Settings → Developer → Edit Config), replace `paste-your-token-here` with the token their workspace admin gave them, save, then quit and reopen the app and start a new session in the same folder with "continue the setup from step 3.4".
   4. In the new session, check that Notion tools are available and ask them for the name of a page they work on; try to open it. If it isn't found, the token isn't connected to that page: tell them to ask their workspace admin to add the connection.

4. **How you ask before acting (them).** Explain the mode selector under the message box in two sentences, and suggest **Manual** while they learn: you'll ask before each action, including sending messages or sharing files.

5. **Where their work lives (you).** Look through their Slack channels, Drive, calendar and Notion, and summarise their main projects, the channels and folders those live in, and the people they work with. Show it to them; if they want, save it as `CLAUDE.md` in this folder so future sessions start with it.

6. **A recurring briefing (you, then them).** Offer to set up a weekday morning briefing (unanswered emails and Slack messages, today's meetings, tasks due this week). If they want it, create it as a local scheduled task at the time they choose, then ask them to click **Run now** on it once and choose "always allow" for each tool, so later runs don't stop to ask. Tell them it only runs while the app is open and the computer is awake.

7. **Wrap up (you).** Point them to [prompts.md](prompts.md) for things to try next, and to guide step 6 for when to use the Code tab, the "Ask [organisation]" project and Remote Control.
