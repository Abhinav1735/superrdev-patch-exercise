# Patch Notes

## Summary of changes
- Fixed task search predicate grouping so archived tasks and status filters are applied consistently to both title and description matches.
- Moved pagination into the database query and retained a separate count query, avoiding loading every matching task into application memory.
- Removed the artificial per-request `Thread.sleep()` delay.
- Added validation for invalid page/pageSize and status values, returning HTTP 400 instead of failing with an uncontrolled exception.
- Fixed frontend request lifecycle handling: stale requests are aborted, errors are cleared on a new request, and loading state is reset reliably.
- Updated the Oracle reference query to match the corrected search predicate.

## What I chose not to change
I did not rewrite the UI, introduce new libraries, or redesign the API. I also left broader performance concerns such as indexing for a larger follow-up because the exercise calls for a focused patch.

## Biggest remaining risk
Search still uses wildcard `LIKE` matching, which can become expensive at scale. Appropriate database indexes or full-text search would be the next investigation depending on the production database and query patterns.

## Tools/AI used
I used ChatGPT to review the codebase, identify likely correctness and performance issues, and reason through focused fixes. I reviewed and adjusted the changes rather than applying a broad rewrite.
