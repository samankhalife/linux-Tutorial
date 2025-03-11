# genhash

**genhash** is a command-line utility designed to generate cryptographic hash values for given input data. It functions similarly to other hashing tools like **md5sum** or **sha1sum**, but it may support multiple hash algorithms and configurable options. Typically, **genhash** can be used to compute a hash digest for a file or standard input, which is useful for verifying data integrity and consistency.

## Key Features

- **Multiple Algorithm Support:**  
  Depending on the implementation, **genhash** can support various hash algorithms (e.g., MD5, SHA-1, SHA-256). You may be able to specify which algorithm to use via command-line options.

- **File and Standard Input Processing:**  
  It can compute hash values for files by taking file names as input or by reading data from standard input.

- **Output Formatting:**  
  The output typically consists of the hash digest, which can then be compared against known values for integrity verification.

## Basic Usage

A typical command line usage might be:

```bash
genhash -a sha256 filename.txt
```

- **-a, --algorithm:**  
  Specifies the hash algorithm to use (e.g., md5, sha1, sha256).

- **filename.txt:**  
  The file for which to compute the hash. If no file is provided, **genhash** may read from standard input.

For example, to compute a SHA-256 hash of data provided via a pipe:

```bash
echo "sample data" | genhash -a sha256
```

This command will output the SHA-256 hash for "sample data".

## Example Output

When you run a command like:

```bash
genhash -a md5 example.txt
```

The output might look like:

```
d41d8cd98f00b204e9800998ecf8427e  example.txt
```

This indicates the MD5 hash of **example.txt** along with the file name.

## Use Cases

- **Data Integrity Verification:**  
  Compare computed hash values with known checksums to verify that files have not been corrupted or tampered with.

- **Software Distribution:**  
  Generate hashes for software packages so that users can verify downloads against published checksums.

- **Scripting and Automation:**  
  Integrate **genhash** in scripts to automate integrity checks for backups, file transfers, or system monitoring.

## Conclusion

**genhash** is a versatile tool for generating hash digests from input data, similar to well-known utilities like **md5sum** and **sha256sum**. Its support for multiple algorithms and straightforward usage makes it a useful utility for verifying file integrity and ensuring data consistency.

For more detailed documentation and options, refer to the specific version’s man page or official documentation provided with the utility.

