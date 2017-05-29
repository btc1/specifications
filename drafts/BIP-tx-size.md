<pre>
  BIP: xxx
  Layer: Consensus (hard fork)
  Title: Transaction size limits
  Author: Jeff Garzik <jgarzik@gmail.com>
  Status: Draft
  Type: Standards Track
  Created: 2017-05-29
</pre>

==Abstract==

Transaction serialized size is limited to 1,000,000 bytes, excluding witness data.

==Motivation==

# Maximize compatibility with current software.
# Hard cap on some algorithmic and data size DoS's.

==Specification==

# MAX_TX_BASE_SIZE is defined as 1,000,000 bytes.
# Any transaction with a non-witness serialized size exceeding MAX_TX_BASE_SIZE is invalid.

==Backward compatibility==

This is compatible with existing software.  No current software will generate a transaction larger than 1,000,000 bytes, because that transaction will not be relayed or mined.

