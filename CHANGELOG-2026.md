# DVDdb PHP 8 Compatibility Edition — 2026 Changelog

This changelog covers the compatibility-only edition of DVDdb. It intentionally excludes the later Album Manager and physical-location features.

## PHP 8 modernization

- Converted legacy PHP short opening tags to standard `<?php` tags.
- Migrated database access from the removed `mysql_*` extension to `mysqli`.
- Kept DVDdb's original `doquery()` abstraction and added compatibility helpers where old MySQL-extension behavior was required.
- Added modern helpers for result access, insert IDs, MySQL error/error-number reporting, and database server information.
- Fixed PHP 8 fatal errors caused by legacy unquoted array keys.
- Removed obsolete `magic_quotes_gpc` handling assumptions.
- Corrected array initialization patterns that PHP 8 treats more strictly than historical PHP releases.
- Added request-variable defaults where necessary to avoid undefined-key warnings/errors on modern PHP.

## Runtime fixes found during live testing

- Fixed menu rendering/type handling so pages no longer stop immediately after the navigation bar on PHP 8.
- Fixed `My movies` / filtered movie-list handling by initializing the filter collection as an array rather than a string before using `$filter[]`.
- Applied the same filter-array correction to Print Results.
- Fixed Search's legacy `date(Y)` expression by quoting the date format (`date("Y")`).
- Corrected additional PHP 8 compatibility issues discovered while exercising the original navigation and administration screens.

## Preserved behavior

The compatibility edition intentionally retains the original DVDdb:

- 0.6-era database/data model
- movie browsing and filtering
- search
- add/edit/delete movie workflows
- loans
- statistics
- user settings and preferences
- per-user themes and site default theme behavior
- administrative pages and lookup-table editing
- original visual themes and server-rendered UI

## Not included in this edition

The following belong to the separate enhanced Album Manager edition and are deliberately **not** part of this compatibility release:

- `movie_location`
- `album_config`
- Album Manager
- Album/Page/Sleeve or compact Location columns
- multi-disc sleeve reservations
- binder-aware navigation
- move/swap and physical-collision management

This separation provides a straightforward upgrade path for existing DVDdb users who only want the original application to run under PHP 8.

## Testing status

The compatibility work was developed through both static PHP syntax checking and live runtime testing against a restored DVDdb database. Core menu options and original application workflows were exercised during the restoration project, with runtime errors corrected as they were found.

## Credits

DVDdb is the original work of **James Gurney** and was released under the GNU General Public License (GPL).

2026 PHP 8 modernization and testing: **Bryan Hochstrasser**, with development assistance from **ChatGPT/OpenAI**.
