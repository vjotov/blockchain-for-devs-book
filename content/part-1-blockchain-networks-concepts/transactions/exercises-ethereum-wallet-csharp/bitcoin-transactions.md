# Bitcoin Transactions

In this chapter we will learn more about the UTXO model mentioned previously, by taking a deep dive into Bitcoin transactions.

## What's a Bitcoin Transaction?

A Bitcoin transaction is basically a transfer of value - a data package with a specific structure that is sent to the network, to be mined and included in a block. It has inputs and outputs - the inputs are a reference of the form `prev_tx_id[output_idx]`, basically an index into the outputs of some previous transaction. Those previous outputs have to be unspent to be able to be used as a valid input to a new transaction, and the person sending this transaction has to have a cryptographic signature and public key that meets the requirements that the output is locked with (normally they are locked to the hash of a public key - that hash is the main part of what we call a "Bitcoin address"). The outputs also have a value associated with them (similar to the denomination of a bank note - for example, some output can have the value of 0.123 BTC).