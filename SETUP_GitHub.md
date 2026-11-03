# RA Project Tracker: data stored in GitHub (one-time setup, about 10 minutes)

Link once live: **https://bhartilfe-tools.github.io/ra-tracker/**

**How it works:** the data is saved in the repo itself, in a file called `data.enc.json`. Every update a team member makes is one commit. The repo is public (GitHub Pages needs that), so the data and the GitHub token are kept **encrypted with the team passcode**. Anyone who opens the repo without the passcode sees only unreadable text.

> First check: on the office laptop, open **https://api.github.com** in the browser. If you see some JSON text, it works ✅. If it is blocked, the tracker cannot save from the office network, so tell me before doing the steps below.

## Step 1: Create the repo (on a personal network or phone hotspot, because github.com is blocked in the office)
1. github.com/bhartilfe-tools → **New repository** → name **ra-tracker** → **Public** → Create.
2. **Add file → Upload files** → upload only **index.html** → Commit.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch **main**, folder **/ (root)** → Save.

## Step 2: Create a token (only for this repo)
1. github.com → profile photo → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Name: `ra-tracker`. Expiration: 1 year. **Resource owner: bhartilfe-tools**.
3. Repository access: **Only select repositories → ra-tracker**.
4. Permissions → Repository permissions → **Contents: Read and write**. Nothing else is needed.
5. Generate, then copy the token (it starts with `github_pat_…`).
   - If the org shows "pending approval": go to the org's **Settings → Personal access tokens → Pending requests** and approve it. You are the org owner.

## Step 3: Admin setup in the tracker page
1. Open **https://bhartilfe-tools.github.io/ra-tracker/**. Because this is the first time, the **Admin setup** screen opens by itself.
2. Owner `bhartilfe-tools`, Repo `ra-tracker`, Branch `main`. Paste the token.
3. Set the **team passcode**: at least 10 characters. Use 3-4 random words plus a number (e.g. `Lantern-Copper-Velvet-42`), not a team/month pattern like `RA-Team@Nov2026`: the repo is public, so anyone can download the encrypted file and keep guessing. Enter it in both boxes.
4. Click **Save & connect**. The page creates `data.enc.json` (with the 20 MIS items) and `config.json` in the repo.
5. After about 1 minute, share the link and the passcode with the team, **privately** (WhatsApp/Teams, not email chains). Each member enters their name and the passcode once.

## Later
- **Token expired / changed:** page footer → **Admin setup** → paste the new token, enter the same passcode → Save.
- **Change the passcode:** Admin setup → enter the new passcode, and the old one under "Current passcode" → Save. Share the new passcode with the team.
- **Next FY months:** Admin setup → edit "Month columns" (e.g. `YTD Sep-27, Oct-27, …`) → Save.
- **Who changed what:** use the **History** button on the page, or check the repo's commits. Every commit message says who changed what.

## Keep in mind
- Anyone who has the passcode can edit the tracker. Keep the passcode within the RA team.
- **When someone leaves the RA team:** change the passcode **and** generate a new token (delete the old one in GitHub). Old encrypted copies stay in the repo's history, so the old passcode could still open the old token.
- **Token expires after 1 year:** set a reminder to create a new one before it expires (then Admin setup → paste the new token).
- On a shared office PC, untick **Remember on this device** (it keeps the passcode in that browser).
- Keep only MIS names, status, notes and file locations here. Don't put customer or policy-level data.
- If two people change **the same cell** at the same time, the second person gets a message ("X changed this…") and sees the latest value. Changes to different cells merge automatically.
