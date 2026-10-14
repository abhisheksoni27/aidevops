<!-- SPDX-License-Identifier: MIT -->
<!-- SPDX-FileCopyrightText: 2026 Marcus Quinn -->

# v3.39.31 unpublished release aggregation recovery

## Summary

Recover the unpublished v3.39.31 release owned by source PR #34603. The original
protected-main release PR #34609 merged, but the public tag was not pushed.
Cross-host tag recovery now succeeds after #34636, including local signature
verification. Publication stops because the legacy signed release tree differs
from the current main tree. No published tag is to be replaced.

The operator authorized a reviewed aggregation PR and subsequent publishing
recovery. This document records the source set verified against GitHub merged-PR
records and first-parent history, not a substitute for the release verifier.

## Immutable reviewed base

- Aggregation PR: #34650, bound to the final commit's immutable source trailers.
- Published baseline: v3.39.30 at c3271d3ba920fec06de6ebc98a03bbb2d1850416.
- Aggregation base: 7cdcdd35d33c729b974d836da80027c6035d7a0d.
- Original signed release commit: 92ff98fab7e7bd834b1286e6e1901d23eca96aba.
- Original provisional tag object: a1af8e65e381530579d09524808d7dd96bdd5ec2.

## Verified source manifest

```text
34592@555a0b4731bac6dd7ed70b34200ba920cd099ed5
34593@fbca8d268c9ed2ddfe99911226976003c1ed1a68
34595@1652e0be6cdcb746bea050e4f70ee6949e97fbdc
34597@ee243cf0ed0bb2095eb67ed45191f50e35b6ffdc
34599@52868c34e70433703b844b09bfc7762339513ace
34602@bd7cc3917e8272c20398c998f0325ef663476bf3
34603@82ce52953247f2701360b27ce5c48fce1684a019
34607@4c4f64f2eda525d084c546d08ab083c5d3e2aa0d
34608@a91659a16f92910d4e61ef13f390625335d86839
34609@87f6ed824e51855e542e473e70f4fc2954091561
34610@a790112df900e9f771a80168353a30dad8db14a0
34612@dd60235d9a64676042e407fc4736f8b55155a1f1
34616@3adab8a8ce74b624554f42b6c056040268b5b424
34623@10d1a39a8424c0e88cbf29c2c42984e25ced9eb9
34624@ce14ad04df09ae761cbbe26810dbfe4d94be1186
34626@95b7f42c5f832167e492d30251dc4837fd996ee6
34627@34b73dff4ee80017a255291eee15f8b9669012db
34634@c7428c4a82a5723c26f7fa521c0208b952131e30
34635@45cf52907891a08715e521a95fb73326a8250d08
34636@92fa077ab0824e9303b96a8ebe41695a5335a79d
34645@7cdcdd35d33c729b974d836da80027c6035d7a0d
```

## Files and reference pattern

This PR changes only this recovery evidence document. Its final immutable commit
and squash-merge message must contain `Aidevops-Release-Aggregator-PR` identifying
this PR and one `Aidevops-Release-Aggregates` trailer per source above.

Reference contracts: `.agents/workflows/release.md`, legacy aggregation recovery;
`.agents/reference/release-aggregation-recovery.md`; and
`.agents/scripts/release-provenance-helper.sh`, aggregate-base verification.

## Verification and continuation

The original reconcile passed signed tag verification and stopped before public
mutation at the main-tree guard. Source discovery used `resolve-source --snapshot`
with immutable pins to the published v3.39.30 baseline and the aggregation base.
The default preview incorrectly selects the recovered unpublished local tag as
its baseline; explicit published-baseline pinning avoids that discovery problem
without changing publication guards.

Before merge, confirm the reviewed base still equals upstream main and run the
required PR gates. Merge by squash with the complete terminal trailer block.
If main advances, refresh the aggregation with the complete new source set.
After verified merge at the exact tip, run `recover-aggregate 34603` for v3.39.31
with the complete expected source set, then observe its protected-main queue.
Completion requires verified GitHub, npm, Homebrew, deployment, and terminal
receipt evidence. Missing evidence remains pending or blocked, never success.
