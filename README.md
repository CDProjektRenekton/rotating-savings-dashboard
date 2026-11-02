# HR RSA Savings Dashboard

A single-page dashboard for the HR rotating savings association (paluwagan). Each round, every member contributes and one member takes home the pot. The page reads a published Google Sheet, so there's no server or build step: open `index.html` or host it on GitHub Pages.

## What it shows

| Tab | What it's for |
| --- | --- |
| **Overview** | Total collected vs due, pot per round, cycle progress, overdue amount, payouts released. Shows the current round: who receives the pot, when, how much has been collected, and who hasn't paid. You can step back and forward through rounds. Also lists upcoming payouts, members needing attention, and monthly and cumulative charts. |
| **Contributions** | Members × months grid. Each cell is marked paid, partial, missed, due now or upcoming, and each member's payout month is outlined. Includes monthly totals and collection rate. You can search it, export it to CSV, and print it. |
| **Payout schedule** | The rotation as a timeline: recipient, payout date, amount, collection progress and release status for every round. |
| **Members** | A ledger with paid to date, balance, amount left to pay, net position, payout and status. You can filter (behind, due, up to date, got payout, waiting), sort, export to CSV, and open any member's month-by-month history. |
| **Google Sheet** | The source sheet, embedded. |

Members who have **already received the pot but are behind on contributions** are flagged. In a rotating savings group they are the main risk.

## Google Sheet format

The sheet must be **published to the web** (File → Share → Publish to web) so the CSV link works.

Required:

- A name column (`Name`, `Member`, … or simply the first column)
- Month columns: `January`…`December`, `Jan`…`Dec`, or `Enero`…`Disyembre`

Optional columns, recognised automatically:

| Column | Example values | Effect |
| --- | --- | --- |
| `Payout Month` | `March`, `3/30/2026`, `Mar 15` | Sets the rotation (and payout day, if a date is given) |
| `Order` / `No.` | `1`, `2`, `3` | Rotation order, one payout per month |
| `Contribution` | `2000` | That member's monthly share, if it differs from the usual amount |
| `Received` | `Yes` / `No` | Confirms payouts that have been released |
| `Total Savings` | `24000` | Fallback total when month cells are empty |

Title rows above the header, a totals row, and "Prepared by:" notes rows are ignored. A member who holds two slots should appear on two rows.

Without a `Payout Month` or `Order` column, the rotation follows the sheet's row order, one payout per month. Payouts dated in the past count as released unless `Received` says `No`.

## Settings

**Settings** (gear icon) lets an admin override the monthly contribution, cycle start month, payout day (15 for kinsenas, 30 for katapusan) and cycle year. It also lets them reorder the rotation or **Draw lots** to shuffle it. These settings are stored in that browser only; use the sheet columns above to share the rotation with everyone.

## Configuration

Edit the `CONFIG` block near the top of the `<script>` in `index.html` to change the sheet link, login, cycle year, default payout day or refresh interval.

> The login only keeps casual visitors out. The credentials are visible in the page source, and the published sheet is public, so don't store sensitive personal data in it.
