# Why the need to fork Metamask?

Qtum differs fundamentally from Ethereum in it's UTXOs Accounting because it is a fork of Bitcoin.

In order to sign Qtum transactions we need access to sign arbitrary data. Metamask is designed in such a way that this is impossible in modern versions - as this is very dangerous. Giving unrestricted access to your private key to DAPPs is very dangerous and can easily lead to stolen funds without your knowledge.

This used to be possible with legacy `eth_sign` functionality, but modern Metamask versions have completely disabled access to unrestricted arbitrary data signing which makes signing Qtum transactions with Metamask impossible.

Modern Metamask `eth_sign` behaves indentically to `personal_sign` which prefixes data which makes signing arbitrary data impossible.

Another technical issue is how accounts are generated from public keys.
* Ethereum computes [KECCAK-256](https://en.wikipedia.org/wiki/SHA-3) from an uncompressed public key
* Qtum/Bitcoin computes [RIPEMD-160](https://en.wikipedia.org/wiki/RIPEMD) from a compressed public key
