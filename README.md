# StellaFrame MCP server

Let your AI agent build and install your website widgets.

[StellaFrame](https://stellaframe.com) makes embeddable widgets for any
website: Google reviews, an Instagram feed, a YouTube gallery, an audio
player, an FAQ, a WhatsApp chat button, a countdown timer and a class
schedule. This is the documentation for its remote
[MCP](https://modelcontextprotocol.io) server. Connect Claude, Claude Code,
Cursor or another AI agent, sign in with your StellaFrame account, and ask
for the widget you want in plain words.

This repository holds documentation only. The server's source code is not in
this repository.

## The address

    https://app.stellaframe.com/mcp

- Remote server, streamable HTTP transport
- Sign-in with OAuth 2.1. There is no API key
- The same address for every agent

## Connect

### Claude (web, desktop or mobile)

1. Open StellaFrame in Claude's connector directory,
   https://claude.ai/directory/connectors/stellaframe, and add it.
2. Choose Connect and sign in with your StellaFrame account.

Or add it yourself: in Claude, open Plugins, choose Add, then Add custom
connector, and paste the address.

### Claude Code

1. Run this command in your terminal:

   ```sh
   claude mcp add --transport http stellaframe https://app.stellaframe.com/mcp
   ```

2. In Claude Code, run `/mcp` to sign in.

### Cursor

1. Add a remote MCP server in Cursor's settings with the address above, or
   add this to `~/.cursor/mcp.json`:

   ```json
   {
     "mcpServers": {
       "stellaframe": { "url": "https://app.stellaframe.com/mcp" }
     }
   }
   ```

2. Sign in with your StellaFrame account when Cursor asks.

### Other agents

Add a remote MCP server (streamable HTTP) with the address above and sign in
when asked.

No account yet? [Create one for free](https://app.stellaframe.com/agents).
You approve every connection: before an agent gets in, a StellaFrame consent
screen asks whether to allow it.

## What your agent can do

- See your plan and how many widgets it allows
- List your widgets, read their settings and see whether a page has shown
  them this month
- Look up what each kind of widget needs and which settings it takes
- Find your business on Google for a reviews widget
- Check the Instagram account or Google business with you first, and give you
  a link to preview a widget before it is installed
- Create, change and delete widgets, the same as you can in the dashboard
- Get the embed code and the install steps for your site
- Give you a link to upgrade, which you open yourself
- Pass a request or a problem on to StellaFrame

An agent that can edit your site's code, such as Claude Code or Cursor with
the project open, adds the embed code itself. For a site builder, the agent
gives you the embed code and the steps to follow.

## What your agent cannot do

- See your password
- See your payment details
- Change your plan
- Charge a card
- Delete your account

## Tools

| Tool | What it does | Kind |
| --- | --- | --- |
| `get_account` | Reads your plan and widget allowance, and passes on news that something you asked for has shipped | Read |
| `list_widgets` | Lists your widgets and whether a page has shown each one this month | Read |
| `get_widget` | Reads one widget, its settings, a fresh preview link and its insights (views and clicks) | Read |
| `get_widget_options` | Says what one kind of widget needs and which settings it takes | Read |
| `search_businesses` | Finds a business on Google for a reviews widget, with its photo and Google Maps link when available | Read |
| `find_instagram_account` | Looks up a public Instagram account before a feed is built on it: name, picture, post count, profile link and three recent posts | Read |
| `create_widget` | Creates a widget, within your plan's limits, and returns a preview link | Write |
| `update_widget` | Changes a widget's settings and returns a preview link | Write |
| `delete_widget` | Deletes a widget | Write, destructive |
| `get_install_instructions` | Returns the embed code, steps for a coding agent and steps for each site builder | Read |
| `get_upgrade_link` | Returns a link you open yourself to upgrade. The agent charges nothing | Read |
| `get_narration_help` | Help with making and hosting an audio file for the audio player | Read |
| `send_feedback` | Passes a request or a problem to StellaFrame | Write |

Every tool declares its MCP annotations (a title, and whether it is
read-only or destructive), so an agent can ask before it changes anything.

## Example prompts

- "Add a Google reviews carousel for my bakery to the homepage."
- "Make an FAQ widget from the questions on my pricing page and install it there."
- "Put a WhatsApp chat button on every page of this site."
- "Change my Instagram feed to three columns and match the site's brand color."
- "Which of my widgets are live on a page this month?"
- "Tell StellaFrame I want a widget it does not have yet."

## Preview before you install

`create_widget`, `update_widget` and `get_widget` each return a preview link.
It opens a small page with the real widget under a line saying it is a
preview and not on your site yet. The link needs no sign-in and works for 24
hours. Ask your agent for a new one after that. Opening a preview does not
count as a widget view.

## Plans

- Connecting an agent needs no upgrade. It works on the Free plan.
- Free: 1 widget of any type, 300 widget views a month, and a "Powered by
  StellaFrame" line under the widget.
- Pro: $5/mo for up to 3 widgets, 100,000 views a month each and no
  "Powered by" line. Each extra $5/mo adds 3 more widgets.
- An agent works within your plan exactly as the dashboard does. If you ask
  for more than your plan allows, the agent says so and can give you an
  upgrade link. Only you can upgrade.

## Privacy and security

- **OAuth 2.1, no API key.** Your agent opens a StellaFrame sign-in page. The
  server follows the MCP authorization spec: dynamic client registration, the
  authorization code flow with PKCE (S256), and rotating refresh tokens.
- **A consent screen for every connection.** It names the app that is asking,
  and it warns you when StellaFrame does not recognize that app.
- **Tokens are hashed at rest.** A copy of the database is not a set of keys.
- **Disconnect any time.** The AI agents page in your dashboard lists every
  agent connected to your account, each with a Disconnect button.
- **Connections expire.** A connection lapses after 90 days without use. An
  account keeps at most 20 connections. Resetting your password disconnects
  all of them.
- **Rate limits.** 120 calls a minute per account, and one message per
  request.
- **No AI model on our side.** Your own agent does the thinking, on your own
  subscription to it. StellaFrame receives the requests the agent makes, not
  your conversation with it.

Full details: [privacy policy](https://stellaframe.com/privacy) and
[terms of service](https://stellaframe.com/terms).

## Limits worth knowing

- An account gets 10 Instagram lookups an hour that reach Instagram. Lookups
  of an account one of your widgets already shows are not counted.
- A preview link works for 24 hours.
- One upgrade link per 30 minutes. It is reused if you ask again.

## Support

Email [support@stellaframe.com](mailto:support@stellaframe.com), or ask your
agent to send feedback. It reaches the same inbox, and we can reply to you by
email.

## Links

- Site: https://stellaframe.com
- About the MCP server: https://stellaframe.com/ai-agents
- Privacy policy: https://stellaframe.com/privacy
- Terms of service: https://stellaframe.com/terms

## About this repository

This repository is documentation for the StellaFrame MCP server. The server
runs at the address above and its source code is not in this repository. To
report a problem or ask for a feature, email support@stellaframe.com.
