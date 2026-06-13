---
description: Verify all done conditions are met before proceeding to git-flow
---

## Steps

1. Check each item below. Mark as pass or fail.

- [ ] Requested feature is implemented
- [ ] Changes follow relevant docs
- [ ] No unrelated files modified
- [ ] If contracts changed, docs are updated

2. If any item fails:
   - Fix it, then re-run `/npm-test` and re-check this list.
   - If fixing requires a change that conflicts with a doc, or two docs conflict with each other — stop and report to the user before proceeding.

3. If all relevant items pass → proceed to `/git-flow`.
