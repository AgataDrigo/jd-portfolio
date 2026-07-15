# JdPortfolio

A single-page academic portfolio/CV site, built with Angular. The site's text content (bio, education, publications, etc.) lives in one plain data file, so it can be updated without touching any code.

## Updating the site content

All of the content on the page lives in one file:

```
public/content.json
```

The site is connected to Cloudflare, which watches the `main` branch: **as soon as a change is committed to `main`, the live site rebuilds and updates automatically**, usually within a minute or two.

### How to edit it

1. Go to the repository on GitHub and open `public/content.json`.
2. Click the pencil icon (top right of the file view) to edit it in your browser.
3. Make your changes (see field guide and formatting rules below).
4. Scroll down to "Commit changes":
   - For a small, low-risk fix (fixing a typo, updating a date), you can commit directly to `main` — it'll go live right away.
5. Click **Commit changes**.

If you'd rather edit locally: clone the repo, open `public/content.json` in any text editor (including Notepad), save your changes, then commit and push them.

### Formatting rules (important!!)

`content.json` is a JSON file, which is picky about punctuation. Breaking these rules won't crash anything permanently, but the page will show "Couldn't load page content" until it's fixed:

- Every piece of text must be wrapped in **double quotes**: `"like this"`.
- Every entry in a list needs a **comma** after it — except the very last one.
- If your text itself contains a double quote (`"`), put a backslash before it: `\"like this\"`.
- Don't remove or rename anything to the **left** of a colon (e.g. `"degree":`, `"years":`) — those are field names the app relies on. Only change the text to the **right** of the colon.
  - If you need to, a more hands on alteration will be needed.
- Keep matching curly braces `{ }` and square brackets `[ ]` — if you copy an entry to duplicate it, make sure you copy the whole block, including its opening and closing brace.

If something goes wrong, the site will show a friendly error message instead of breaking silently — just go back and check for a missing quote or comma near your last edit, or undo the commit on GitHub ("Revert" button on the commit page).

**Tip:** if you're not sure your edit is valid, paste the whole file into a free JSON validator like [jsonlint.com](https://jsonlint.com) before committing — it'll point out exactly where the syntax is broken.

### Field guide

| Field                                              | What it is                                                                                                                                                   |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `name`                                             | Full name, shown in the header and page title.                                                                                                               |
| `tagline`                                          | Short one-line description under the name.                                                                                                                   |
| `university`, `location`, `email`                  | Contact/affiliation details.                                                                                                                                 |
| `photoUrl`                                         | Path to the profile photo (see "Updating the photo or CV" below).                                                                                            |
| `linkedinUrl`, `academiaUrl`, `blueskyUrl`         | Profile links. Leave as `""` (empty quotes) to hide a link.                                                                                                  |
| `cvUrl`                                            | Path to the downloadable CV PDF.                                                                                                                             |
| `about`                                            | A list of paragraphs for the About section. Add or remove lines to add/remove paragraphs.                                                                    |
| `education`                                        | A list of entries, each with `degree`, `institution`, `years`, and `detail`. Copy an existing entry to add a new one.                                        |
| `researchInterests`                                | A list of short text bullet points.                                                                                                                          |
| `publications.peerReviewed` / `publications.other` | Two separate lists of publication citations (plain text strings).                                                                                            |
| `selectedPresentations`                            | A curated list of presentations shown on the page. Keep this short — this section deliberately doesn't list everything; the full list belongs in the CV PDF. |
| `teaching`                                         | A list of entries, each with `title`, `institution`, `years`.                                                                                                |
| `teachingNote`                                     | One paragraph of extra teaching context, shown below the teaching list.                                                                                      |
| `fellowships`                                      | A list of short text bullet points.                                                                                                                          |
| `languages.modern` / `languages.historical`        | Two paragraphs of text describing language proficiency.                                                                                                      |

### Adding or removing a list item

To add an entry (e.g. a new publication or teaching entry): copy an existing one in that list, paste it right below (or above), add a comma after the entry above it, and edit the copied text. For simple lists (like `researchInterests` or `fellowships`), each entry is just a quoted string; for entries with `institution`/`years`/etc. (like `education` or `teaching`), copy the whole `{ ... }` block.

To remove an entry, delete the whole block/line for it, and make sure the entry before it doesn't end with a trailing comma if it's now the last one in the list.

### Updating the photo or CV PDF

Both files live in `public/`:

- `public/profile.jpeg` — the profile photo.
- `public/Jasmim-Drigo-CV.pdf` — the downloadable CV.

The easiest way to update either: upload a new file with the **same name** to the `public/` folder on GitHub (this overwrites the old one) — no changes to `content.json` needed. If you upload a file under a different name instead, update `photoUrl` or `cvUrl` in `content.json` to match the new filename (paths start with `/`, e.g. `/my-new-photo.jpg`).
