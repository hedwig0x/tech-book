# Implementation Alignment Notes

This page summarizes the key doc-vs-runtime mismatches identified during this review.

## Why this exists

The tech-book mixes architecture intent and implementation examples.
That is useful, but examples can become stale faster than architecture principles.

To avoid confusion:

- use this book for design intent,
- use current `fluentbase` docs and active release branches for exact behavior.

## Mismatches found in this review

### 1) Sidebar and chapter coverage drift

- `SUMMARY.md` had dead placeholders and missing links to existing chapters.
- Rollup-related chapters were present but empty.

**Action in this PR:** fixed summary links and filled L2/proof/DA chapters with architecture-level content.

### 2) Runtime family statements too absolute

Some text implied fixed support/runtime labels across all releases.
In practice, runtime availability and activation can vary by release/network.

**Action in this PR:** reworded to mark runtime-family lists as release-dependent where needed.

### 3) Syscall examples treated as if permanent

The system-call chapter includes concrete signatures/IDs from a specific snapshot.
Those are valuable, but not always current.

**Action in this PR:** retained detail but added explicit warning that current SDK/runtime docs are authoritative.

### 4) Fluentbase module list drift

The previous Fluentbase module section listed crate names that no longer match current repo layout exactly.

**Action in this PR:** updated module overview to current crate families and added a note about historical names.

### 5) Genesis/runtime status wording

Some runtime status statements in the genesis chapter read as hard invariants.

**Action in this PR:** added release-dependent status note for genesis/runtime contract set.

## Reader workflow (recommended)

When implementing something production-sensitive:

1. Read architecture intent in this book.
2. Cross-check `fluentbase/docs` for current behavior.
3. Verify against active release branch before shipping.
