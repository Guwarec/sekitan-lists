# SEKITAN Lists

Word lists for the **SEKITAN** mentalism iOS app.

These files are downloaded by the app at runtime from this repo,
served by [Cloudflare Pages](https://sekitan-lists.pages.dev).

## Folder structure

```
001_Names/        First names by frequency
002_Words/        Common words by language
003_Destinations/ City names + countries (with airport-style links)
004_ZipCode/      Postal codes by country
005_Films(Series)/Movies and TV shows
```

The iOS app walks the **entire repository tree recursively**
(`/git/trees/HEAD?recursive=1`), so subfolders are fine —
they show up flat in the in-app preset picker.

## File format

- **Encoding**: UTF-8 (no BOM — but the app strips BOM if present)
- **Separator**: `;` is preferred. `,` works too, with proper CSV
  quoting (`"Foo, Bar"`) for fields containing the separator.
- **Header**: first line, examples
  - `Words`
  - `Words;Score`
  - `Words;Link;Score`
  - At least 2 recognized header keywords required
    (`Words`/`Word`/`Mot`, `Score`/`Frequency`/`Freq`,
    `Link`/`Association`/`Assoc`/`Payload`/`Info`).
- **Rows**: one entry per line, e.g. `Paris;France;1000`

## "NEW_" files

Some files are stored twice in this repo, both as the original
and as `NEW_*.csv`. The `NEW_` versions:

- Use `;` as separator (instead of `,`) → no need for quoted fields
- Strip the UTF-8 BOM (Excel "CSV UTF-8" mode adds one)

These were generated as a one-shot fix for the original SEKITAN V1.9
parser limitations. Newer parsers handle quoted CSV and BOM
transparently, so the originals work too. Use whichever you prefer.

## Supported scripts (T9 lookup)

The SEKITAN T9 builder maps Latin (all variants), Hebrew, and a few
extended Latin alphabets to the T9 keypad. Files in scripts NOT
mapped will load (no crash) but the words will not be matchable
during a scan:

- ✅ Latin (most languages), Hebrew
- ⚠️ Arabic, Greek, Cyrillique, Japanese, Korean, Thai, Hindi
  (loaded but silently dropped from the T9 dictionary)

## Adding a new list

1. Make a UTF-8 file (no BOM). Excel: "CSV UTF-8 (with comma)"
   then strip the BOM, or use Numbers/LibreOffice.
2. Header: `Words;Score` (mandatory header for the parser to take
   the file in structured mode).
3. One word per line, optional `;score` and `;link` columns.
4. Drop in the appropriate folder (or root), commit, push.
   The app will pick it up on the next preset refresh.
</content>
</invoke>