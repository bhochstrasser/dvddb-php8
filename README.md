# DVDdb PHP 8 Compatibility Edition

This package is a compatibility-focused modernization of the original DVDdb application by James Gurney.

Its purpose is deliberately narrow: keep the original DVDdb database schema, user interface, navigation, and behavior as intact as practical while allowing the application to run on a modern PHP 8.x stack.

This edition does **not** include the later Album Manager / physical binder-location extensions. Those are maintained separately in the enhanced DVDdb PHP 8 + Album Manager edition.

## What changed

- Converted legacy short PHP opening tags (`<?`) to `<?php`.
- Replaced the removed PHP `mysql_*` extension with `mysqli`.
- Preserved the original `doquery()` database abstraction so most of DVDdb could remain close to the upstream code.
- Added small compatibility helpers for functionality removed from modern PHP, including `mysql_result()`-style access, insert IDs, database errors, error numbers, and server-version information.
- Fixed legacy unquoted array keys that are fatal on PHP 8.
- Removed obsolete `magic_quotes_gpc` assumptions.
- Corrected menu-array initialization and related PHP 8 type errors.
- Added conservative defaults for request variables where needed to avoid PHP 8 undefined-key problems.
- Fixed movie-list/print filter arrays that PHP 8 no longer permits to be appended to after string initialization.
- Fixed the legacy unquoted `date(Y)` call on the Search page.
- Retained the original themes, preferences, movie lists, search, loans, statistics, settings, and administrative pages.

## Database compatibility

This compatibility edition is intended to work with an existing DVDdb 0.6-era database without adding the Album Manager schemas or changing the movie data model.

As with any old application being moved to a new runtime, make a database backup before upgrading and test against a copy first when practical.

## Configuration

Edit `inc/db.php` and replace the placeholders with your MySQL/MariaDB credentials:

```php
"host" => "localhost",
"username" => "xxx",
"password" => "xxx",
"dbname" => "xxx",
```

The PHP installation must have the `mysqli` extension enabled.

## Suggested upgrade/test procedure

1. Back up the existing DVDdb files and database.
2. Test against a restored copy of the database if possible.
3. Upload this compatibility edition to a separate directory first.
4. Configure `inc/db.php`.
5. Select a supported PHP 8.x runtime with `mysqli` enabled.
6. Test login and account creation.
7. Test My Movies, All Movies, Search, and Print Results.
8. Test movie view/add/edit/delete, loans, statistics, settings, themes, and administrative pages.
9. Once satisfied, deploy over the legacy PHP application while retaining your backup.

## Scope: intentionally unchanged

This is a compatibility release, not a security rewrite or redesign. DVDdb still contains architecture and conventions appropriate to its original era, including legacy authentication/password handling, hand-built SQL in portions of the application, and legacy HTML/CSS.

Those behaviors are intentionally outside the scope of this edition so that users with an existing DVDdb installation can move to PHP 8 with the smallest practical functional change.

## Album Manager edition

A separate enhanced edition adds physical DVD binder management, including Album/Page/Sleeve locations, multi-disc occupancy, configurable binder dimensions, move/swap operations, and location columns in movie listings.

Use this compatibility edition if your goal is simply to keep the original DVDdb application running on PHP 8.

## Credits and license

DVDdb was created by **James Gurney** and distributed under the GNU General Public License (GPL).

The 2026 compatibility work preserves the original application and authorship while adapting the code for PHP 8.x. Original copyright and GPL notices should be retained when redistributing the software.

PHP 8 modernization and runtime testing were performed by Bryan Hochstrasser with development assistance from ChatGPT/OpenAI.

