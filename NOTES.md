# Patch Notes

## Summary of changes

I fixed four high-value issues in the task tracker.

1. Corrected the SQL search condition so title/description matching is grouped correctly with status and archived filters.
2. Changed pagination to be handled by the database using Spring Data `Page` and `Pageable` instead of loading all matching tasks into memory.
3. Removed an unnecessary `Thread.sleep()` that artificially delayed API requests.
4. Improved the frontend request lifecycle by cancelling stale requests with `AbortController` and correctly managing loading and error states.

## What I chose not to change

I did not fix the missing favicon, dependency audit warnings, or unrelated warnings from Spring Boot because they were outside the highest-value functional issues and would increase the scope of the patch.

## Biggest remaining risk

The biggest remaining risk is that the application has limited automated test coverage. Future changes could therefore introduce regressions without being detected immediately.

## Tools/AI used

I used ChatGPT to review the codebase, identify potential issues, explain the root causes, and help plan a focused patch. I reviewed and tested the changes myself, including API requests, pagination, validation, frontend behavior, and the production build.