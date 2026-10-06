# Notes

## Summary of Changes

I reviewed the task search flow across the Spring Boot backend, React frontend, and SQL query files. I fixed an SQL filtering bug where archived tasks could bypass the archive filter because of missing parentheses around the title/description OR condition.

I removed an artificial `Thread.sleep()` from the search API that introduced unnecessary request latency. I also added validation for invalid status, page, and pageSize parameters so invalid client input returns a 400 response instead of causing server errors.

On the frontend, I fixed pagination not resetting when the search query or status filter changes. I also improved the task-fetching hook so loading and error states are handled correctly and stale requests cannot overwrite newer results.

## What I Chose Not to Change

I avoided large architectural changes, database redesigns, UI redesigns, and unrelated refactoring. The existing structure was sufficient for the exercise, so I focused on bugs that directly affect correctness, reliability, performance, and user experience.

## Biggest Remaining Risk

The biggest remaining risk is that pagination is performed in memory after retrieving all matching tasks from the database. This could become inefficient as the task table grows because the API loads all matching records before selecting one page.

## Tools / AI Used

I used ChatGPT to help inspect the code, identify potential bugs, and reason about SQL operator precedence, API validation, and React state handling. I reviewed the suggested changes and adapted them to the existing project structure rather than blindly applying generated code.
