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




***


