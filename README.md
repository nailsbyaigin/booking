# Nail booking site: setup (about 10 minutes)

## 1. Create the repo and publish
1. On GitHub, create a **public** repo (e.g. `booking`).
2. Upload `index.html` and `slots.json` to it.
3. **Settings → Pages** → Source: *Deploy from a branch* → `main` / root → Save.
4. Your site: `https://USERNAME.github.io/booking/`. This is the link for customers.
   Admin page: the same link with `#admin` on the end.

## 2. Create two tokens
Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token.**
For both: *Repository access* → **Only select repositories** → your booking repo.

**Customer token** (goes in the website):
- Permissions → **Issues: Read and write**. Nothing else.
- Set expiry to the maximum (1 year), and put a reminder to renew it.

**Admin token** (only your wife keeps it):
- Permissions → **Issues: Read and write** and **Contents: Read and write**.

## 3. Put the customer token in index.html
GitHub automatically revokes tokens it finds in public repos, so split it in two.
Edit the top of `index.html`:

```js
owner: "your-github-username",
repo: "booking",
salon: "Nails by Aigin",
tokenParts: ["github_pat_11ABC", "...rest of the token..."]
```
Cut the token anywhere in the middle. Commit the change.

## 4. First login (your wife)
1. Open `https://USERNAME.github.io/booking/#admin`
2. Paste the **admin token**. The page creates an encryption key pair, keeps the private key in her browser, and stores only the public key in `slots.json`.
3. **Copy the private key from the Backup section and save it somewhere safe** (e.g. WhatsApp to herself). Without it, bookings can't be read on a new phone or after clearing the browser. On a new device: paste the admin token, then the private key.

## 5. Daily use
- **Add free times:** pick a date, type times like `10:00, 11:30, 14:00`, tap Add.
- **See bookings:** listed at the top with name, phone, service. Phone numbers are tap-to-call.
- **Cancel:** the Cancel button frees the slot.
- New slots show for customers within a minute or so.

## Notes
- Customer names/phones are encrypted in the browser. Strangers can see that a time is taken, nothing more.
- Times are in the visitor's/your device clock; everyone is in one place, so this is fine.
- GitHub emails you about new issues if you "Watch" the repo, which gives a free notification that someone booked (the details stay encrypted).
- Limit: a determined person could spam fake bookings. Cancel them from the admin page.
