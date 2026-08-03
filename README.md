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

1. Sign up at [emailjs.com](https://www.emailjs.com/).
2. **Email Services** → add your Gmail/Outlook account → note the **Service ID**.
3. **Email Templates** → create a template that uses these variables in the body:
   `{{subject}}`, `{{message}}`, `{{to_email}}` → note the **Template ID**.
4. Still in the template editor, open the **Attachments** tab → add an attachment of
   type **Variable Attachment** → set its parameter name to `attachment` (this is what
   the code sends the Excel file under). Attachments are an EmailJS paid-plan feature —
   check their current [pricing](https://www.emailjs.com/pricing/) before relying on it;
   without a plan that supports attachments, EmailJS will still send the email but the
   file may not come through.
5. **Account → General** → copy your **Public Key**.
6. Open `index.html`, find this block near the top of the `<script>` section:
   ```js
   const EMAILJS_PUBLIC_KEY  = '';
   const EMAILJS_SERVICE_ID  = '';
   const EMAILJS_TEMPLATE_ID = '';
   ```
   Paste your three values in between the quotes, save, and push to GitHub.

Once configured, **Email Report** sends the Excel workbook itself, as an attachment,
straight to jmwero@pala.co.ke — no extra steps. Until then, it downloads the file and
opens a pre-filled email draft for you to attach it to and send manually.

## 3. WhatsApp

**Send via WhatsApp** downloads the Excel file and opens a WhatsApp chat to
**+254 745 553 496** with the wage summary pre-filled. This one has a hard platform
limit rather than a plan/config issue: WhatsApp's click-to-chat links
(`wa.me/...?text=...`) only support pre-filling text — there's no parameter for a file
or a link to one, on any plan, without going through WhatsApp's Business API and a
backend to host the file at a real URL. So this button downloads the file and opens the
chat pre-filled; you attach the downloaded file yourself and tap send. If you want this
fully automatic later, it's possible with a small backend (e.g. upload the file to
private cloud storage and message a link via the WhatsApp Business API) — say the word
if you'd like that built.

## 4. Notes

- Data lives only in the page's memory while it's open. Refreshing or closing the tab
  clears whatever hasn't been exported yet — export before you close, or ask about
  adding persistent storage if you're using this daily.
- Worker "Amount" = Rate × Days. "OT Amount" = (Rate ÷ 8) × OT Hours. "Total" = Amount + OT Amount.
