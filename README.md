# Labour Projection Tracker

A single-page site for logging labour projections across:
- **Food for Education** (Miagayuini Primary, Ihururu Primary, Kiriti Secondary, Mathakwaini Primary)
- **Highlands**, **Kigumo**, **Mai Mahiu**, **Migaa**, **MUA**

All data entry (name, ID, phone, worker type, rate, days, tasks, BQ quantities) is manual.
Extra-hour rate, Amount, OT Amount and totals calculate automatically. The Excel export is
styled to match the F4E payroll sample: site name and date top-left, blue column headers,
shaded subtotal rows, and an orange grand-total row.

## 1. Put this on GitHub Pages

1. Create a new repository on GitHub (e.g. `labour-tracker`).
2. Upload `index.html` (and this `README.md`) to the repository — either drag-and-drop
   on the GitHub web UI ("Add file → Upload files") or via git.
3. Go to **Settings → Pages**.
4. Under "Build and deployment", set **Source: Deploy from a branch**, **Branch: main**,
   folder **/ (root)**, then **Save**.
5. Wait about a minute, then GitHub shows your live URL
   (something like `https://yourusername.github.io/labour-tracker/`). Open it — that's
   the site, live and shareable, no server needed.

Any time you want to change something, edit `index.html` in the repo and GitHub Pages
redeploys automatically within a minute or two.

## 2. Make "Email Report" send automatically (optional but recommended)

A static site like this can't send email on its own — there's no server behind it.
To get a genuine one-click "auto-send to jmwero@pala.co.ke", wire up **EmailJS**
(free tier, no backend required):

1. Sign up at [emailjs.com](https://www.emailjs.com/) (free plan is fine).
2. **Email Services** → add your Gmail/Outlook account → note the **Service ID**.
3. **Email Templates** → create a template using these variables in the body:
   `{{subject}}`, `{{message}}`, `{{to_email}}` → note the **Template ID**.
4. **Account → General** → copy your **Public Key**.
5. Open `index.html`, find this block near the top of the `<script>` section:
   ```js
   const EMAILJS_PUBLIC_KEY  = '';
   const EMAILJS_SERVICE_ID  = '';
   const EMAILJS_TEMPLATE_ID = '';
   ```
   Paste your three values in between the quotes, save, and push to GitHub.

Once configured, **Email Report** sends the site-by-site wage summary straight to
jmwero@pala.co.ke with no extra steps. Until then, it downloads the Excel file and
opens a pre-filled email draft for you to attach the file to and send manually.

**Note on attachments:** EmailJS's free tier sends text, not file attachments, so the
auto-sent email carries the wage summary (per site, plus grand total) rather than the
Excel file itself. The full formatted workbook still downloads to your device on every
click — attach it to the auto-sent email afterwards if you want the file itself to reach
that inbox too.

## 3. WhatsApp

**Send via WhatsApp** downloads the Excel file and opens a WhatsApp chat to
**+254 745 553 496** with the wage summary pre-filled. Browsers can't attach a local
file to a WhatsApp message or tap "send" for you — WhatsApp only allows that through
their paid Business API with a backend behind it — so you'll attach the downloaded file
and tap send yourself. It's one extra step, but everything else is prepared for you.

## 4. Notes

- Data lives only in the page's memory while it's open. Refreshing or closing the tab
  clears whatever hasn't been exported yet — export before you close, or ask about
  adding persistent storage if you're using this daily.
- Worker "Amount" = Rate × Days. "OT Amount" = (Rate ÷ 8) × OT Hours. "Total" = Amount + OT Amount.
