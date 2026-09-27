# Davia Creation

Build and revise the characters, places, and rules of your private Davia game
drafts from an assistant. [Davia](https://davia.ai) is a character-first sandbox
RPG: creators build worlds that players inhabit as one character.

This plugin connects to Davia's hosted MCP server and includes one skill for
using it. The detailed creation skill and its references are served by the
MCP itself, so the plugin does not duplicate those instructions or bundle the
server implementation.

## Requirements

- A Davia account and a private editable game draft with a board.
- A client that supports remote MCP over Streamable HTTP and OAuth.
- MCP resource reading to load the server's current creation guidance before
  editing. A host that exposes only tools can inspect files but cannot follow
  the full editing workflow described by this plugin.

## Connect

The plugin is prepared for submission to the Cursor Marketplace, which is
used by Grok Bot. It is not yet an approved marketplace listing.

For a local Cursor preview, clone this repository directly into Cursor's
local plugin directory:

```sh
git clone https://github.com/davialabs/davia-creation-plugin.git \
  ~/.cursor/plugins/local/davia-creation
```

Reload Cursor, open Customize, and check that the `davia-creation` skill and
MCP server appear. Local plugin imports must be allowed by your team policy.
This local preview procedure applies to Cursor IDE; it does not install the
plugin into Grok Bot.

For an internal team preview, use Cursor Dashboard → Plugins & MCPs → Team
Marketplaces → Add Marketplace → Import from Repo. Import this repository and
enable the plugin for the intended members. Team marketplaces require a Teams
or Enterprise plan. See [Cursor's plugin documentation](https://cursor.com/docs/plugins).

Choose Connect or Authorize for Davia Creation and sign in to Davia in the
browser. No API key, environment variable, or local server is required.

The MCP endpoint is:

```text
https://tale-mcp-208104258932.us-east4.run.app/mcp
```

Clients that support adding a remote MCP directly can use this URL without
installing the plugin. That adds the server; it does not install the bundled
client-side skill.

## Try it

- “Show my editable Davia games.”
- “Open my game named Harbor at Dawn and show its simulation rules.”
- “In the selected game, rename the character Mira to Mirabel.”
- “Find a suitable Map Asset for this landmark.”

The MCP works on existing private drafts. It can inspect and update world
files, add or remove entities and landmarks, append stat definitions, and
assign current Map Assets. It cannot create a whole game, publish a game,
delete a whole game, or create or remove map cells. Use the Creation Hub for
those actions.

## Data and access

Requests go to Davia's hosted service. OAuth identifies the creator, and the
server restricts game access to that creator's eligible private drafts.
Reading exposes the requested game content to the connected assistant;
editing writes to the saved draft. Removing an entity or landmark deletes
that object from the draft. This repository contains no credentials or game
data.

- [Privacy policy](https://davia.ai/legal/privacy-policy)
- [Terms of use](https://davia.ai/legal/terms-of-use)
- Support: [contact@davia.ai](mailto:contact@davia.ai)

## Package and maintenance

```text
.cursor-plugin/plugin.json       Plugin metadata
mcp.json                         Hosted MCP connection
skills/davia-creation/SKILL.md    One MCP usage skill
assets/logo.png                  Davia logo
LICENSE                          MIT license for this package
```

The public skill is an entry point to
`skill://davia-creation/SKILL.md` and its server-provided references. Maintain
detailed game contracts on the MCP. Update this package when its connection,
metadata, or usage workflow changes. Davia's hosted service and private server
code are not licensed by this repository. The MIT license does not grant
rights to use Davia trademarks to imply endorsement.

## Publisher checklist

Before submitting a release, validate the manifest and skill, then test in the
target client: plugin discovery, OAuth sign-in, reading the skill resource and
its references, listing and selecting a draft, reading a file, and one small
edit on a disposable draft followed by a reread. Restore the test edit.
Check reconnect behavior and confirm that unrelated games remain untouched.

Submit this repository URL at
[Cursor Marketplace → Publish](https://cursor.com/marketplace/publish).
Marketplace review and target-client OAuth validation are separate from
publishing this Git repository. See the
[submission requirements](https://cursor.com/docs/reference/plugins#submitting-a-plugin).
