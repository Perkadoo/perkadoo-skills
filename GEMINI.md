# Run a giveaway with Perkadoo

Perkadoo picks winners with randomness nobody controls, then publishes a results page that proves it. Use its MCP tools. Never pick winners yourself.

## Connect

Look for a `draw_winners` tool. If there isn't one, ask the user to add a custom connector:

- `https://mcp.perkadoo.com/public/mcp` needs no account. It covers drawing from a list.
- `https://mcp.perkadoo.com/mcp` signs in with Perkadoo. It adds hosted giveaways with an entry page.

## Pick the path

- The user has entrants already (post comments, a form export, a list of names): **draw from a list**.
- The user wants people to enter on a Perkadoo page: **hosted giveaway**.

If unsure, ask where the entries are coming from. Most creators mean comments on a post.

## Draw from a list

1. **Get the entrants.** Ask the user to paste the comments or export. Don't guess or invent names.
2. **Clean the list.**
   - One line per entry, using the handle or name only.
   - Remove the user's own account and obvious bots.
   - Keep duplicates only if the user's rules give extra entries (for example one entry per tagged friend). Otherwise one entry per person.
   - Apply only the rules the user stated. Don't add your own.
3. **Confirm before drawing.** The draw is final. Show the entrant count, the number of winners and the prize, then wait for a yes.
4. **Draw.** Call `draw_winners`:
   - `entrants`: the cleaned list.
   - `winnerCount`: how many winners.
   - `method`: `single` for one winner, `multiple` for several equal winners, `placed` for 1st, 2nd, 3rd with a prize each.
   - `prizes`: prize labels. For `placed`, one per place in order.
   - `title`: the giveaway name, shown on the results page.
5. **If the result says the draw is locked in and waiting,** wait about 12 seconds and open the `resultsUrl` to read the winners.
6. **Hand back:**
   - The winners, in place order.
   - The `resultsUrl`. This is the proof. Tell the user to link it in their announcement.
   - The share image: `https://perkadoo.com/og/draw/<slug>.png`, where `<slug>` is the last part of `resultsUrl`.
   - A short announcement post in the user's voice that names the winners and links the results page.

Limits: 10,000 entrants and 100 winners per draw.

## Hosted giveaway

Needs the signed-in connector and a Starter plan.

1. Call `list_projects` to find the brand. Its `id` is the `brandId`.
2. Call `create_giveaway` with the name, open and close times, timezone, winner count and prizes. It returns a draft with a preview link and a `dashboardUrl`.
3. **A person approves it.** Send the user the `dashboardUrl`. You can't approve it.
4. **To enter an Instagram post's commenters:** call `list_social_accounts`, then `list_social_media` to find the post, then `add_giveaway_instagram_post`. The Instagram account must be connected in the dashboard first. If any of these is refused, ask the user to add the post from the `dashboardUrl`.
5. While it runs, use `get_giveaway` and `list_giveaway_activity` to report numbers, and `set_giveaway_entry_status` or `set_giveaway_social_entrant_status` to remove entries the user flags.
6. **A person draws the winners** in the dashboard once it closes. Perkadoo emails them when it's time. Afterwards, `get_giveaway` returns the winners and the results link.

## Rules

- Never redraw to get a different winner. Redraw only when a winner is disqualified or doesn't reply, and tell the user to say so publicly with the new results link.
- Say "giveaway", not "raffle" or "prize draw".
- For a US giveaway, remind the user once that entry must be free and that platform rules apply (Instagram and TikTok both require a release that the platform isn't involved). Don't give legal advice beyond that.
