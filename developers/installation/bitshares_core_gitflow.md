## BitShares Core - GitFlow

### Development / Release / Bugfix Workflows

The purpose of this document is to describe and define how changes flow into our code and through the various stages of development until it finally goes into production.

The general idea is based on git-flow.

For our purposes, the general concept behind gitflow has been extended to allow for these additional needs:

1. We have two different types of releases, mainnet and testnet, with a master-like branch for each one.
2. We have to distinguish consensus-breaking changes (aka hardforks) from non-consensus-breaking changes.


***

<p align="center">
  <img src="https://github.com/cedar-book/btsdoc-portal/blob/master/developers/images/BitSharesCore-GitFlow-Base20180515.png" width="800" title="wallet-type">
</p>

***

### Goals To Achieve:

1. Maintain two independent release versions, testnet and mainnet.
2. Decouple development from releases, i. e. maintain the ability to create emergency bugfixes for current release without bringing incomplete new features into production.
3. Separate consensus-related changes from non-consensus-related changes.
4. Keep development branches compatible with mainnet.

### Basic Rules:

1. Development always happens in private feature-branches. The only exception is a change that must be distinguished in the destination branch (typical example: hardfork date in testnet).
2. Features are merged after they are reasonably complete, i. e. they come with unit tests that provide reasonable coverage and do not report any errors.
    1. "Completed" features that are not consensus-related are merged into "develop".
    2. "Completed" features that are consensus-related are merged into the "hardfork" branch, with a hardfork date in the far future.
    3. All merges into "develop" or "hardfork" are performed via github PR's and require review and approval from core developers (if the PR is created by a core dev at least one other core dev must review and approve).
    4. To maintain a clean history and make reviewing and merging easier, feature branches must be rebased onto current "develop" (or "hardfork") before creating a PR.
    5. Merges are always done as real merges, not as fast-forwards, and not squashed.
3. Core devs coordinate regular merges from "develop" into "hardfork".
4. Both "develop" and "hardfork" should always remain compatible with mainnet, i. e. a full replay must be possible.



***


