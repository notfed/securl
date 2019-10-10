# securl

`securl` is a (very simple) command which enables you to download (via `curl`) a file with the added benefit of verifying its cryptographic hash—the expected hash must be embedded in the URL.

This enables the ability to create a hyperlink to any Internet resource (for example, executable code) with the cryptographic guarantee that the file downloaded contains the exact contents it was originally intended to contain when the hyperlink was created.

Apart from that, `securl` simply forwards itself to `curl`, so takes all of the same options `curl` does.

For example,

    $ securl https://example.com/code.sh#n3GQYoa6bQxYBpuMZegudWp9rnN8vUeWH

The above command will:

- Download `https://example.com/code.sh#n3GQYoa6bQxYBpuMZegudWp9rnN8vUeWH
- Calculate the SHA-256 hash of the downloaded file (`actual_hash`)
- Verify that the `actual_hash` was in the original URL

If the hash does not match, it will refuse to output the file, and will print an error:

    $ securl -s https://example.com/code.sh#n3GQYoa6bQxYBpuMZegudWp9rnN8vUeWH
    securl: error: actual hash (2iMUCASH5G1zxdnoHbPuz2EFbfWWJio3z) was not found in the URL (https://example.com/code.sh#n3GQYoa6bQxYBpuMZegudWp9rnN8vUeW)
