# RA Project Tracker: notes for future changes

- Hosted on GitHub Pages: https://bhartilfe-tools.github.io/ra-tracker/ (repo `bhartilfe-tools/ra-tracker`).
- Only **index.html** is uploaded by hand. `data.enc.json` and `config.json` are created by the page's Admin setup. Never edit them by hand.
- **Storage:** no Google Sheet and no server. The page reads and writes `data.enc.json` through the GitHub Contents API (api.github.com) using a fine-grained token (Contents: Read and write on this repo only).
- **Encryption:** AES-GCM-256. The key comes from the team passcode via PBKDF2-SHA256 (250,000 iterations).
  - `data.enc.json` = `{v, alg, kdf, iter, salt, iv, ct}`.
  - `config.json` = `{owner, repo, branch, path, tok:{same envelope, encrypting {token}}}`.
- **Decrypted data shape:**
  `{ v:1, months:["YTD Sep-26","Oct-26",…], rows:[{ "ID":"RA-01", "MIS / Monthly trends / Repository", "Responsibility", "File Name", "File Location", "Last 5 years?", <month columns>, "Remarks", "Updated By", "Updated At" }], log:[{t,u,id,f,o,n}], updated, updatedBy }`
- **Month cell format:** `"<Status>"` or `"<Status> | <note>"`, where Status is one of Done / In progress / Pending / NA.
- **Saving:**
  - Each change re-reads the latest file and checks that the cell still holds the value the user saw. If it does not, the user gets a conflict message.
  - It then re-encrypts and commits with the file's `sha`. On a 409/422 it retries, so changes to different cells merge.
- **Any change to the data shape must keep reading old files.** Otherwise the team's existing data will not load.
