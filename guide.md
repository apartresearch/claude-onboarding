# Set up Claude on your work accounts

About 20 minutes; add 10 if you need Notion through a token (step 4). You need a Mac or Windows computer, your work Google account, and a seat on your organisation's Claude Team plan: accept the invitation email first, and ask your Claude Team Owner if you don't have one.

Steps marked *(unverified)* haven't yet been walked end to end.

## 1. Install and sign in

1. Download the Claude desktop app from https://claude.com/download and install it. If you already have it, update it: on Windows, older versions ask for Git before they start.
2. Sign in with your work Google account. If you also have a personal Claude account, check the account menu shows your organisation, not your personal plan.

## 2. Open the Code tab in a folder

1. Open the **Code** tab at the top.
2. Choose a folder to work in, for example a new folder called `Claude` in your Documents. Files Claude writes for you land there. *(unverified: exact wording of the folder picker)*

From here, you can let Claude walk you through the rest: send it this repository's address and "Read SETUP-FOR-CLAUDE.md in this repository and set me up."

## 3. Connect your tools

Select **+** next to the message box, then **Connectors** (or Settings → Connectors), and connect each with your own login. Claude only ever sees what your own account can see.

| Connector | What Claude can do with it |
|-----------|----------------------------|
| Gmail | Search and read your email; write drafts into your Drafts folder; send, reply and forward |
| Google Calendar | Read your calendar; create and change events and send invitations |
| Google Drive | Search and read your files; create, copy, move, share and delete files |
| Google Docs, Sheets, Slides | Read and edit; Docs edits can be made as suggestions you accept or reject |
| Slack | Search and read the channels you're in; draft, send and schedule messages |
| Notion | Read and query pages and databases; create and update pages; comment. Full workspace members connect it here; guests use step 4 |
| Granola | Your own meeting notes, if you record meetings in Granola |

If a connector shows **Request** instead of **Connect**, it hasn't been switched on for your organisation yet: tell your Claude Team Owner.

To check: ask Claude "which connectors do you have in this session?"

## 4. Notion if you're a guest in the workspace

Notion's connector refuses guest accounts ("You are a guest, so you cannot connect to Notion MCP"). Guests use a Notion integration token instead, which a workspace admin creates for you.

1. Get your token from your workspace admin, and ask them to connect it to the pages you work on (guests can't add connections themselves).
2. Install Node.js (the LTS version) from https://nodejs.org.
3. In the Claude app, open Settings → Developer → **Edit Config** and add the block below, with your token in place of `paste-your-token-here`. If the file already has an `"mcpServers"` section, add the `"notion"` entry inside it. *(unverified: menu path)* The file is `~/Library/Application Support/Claude/claude_desktop_config.json` on a Mac and `%APPDATA%\Claude\claude_desktop_config.json` on Windows.

   ```json
   {
     "mcpServers": {
       "notion": {
         "command": "npx",
         "args": ["-y", "@notionhq/notion-mcp-server"],
         "env": { "NOTION_TOKEN": "paste-your-token-here" }
       }
     }
   }
   ```

4. Quit and reopen the app. In the Code tab, ask: "Can you see the Notion page [a page you work on]?" If it can't, the connection on that page is missing: ask your workspace admin.

Keep the token in that file only, never in a chat, a message or a document. This route works in the Code tab, not in the app's Cowork mode.

## 5. How Claude asks before acting

The selector under the message box sets how much Claude asks first. **Manual** asks before every action, which is a good place to start: with Gmail, Slack, Calendar and Drive connected, Claude can send email and messages, invite people and share files, and in Manual mode it asks you each time. Switch modes whenever you like.

## 6. When to use what

- **Code tab:** anything that should produce something: a draft, a Google Doc or Sheet, a Notion update, a recurring briefing.
- **"Ask [your organisation]"** (in the claude.ai sidebar and the app's chat, if your Owner has set it up): quick questions answered from your connected tools, with sources, such as "what did we decide about X?" or "catch me up on #channel". It searches Notion through Notion's connector, so not for guests.
- **From your phone or another computer:** type `/remote-control` in a Code session (or turn on Settings → Claude Code → "Connect new sessions to Remote Control") and continue it from claude.ai/code or the Claude mobile app. Your computer has to stay on, and your Owner has to have turned Remote Control on.

## 7. A recurring briefing

Ask Claude in a Code session, for example "every weekday at 8, tell me what needs me today", or create it under **Routines** → **New routine** → **Local**. It runs while the app is open and the computer is awake; if the computer was asleep, it runs once when it wakes. After creating it, click **Run now** once and choose "always allow" for each tool it uses, or later runs stop to ask.

## 8. Try it

Start with the first prompt in [prompts.md](prompts.md): it has Claude map where your work lives from your own tools. Claude reads a file called `CLAUDE.md` in your folder at the start of every session, so if you like the summary, ask Claude to save it there.
