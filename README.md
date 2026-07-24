# 📓 Inventory Notebook

A single-page, notebook-styled inventory tracker that uses **NFC tags** to
quickly add/subtract item counts by tapping your phone against a physical
tag stuck on a fridge, freezer, shelf, or bin. All data is stored locally
in the browser (`localStorage`) — no backend or database required.

---

## 1. Setup (GitHub Pages)

1. Add `inventory.html` to your GitHub Pages repo (e.g. commit it to the
   root, or to a subfolder like `/inventory/`).
2. Enable GitHub Pages for the repo if you haven't already
   (**Settings → Pages → Build and deployment → Deploy from branch**).
3. Once deployed, your page will be reachable at something like:

   ```
   https://<your-username>.github.io/<repo-name>/inventory.html
   ```

4. Open that URL on your **phone** (the device you'll use to tap tags) —
   everything runs client-side, so no server setup is needed.

---

## 2. Adding a "Place"

A **place** is any physical storage location — fridge, freezer, pantry,
garage shelf, etc.

- Click **"+ new place"** on the tab bar (left side) and name it.
- Each place gets its own colored notebook tab you can switch between.
- To remove a place (and everything stored in it), use **"remove place"**
  at the top of its page.

---

## 3. Adding an Item

1. Open the place it belongs to (click its tab).
2. At the bottom of the list, type the item name and a starting count,
   then click **Add**.
3. A popup will immediately show the **tag URL** for that item — this is
   what you'll write onto a physical NFC tag (see below).
4. You can re-open this URL anytime later via the **"tag link"** button
   next to any item.

---

## 4. Writing the URL to a Physical NFC Tag

You'll need an NFC-writing app — **NFC Tools** (free, Android & iOS) is
recommended.

1. Open NFC Tools → **Write** → **Add a record** → **URL/URI**.
2. Paste in the tag URL shown by the app (looks like:
   `https://<your-username>.github.io/.../inventory.html?tag=item-ab12cd`).
3. Tap **Write** and hold your phone against the physical NFC tag/sticker.
4. Stick the tag on the relevant fridge shelf, freezer bin, cabinet, etc.

---

## 5. Using It Day-to-Day

- **Tap a written tag** with your phone → the page opens automatically →
  a sticky-note popup appears showing that item's current count, with
  **+ / −** buttons to adjust it → tap **Done** when finished.
- **Tap an unknown/blank tag** (one you haven't registered yet) → the app
  shows a "Name this item" form instead, so you can register it on the
  spot (choose or create a place, name it, set a starting count).
- You can also add/adjust/remove items directly from the notebook page
  itself, without needing to tap a tag — useful when first setting things
  up or doing a manual recount.

---

## 6. Exporting to CSV

Click **⬇ Export CSV** at the top of the page at any time to download a
snapshot of your full inventory.

- The file is automatically named with **today's date**, e.g.:
  ```
  inventory-2026-07-25.csv
  ```
- Columns: `Location, Item, Count, Tag ID`
- Useful for backups, sharing a snapshot, or opening in Excel/Google
  Sheets to review stock over time.

> Note: exporting does **not** clear or reset your data — it's just a
> read-only snapshot at that moment.

---

## 7. Data & Backups

- All data lives in your browser's `localStorage`, tied to the specific
  device + browser you're using. It will **not** automatically sync
  across devices.
- Because of this, it's a good habit to **export a CSV occasionally** as
  a backup, especially before clearing browser data or switching phones.
- If you outgrow local-only storage (e.g. want it synced across your
  phone and laptop), the data model (`locations[]` + `items[]`) is
  already structured simply enough to move into a backend like Supabase
  later without redesigning the app.

---

## 8. Troubleshooting

| Issue | Likely cause |
|---|---|
| Tapping the tag does nothing | NFC might be off in phone settings, or the tag wasn't written correctly — re-check in NFC Tools |
| Tag opens the page but no popup appears | The URL might be missing the `?tag=...` parameter, or it was mistyped when written |
| Counts reset unexpectedly | Browser data (localStorage) may have been cleared — restore from your latest CSV export manually if needed |
| Page opens but shows "Name this item" for a tag you already registered | The tag might have been overwritten with a different/new random ID — check the URL currently on the tag against the item's "tag link" in the app |
