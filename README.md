# securl

`securl` is a (very simple) command which enables you to download (via `curl`) a file with the added benefit of verifying its SHA-256 hash—the expected SHA-256 hash must be embedded in the URL.

This enables the ability to create a hyperlink to any Internet resource (for example, executable code) with the cryptographic guarantee that the file downloaded contains the exact contents it was originally intended to contain when the hyperlink was created.

Apart from that, `securl` simply forwards itself to `curl`, so takes all of the same options `curl` does.

For example,

    $ securl -s https://example.com#3587cb776ce0e4e8237f215800b7dffba0f25865cb84550e87ea8bbac838c423

The above command will:

- Download `https://example.com#3587cb776ce0e4e8237f215800b7dffba0f25865cb84550e87ea8bbac838c423` using curl
- Calculate the SHA-256 hash of the downloaded file (`actual_hash`)
- Verify that the `actual_hash` was in the original URL

If the hash does not match, it will refuse to output the file, and will print an error:

    $ securl -s https://example.com#3587cb776ce0e4e8237f215800b7dffba0f25865cb84550e87ea8bba00000000
    securl: SHA256 didn't match any hash in the URL
    securl: actual_hash 3587cb776ce0e4e8237f215800b7dffba0f25865cb84550e87ea8bbac838c423
    securl: url: https://example.com#3587cb776ce0e4e8237f215800b7dffba0f25865cb84550e87ea8bba00000000
