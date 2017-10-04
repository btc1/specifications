
# SegWit2x

<pre>
  PCS: 2017-0002
  Title: Block size increase to 2MB coupled with Segwit activation
  Authors: Sergio Demian Lerner
  Status: Draft
  Type: Standards Track
  Created: 2017-07-01
  License: BSD-2-Clause
           OPL
</pre>

## Abstract

This BIPs describes a one-time increase in the maximum non-witness block size from 1MB to 2MB, triggered by the activation of segwit as of BIP91, but delayed approximately 3 months after segwit activation.

To prevent DoS attacks, transaction serialized size is limited to 1,000,000 bytes, excluding witness data.


## Copyright

This BIP is dual-licensed under the Open Publication License and BSD 2-clause license.

## Motivation

* Enabling Segwit
* Reducing temporarily the fee pressure until other scaling techniques such as the Lighntning Network, sidechains, drivechains and extension blocks prove to be useful or not for Bitcoin scaling.
* Maximum transaction size is kept, to maximize compatibility with current software and prevent algorithmic and data size DoS's.

## Rationale

The "transaction pattern" is defined as the average number and size of transaction inputs and outputs in a block.
Assuming the current transaction pattern is replicated in a 2 MB plain-sized block that is 100% filled with transactions, then the witness-serialized block would occupy 3.6 MB [1]. This is considered safe by many users, companies, miners and academics [2]. 

## Specification


### Consensus

* The no-wit block size is defined as the serialized block size without witness programs.
* Deploy a modified BIP91 to activate Segwit. The BIP9 version bit 4 is redefined as the segwit2x signal.
* If segwit2x activates at block N, then at block N+12960 the block weight limit rises from 4,000,000 to 8,000,000. Also the maximum sigop cost per blocks rises from 80,0000 to 160,000.  Both changes represent hard-forks.
* The block that activates the hard-fork must have a no-wit block size greater than 1,000,000 bytes.
* Any transaction with a non-witness serialized size exceeding 1,000,000 is invalid.

### Non-consensus

* BIP91 is modified so the signal "segsignal" is replaced by "segwit2x". This affects the rpc mining interface (getblocktemplate).


## Backward compatibility

Older clients are not compatible with this change.  The first block having no-wit size exceeding 1,000,000 bytes will partition older clients off the new network.

## Discussion

In the short term, an increase is needed to continue to facilitate
network growth, and buy time for more comprehensive solutions to be
developed and tested, such as the Lightning Network, sidechains, drivechains and extension blocks.
This reduces the fee pressure on users and companies creating on-chain transactions, matching market expectations and preventing further market disruption.

The restriction of the size of a non-witness serialized transaction prevents worsening quadratically the effects of the O(N^2) hashing attack vector but this BIP is not a final solution to this problem. This BIP doubles the worst case block processing time. However future soft-forks may tackle this problem directly by limiting sigops per input, per transaction, or total bytes hashed per transaction. 
Note that the maximum transaction size can exceed 1 MB by using witness programs, but Signature checks in witness programs do not require full transaction re-hashing and therefore do not worsen the attack vector.
  

## Implementation

https://github.com/btc1/bitcoin branch segwit2x

## Acknowledgements

Thanks to Jeff Garzik and the Segwit2x group for the reference code, corrections and suggestions.

## References

[1] https://github.com/SergioDemianLerner/SegwitStats
[2] http://fc16.ifca.ai/bitcoin/papers/CDE+16.pdf

