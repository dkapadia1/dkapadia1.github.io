# Simple rust CLI to send SolPPC standard API calls

The SolPPC idea was to make a standard in which vendors could verify payment across Solana and return their microservices. 

This app is based in Rust CLAP, and uses the solana package to create transactions.

To use, download the [source](https://github.com/dkapadia1/SolPPC/tree/776f2cdc81f9968ed58aa8a7c1c994e22a32e228/SolPPC/SolPPC-cli) and build using cargo --build --release, which will make a binary that you can use like curl. 

You also need to set up you're solana CLI config, to be used as a wallet to pay for transactions.

Here is an example usage:

solppc-cli call
http://127.0.0.1:8000/test
--method POST
--data data.json
-H "Content-Type: application/json"
--max-lamports 100000 \

Which will send a maximum of 100000 lamports for the usage of the server hosted on port 8000