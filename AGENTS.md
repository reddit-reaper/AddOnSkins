# World of Warcraft Addon Maintenance Instructions

## Project Goal

This repository contains an abandoned World of Warcraft addon that is being restored and maintained.

The primary goal is to restore compatibility with the current World of Warcraft client while preserving the addon's original behavior, configuration, user experience, and SavedVariables whenever possible.

## Maintenance Rules

* Prefer minimal compatibility fixes over large rewrites.
* Do not refactor working code simply because a newer style exists.
* Preserve existing behavior unless a change is required to restore functionality.
* Preserve SavedVariables names and formats unless a migration is absolutely necessary.
* Do not rename public addon APIs without a specific reason.
* Do not remove functionality merely because it uses an older implementation.
* Determine the root cause of errors before adding defensive nil checks.

## World of Warcraft API Compatibility

When encountering a Blizzard API that appears deprecated, removed, renamed, or behaviorally changed:

1. Identify what the old API did.
2. Determine when or why it changed.
3. Identify the current supported API or implementation.
4. Search the entire repository for other uses of the same API.
5. Make the smallest compatibility change necessary.
6. Preserve existing addon behavior wherever possible.

Pay particular attention to:

* Removed global functions
* C_* namespace migrations
* Event argument changes
* Frame API changes
* Unit APIs
* Spell APIs
* Item APIs
* Tooltip APIs
* Container/bag APIs
* Talent and specialization APIs
* Secure execution
* Protected frames
* Combat lockdown
* SecureActionButton behavior
* Hooks and secure hooks
* XML template changes

## Third-Party Libraries

Do not modify bundled third-party libraries merely because they are old.

First determine:

* Which libraries are bundled.
* Whether the addon actually uses them.
* Whether the library itself is incompatible with the current WoW client.
* Whether updating the library would introduce breaking API changes.

Prefer updating a library through its established upstream version rather than manually rewriting library internals.

## Debugging

When given a Lua error or stack trace:

1. Trace the complete call path.
2. Identify the actual root cause.
3. Inspect related callers and dependent functions.
4. Determine whether the problem is caused by a WoW API change or an addon bug.
5. Search for other occurrences of the same problem.
6. Make the smallest appropriate repair.

Do not hide errors with broad `pcall`, excessive nil checking, or silent failure unless there is a valid reason.

## Change Discipline

Before making a significant multi-file change:

* Explain the problem.
* Explain the proposed solution.
* Identify which files need modification.

When making changes:

* Keep modifications focused.
* Do not perform unrelated cleanup.
* Do not reformat entire files.
* Do not rename large numbers of variables unnecessarily.
* Do not change indentation or formatting outside the affected code unless needed.

After making changes:

* Summarize exactly what changed.
* Identify any assumptions.
* Identify anything that still needs to be tested inside World of Warcraft.

## Testing Reality

World of Warcraft addon runtime behavior cannot necessarily be validated entirely through static analysis.

Clearly distinguish between:

* Problems confirmed from source code.
* Problems strongly indicated by API changes.
* Changes that still require testing inside World of Warcraft.
