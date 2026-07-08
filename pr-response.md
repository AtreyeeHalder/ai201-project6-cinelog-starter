# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**Comment on line R12 of `services/watchlist_service.py`:** `save_to_watchlist()` should follow the project's naming convention. Compare with `add_to_collection()` — the pattern here is `verb_to_noun`. Please rename to `add_to_watchlist()` and update all call sites.

**What I did:** Renamed `save_to_watchlist()` to `add_to_watchlist()` in `services/watchlist_service.py` and updated all call sites.

**How I verified:** Conducted project-wide search of `save_to_watchlist` in VS Code to confirm no call sites are missed.

## Comment 2 — Deduplication
**Comment on line R30 of `services/watchlist_service.py`:** What happens if a user calls this with a film that's already on their watchlist? The current implementation would add a duplicate entry. Please handle this case.

**What I did:** Added deduplication logic to `add_to_watchlist()` in `services/watchlist_service.py` by raising an `AlreadyInWatchlistError` with the message "Film '{film_id}' is already in this user's watchlist" if the film is already in the user's watchlist.

**How I verified:** Ensured pattern consistency by following the same pattern as `add_to_collection()` deduplication handling in `services/collection_service.py`

## Comment 3 — Missing test
**Comment:** Please add a test for the case where film_id doesn't exist in the database. Look at the existing tests in test_collection.py — the pattern is there.

**What I did:** Created a new file `tests/test_watchlist.py`. Wrote `test_add_to_watchlist_nonexistent_film_raises` test for `add_to_watchlist()` to ensure `FilmNotFoundError` is raised when adding a film_id that doesn't exist in the database. Followed the same fixture and assertion structure as `test_add_to_collection_nonexistent_film_raises` in `tests/test_collection.py`.

**How I verified:** Ran the test `pytest tests/test_watchlist.py -v` to confirm it passes. Ran the full test suite `pytest tests/ -v` to confirm nothing is broken.

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->