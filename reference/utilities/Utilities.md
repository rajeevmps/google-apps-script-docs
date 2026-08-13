# Utilities

This service provides utilities for string encoding/decoding, date formatting, JSON manipulation, and other miscellaneous tasks.

This service provides utilities for string encoding/decoding, date formatting, JSON manipulation, and other miscellaneous tasks.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------|
| base64Decode(encoded) | Byte[] | Decodes a base-64 encoded string into a UTF-8 byte array |
| base64Decode(encoded, charset) | Byte[] | Decodes a base-64 encoded string into a byte array in a specific character set |
| base64DecodeWebSafe(encoded) | Byte[] | Decodes a base-64 web-safe encoded string into a UTF-8 byte array |
| base64DecodeWebSafe(encoded, charset) | Byte[] | Decodes a base-64 web-safe encoded string into a byte array in a specific character set |
| base64Encode(data) | String | Generates a base-64 encoded string from the given byte array |
| base64Encode(data) | String | Generates a base-64 encoded string from the given string |
| base64Encode(data, charset) | String | Generates a base-64 encoded string from the given string in a specific character set |
| base64EncodeWebSafe(data) | String | Generates a base-64 web-safe encoded string from the given byte array |
| base64EncodeWebSafe(data) | String | Generates a base-64 web-safe encoded string from the given string |
| base64EncodeWebSafe(data, charset) | String | Generates a base-64 web-safe encoded string from the given string in a specific character set |
| computeDigest(algorithm, value) | Byte[] | Compute a digest using the specified algorithm on the specified Byte[] value |
| computeDigest(algorithm, value) | Byte[] | Compute a digest using the specified algorithm on the specified String value |
| computeDigest(algorithm, value, charset) | Byte[] | Compute a digest using the specified algorithm on the specified String value with the given character set |
| computeHmacSha256Signature(value, key) | Byte[] | Signs the provided value using HMAC-SHA256 with the given key |
| computeHmacSha256Signature(value, key) | Byte[] | Signs the provided value using HMAC-SHA256 with the given key (String overload) |
| computeHmacSha256Signature(value, key, charset) | Byte[] | Signs the provided value using HMAC-SHA256 with the given key and character set |
| computeHmacSignature(algorithm, value, key) | Byte[] | Compute a message authentication code using the specified algorithm on the specified key and value |
| computeHmacSignature(algorithm, value, key) | Byte[] | Compute a message authentication code (String overload) |
| computeHmacSignature(algorithm, value, key, charset) | Byte[] | Compute a message authentication code with character set specification |
| computeRsaSha1Signature(value, key) | Byte[] | Signs the provided value using RSA-SHA1 with the given key |
| computeRsaSha1Signature(value, key, charset) | Byte[] | Signs the provided value using RSA-SHA1 with the given key and charset |
| computeRsaSha256Signature(value, key) | Byte[] | Signs the provided value using RSA-SHA256 with the given key |
| computeRsaSha256Signature(value, key, charset) | Byte[] | Signs the provided value using RSA-SHA256 with the given key |
| computeRsaSignature(algorithm, value, key) | Byte[] | Signs the provided value using the specified RSA algorithm with the given key |
| computeRsaSignature(algorithm, value, key, charset) | Byte[] | Signs the provided value using the specified RSA algorithm with the given key and charset |
| formatDate(date, timeZone, format) | String | Formats date according to specification described in Java SE SimpleDateFormat class |
| formatString(template, args) | String | Performs sprintf-like string formatting using '%'-style format strings |
| getUuid() | String | Get a UUID as a string |
| gzip(blob) | Blob | gzip-compresses the provided Blob data and returns it in a new Blob object |
| gzip(blob, name) | Blob | gzip-compresses the provided Blob data and returns it in a new Blob object |
| newBlob(data) | Blob | Create a new Blob object from a byte array |
| newBlob(data, contentType) | Blob | Create a new Blob object from a byte array and content type |
| newBlob(data, contentType, name) | Blob | Create a new Blob object from a byte array, content type, and name |
| newBlob(data) | Blob | Create a new Blob object from a string |
| newBlob(data, contentType) | Blob | Create a new Blob object from a string and content type |
| newBlob(data, contentType, name) | Blob | Create a new Blob object from a string, content type, and name |
| parseCsv(csv) | String[][] | Returns a tabular 2D array representation of a CSV string |
| parseCsv(csv, delimiter) | String[][] | Returns a tabular 2D array representation of a CSV string using a custom delimiter |
| parseDate(date, timeZone, format) | Date | Parses the provided string date according to the specification described in Java SE SimpleDateFormat |
| sleep(milliseconds) | void | Sleeps for specified number of milliseconds |
| ungzip(blob) | Blob | Uncompresses a Blob object and returns a Blob containing the uncompressed data |
| unzip(blob) | Blob[] | Takes a Blob representing a zip file and returns its component files |
| zip(blobs) | Blob | Creates a new Blob object that is a zip file containing the data from the Blobs passed in |
| zip(blobs, name) | Blob | Creates a new Blob object that is a zip file containing the data from the Blobs passed in |
| jsonParse(jsonString) *(deprecated)* | Object | Return an object corresponding to the JSON string passed in |
| jsonStringify(obj) *(deprecated)* | String | Return a JSON string of the object passed in |

### base64Decode(encoded: String) → Byte[]

Decodes a base-64 encoded string into a UTF-8 byte array.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| encoded | String | An array of bytes of data to decode |

**Return** — Byte[]: The raw data represented by the base-64 encoded argument as a byte array.

```javascript
// This is the base64 encoded form of "Google グループ"
const base64data = 'R29vZ2xlIOOCsOODq+ODvOODlw==';

// This logs:
//     [71, 111, 111, 103, 108, 101, 32, -29, -126, -80,
//      -29, -125, -85, -29, -125, -68, -29, -125, -105]
const decoded = Utilities.base64Decode(base64data);
Logger.log(decoded);

// If you want a String instead of a byte array:
// This logs the original "Google グループ"
Logger.log(Utilities.newBlob(decoded).getDataAsString());
```

### base64Decode(encoded: String, charset: Charset) → Byte[]

Decodes a base-64 encoded string into a byte array in a specific character set.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| encoded | String | The string of data to decode |
| charset | Charset | A Charset specifying the charset of the input |

**Return** — Byte[]: The raw data represented by the base-64 encoded argument as a byte array.

```javascript
// This is the base64 encoded form of "Google グループ"
const base64data = 'R29vZ2xlIOOCsOODq+ODvOODlw==';

const decoded = Utilities.base64Decode(base64data, Utilities.Charset.UTF_8);

// This logs:
//     [71, 111, 111, 103, 108, 101, 32, -29, -126, -80,
//      -29, -125, -85, -29, -125, -68, -29, -125, -105]
Logger.log(decoded);

// If you want a String instead of a byte array:
// This logs the original "Google グループ"
Logger.log(Utilities.newBlob(decoded).getDataAsString());
```

### base64DecodeWebSafe(encoded: String) → Byte[]

Decodes a base-64 web-safe encoded string into a UTF-8 byte array.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| encoded | String | An array of bytes of web-safe data to decode |

**Return** — Byte[]: The raw data represented by the base-64 web-safe encoded argument as a byte array.

```javascript
// This is the base64 web-safe encoded form of "Google グループ"
const base64data = 'R29vZ2xlIOOCsOODq-ODvOODlw==';

const decoded = Utilities.base64DecodeWebSafe(base64data);

// This logs:
//     [71, 111, 111, 103, 108, 101, 32, -29, -126, -80,
//      -29, -125, -85, -29, -125, -68, -29, -125, -105]
Logger.log(decoded);

// If you want a String instead of a byte array:
// This logs the original "Google グループ"
Logger.log(Utilities.newBlob(decoded).getDataAsString());
```

### base64DecodeWebSafe(encoded: String, charset: Charset) → Byte[]

Decodes a base-64 web-safe encoded string into a byte array in a specific character set.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| encoded | String | The string of web-safe data to decode |
| charset | Charset | A Charset specifying the charset of the input |

**Return** — Byte[]: The raw data represented by the base-64 web-safe encoded argument as a byte array.

```javascript
// This is the base64 web-safe encoded form of "Google グループ"
const base64data = 'R29vZ2xlIOOCsOODq-ODvOODlw==';

const decoded = Utilities.base64DecodeWebSafe(
    base64data,
    Utilities.Charset.UTF_8,
);

// This logs:
//     [71, 111, 111, 103, 108, 101, 32, -29, -126, -80,
//      -29, -125, -85, -29, -125, -68, -29, -125, -105]
Logger.log(decoded);

// If you want a String instead of a byte array:
// This logs the original "Google グループ"
Logger.log(Utilities.newBlob(decoded).getDataAsString());
```

### base64Encode(data: Byte[]) → String

Generates a base-64 encoded string from the given byte array. Base 64 is a common encoding accepted by a variety of tools that cannot accept binary data. Base 64 is commonly used in internet protocols such as email, HTTP, or in XML documents.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | Byte[] | A byte[] of data to encode |

**Return** — String: The base-64 encoded representation of the passed in data.

```javascript
// Instantiates a blob here for clarity
const blob = Utilities.newBlob('A string here');

// Writes 'QSBzdHJpbmcgaGVyZQ==' to the log.
const encoded = Utilities.base64Encode(blob.getBytes());
Logger.log(encoded);
```

### base64Encode(data: String) → String

Generates a base-64 encoded string from the given string. Base 64 is a common encoding accepted by a variety of tools that cannot accept binary data. Base 64 is commonly used in internet protocols such as email, HTTP, or in XML documents.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string to encode |

**Return** — String: The base-64 encoded representation of the input string.

```javascript
// Writes 'QSBzdHJpbmcgaGVyZQ==' to the log.
const encoded = Utilities.base64Encode('A string here');
Logger.log(encoded);
```

### base64Encode(data: String, charset: Charset) → String

Generates a base-64 encoded string from the given string in a specific character set. A Charset is a way of encoding characters such that they can be encoded. These are typically done in a binary format, which can generally be incompatible with certain data transmission protocols. To make the data compatible, they are generally encoded into base 64, which is a common encoding accepted by a variety of tools that cannot accept binary data. Base 64 is commonly used in internet protocols such as email, HTTP, or in XML documents.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string of data to encode |
| charset | Charset | A Charset specifying the charset of the input |

**Return** — String: The base-64 encoded representation of the input string with the given Charset.

```javascript
// "Google Groups" in Katakana (Japanese)
const input = 'Google グループ';

// Writes "R29vZ2xlIOOCsOODq+ODvOODlw==" to the log
const encoded = Utilities.base64Encode(input, Utilities.Charset.UTF_8);
Logger.log(encoded);
```

### base64EncodeWebSafe(data: Byte[]) → String

Generates a base-64 web-safe encoded string from the given byte array. Base 64 is a common encoding accepted by a variety of tools that cannot accept binary data. Base 64 web-safe is commonly used in internet protocols such as email, HTTP, or in XML documents.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | Byte[] | An array of bytes of data to encode |

**Return** — String: The base-64 web-safe encoded representation of the passed in data.

```javascript
// Instantiates a blob here for clarity
const blob = Utilities.newBlob('A string here');

// Writes 'QSBzdHJpbmcgaGVyZQ==' to the log.
const encoded = Utilities.base64EncodeWebSafe(blob.getBytes());
Logger.log(encoded);
```

### base64EncodeWebSafe(data: String) → String

Generates a base-64 web-safe encoded string from the given string. Base 64 is a common encoding accepted by a variety of tools that cannot accept binary data. Base 64 web-safe is commonly used in internet protocols such as email, HTTP, or in XML documents.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string to encode |

**Return** — String: The base-64 web-safe encoded representation of the input string.

```javascript
// Writes 'QSBzdHJpbmcgaGVyZQ==' to the log.
const encoded = Utilities.base64EncodeWebSafe('A string here');
Logger.log(encoded);
```

### base64EncodeWebSafe(data: String, charset: Charset) → String

Generates a base-64 web-safe encoded string from the given string in a specific character set. A Charset is a way of encoding characters such that they can be encoded. These are typically done in a binary format, which can generally be incompatible with certain data transmission protocols. To make the data compatible, they are generally encoded into base 64, which is a common encoding accepted by a variety of tools that cannot accept binary data. Base 64 web-safe is commonly used in internet protocols such as email, HTTP, or in XML documents.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string of data to encode |
| charset | Charset | A Charset specifying the charset of the input |

**Return** — String: The base-64 web-safe encoded representation of the input string with the given Charset.

```javascript
// "Google Groups" in Katakana (Japanese)
const input = 'Google グループ';

// Writes "R29vZ2xlIOOCsOODq-ODvOODlw==" to the log
const encoded = Utilities.base64EncodeWebSafe(input, Utilities.Charset.UTF_8);
Logger.log(encoded);
```

### computeDigest(algorithm: DigestAlgorithm, value: Byte[]) → Byte[]

Compute a digest using the specified algorithm on the specified Byte[] value.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | DigestAlgorithm | A DigestAlgorithm to use |
| value | Byte[] | An input string value to compute a digest for |

**Return** — Byte[]: A byte[] representing the output digest.

```javascript
const input = Utilities.base64Decode(
    'aW5wdXQgdG8gaGFzaA0K');  // == base64encode("input to hash")
const digest = Utilities.computeDigest(Utilities.DigestAlgorithm.MD5, input);
Logger.log(digest);
```

### computeDigest(algorithm: DigestAlgorithm, value: String) → Byte[]

Compute a digest using the specified algorithm on the specified String value.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | DigestAlgorithm | A DigestAlgorithm to use |
| value | String | An input string value to compute a digest for |

**Return** — Byte[]: A byte[] representing the output digest.

```javascript
const digest = Utilities.computeDigest(
    Utilities.DigestAlgorithm.MD5,
    'input to hash',
);
Logger.log(digest);
```

### computeDigest(algorithm: DigestAlgorithm, value: String, charset: Charset) → Byte[]

Compute a digest using the specified algorithm on the specified String value with the given character set.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | DigestAlgorithm | A DigestAlgorithm to use |
| value | String | An input string value to compute a digest for |
| charset | Charset | A Charset representing the input character set |

**Return** — Byte[]: A byte[] representing the output digest.

```javascript
const digest = Utilities.computeDigest(
    Utilities.DigestAlgorithm.MD5,
    'input to hash',
    Utilities.Charset.US_ASCII,
);
Logger.log(digest);
```

### computeHmacSha256Signature(value: Byte[], key: Byte[]) → Byte[]

Signs the provided value using HMAC-SHA256 with the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | Byte[] | The input value to generate a hash for |
| key | Byte[] | A key to use to generate the hash with |

**Return** — Byte[]: A byte[] representing the output signature.

```javascript
// This writes an array of bytes to the log.
const input = Utilities.base64Decode(
    'aW5wdXQgdG8gaGFzaA0K');                 // == base64encode("input to hash")
const key = Utilities.base64Decode('a2V5');  // == base64encode("key")
const signature = Utilities.computeHmacSha256Signature(input, key);
Logger.log(signature);
```

### computeHmacSha256Signature(value: String, key: String) → Byte[]

Signs the provided value using HMAC-SHA256 with the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | String | The input value to generate a hash for |
| key | String | A key to use to generate the hash with |

**Return** — Byte[]: A byte[] representing the output signature.

```javascript
// This writes an array of bytes to the log.
const signature = Utilities.computeHmacSha256Signature(
    'this is my input',
    'my key - use a stronger one',
);
Logger.log(signature);
```

### computeHmacSha256Signature(value: String, key: String, charset: Charset) → Byte[]

Signs the provided value using HMAC-SHA256 with the given key and character set.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | String | The input value to generate a hash for |
| key | String | A key to use to generate the hash with |
| charset | Charset | A Charset representing the input character set |

**Return** — Byte[]: A byte[] representing the output signature.

```javascript
// This writes an array of bytes to the log.
const signature = Utilities.computeHmacSha256Signature(
    'this is my input',
    'my key - use a stronger one',
    Utilities.Charset.US_ASCII,
);
Logger.log(signature);
```

### computeHmacSignature(algorithm: MacAlgorithm, value: Byte[], key: Byte[]) → Byte[]

Compute a message authentication code using the specified algorithm on the specified key and value.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | MacAlgorithm | A MacAlgorithm algorithm to use to hash the input value |
| value | Byte[] | The input value to generate a hash for |
| key | Byte[] | A key to use to generate the hash with |

**Return** — Byte[]: A byte[] representing the output signature.

```javascript
// This writes an array of bytes to the log.
const input = Utilities.base64Decode(
    'aW5wdXQgdG8gaGFzaA0K');                 // == base64encode("input to hash")
const key = Utilities.base64Decode('a2V5');  // == base64encode("key")
const signature = Utilities.computeHmacSignature(
    Utilities.MacAlgorithm.HMAC_MD5,
    input,
    key,
);
Logger.log(signature);
```

### computeHmacSignature(algorithm: MacAlgorithm, value: String, key: String) → Byte[]

Compute a message authentication code using the specified algorithm on the specified key and value.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | MacAlgorithm | A MacAlgorithm algorithm to use to hash the input value |
| value | String | The input value to generate a hash for |
| key | String | A key to use to generate the hash with |

**Return** — Byte[]: A byte[] representing the output signature.

```javascript
// This writes an array of bytes to the log.
const signature = Utilities.computeHmacSignature(
    Utilities.MacAlgorithm.HMAC_MD5,
    'input to hash',
    'key',
);
Logger.log(signature);
```

### computeHmacSignature(algorithm: MacAlgorithm, value: String, key: String, charset: Charset) → Byte[]

Compute a message authentication code using the specified algorithm on the specified key and value.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | MacAlgorithm | A MacAlgorithm algorithm to use to hash the input value |
| value | String | The input value to generate a hash for |
| key | String | A key to use to generate the hash with |
| charset | Charset | A Charset representing the input character set |

**Return** — Byte[]: A byte[] representing the output signature.

### computeRsaSha1Signature(value: String, key: String) → Byte[]

Signs the provided value using RSA-SHA1 with the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | String | The value to sign |
| key | String | The key to sign with |

**Return** — Byte[]: A byte[] representing the output signature.

### computeRsaSha1Signature(value: String, key: String, charset: Charset) → Byte[]

Signs the provided value using RSA-SHA1 with the given key and charset.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | String | The value to sign |
| key | String | The key to sign with |
| charset | Charset | A Charset representing the input character set |

**Return** — Byte[]: A byte[] representing the output signature.

### computeRsaSha256Signature(value: String, key: String) → Byte[]

Signs the provided value using RSA-SHA256 with the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | String | The value to sign |
| key | String | The key to sign with |

**Return** — Byte[]: A byte[] representing the output signature.

### computeRsaSha256Signature(value: String, key: String, charset: Charset) → Byte[]

Signs the provided value using RSA-SHA256 with the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| value | String | The value to sign |
| key | String | The key to sign with |
| charset | Charset | A Charset representing the input character set |

**Return** — Byte[]: A byte[] representing the output signature.

### computeRsaSignature(algorithm: RsaAlgorithm, value: String, key: String) → Byte[]

Signs the provided value using the specified RSA algorithm with the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | RsaAlgorithm | The RSA algorithm to use |
| value | String | The value to sign |
| key | String | The key to sign with |

**Return** — Byte[]: A byte[] representing the output signature.

### computeRsaSignature(algorithm: RsaAlgorithm, value: String, key: String, charset: Charset) → Byte[]

Signs the provided value using the specified RSA algorithm with the given key and charset.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| algorithm | RsaAlgorithm | The RSA algorithm to use |
| value | String | The value to sign |
| key | String | The key to sign with |
| charset | Charset | A Charset representing the input character set |

**Return** — Byte[]: A byte[] representing the output signature.

### formatDate(date: Date, timeZone: String, format: String) → String

Formats date according to specification described in Java SE SimpleDateFormat class.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| date | Date | The date to format |
| timeZone | String | The timezone to format the date in |
| format | String | The format string to use |

**Return** — String: The formatted date string.

### formatString(template: String, args: Object...) → String

Performs sprintf-like string formatting using '%'-style format strings.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| template | String | The format string template |
| args | Object... | Variable arguments to substitute into the template |

**Return** — String: The formatted string.

### getUuid() → String

Get a UUID as a string (equivalent to using the java.util.UUID.randomUUID() method).

**Parameters** — None

**Return** — String: A UUID as a string.

### gzip(blob: BlobSource) → Blob

gzip-compresses the provided Blob data and returns it in a new Blob object.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| blob | BlobSource | The Blob data to compress |

**Return** — Blob: A new Blob containing the gzip-compressed data.

### gzip(blob: BlobSource, name: String) → Blob

gzip-compresses the provided Blob data and returns it in a new Blob object.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| blob | BlobSource | The Blob data to compress |
| name | String | The name for the resulting Blob |

**Return** — Blob: A new Blob containing the gzip-compressed data.

### newBlob(data: Byte[]) → Blob

Create a new Blob object from a byte array.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | Byte[] | The byte array data |

**Return** — Blob: A new Blob object.

### newBlob(data: Byte[], contentType: String) → Blob

Create a new Blob object from a byte array and content type.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | Byte[] | The byte array data |
| contentType | String | The MIME type content type |

**Return** — Blob: A new Blob object.

### newBlob(data: Byte[], contentType: String, name: String) → Blob

Create a new Blob object from a byte array, content type, and name.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | Byte[] | The byte array data |
| contentType | String | The MIME type content type |
| name | String | The name for the Blob |

**Return** — Blob: A new Blob object.

### newBlob(data: String) → Blob

Create a new Blob object from a string.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string data |

**Return** — Blob: A new Blob object.

### newBlob(data: String, contentType: String) → Blob

Create a new Blob object from a string and content type.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string data |
| contentType | String | The MIME type content type |

**Return** — Blob: A new Blob object.

### newBlob(data: String, contentType: String, name: String) → Blob

Create a new Blob object from a string, content type, and name.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| data | String | The string data |
| contentType | String | The MIME type content type |
| name | String | The name for the Blob |

**Return** — Blob: A new Blob object.

### parseCsv(csv: String) → String[][]

Returns a tabular 2D array representation of a CSV string.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| csv | String | A CSV formatted string |

**Return** — String[][]: A 2D array of strings representing CSV data.

### parseCsv(csv: String, delimiter: Char) → String[][]

Returns a tabular 2D array representation of a CSV string using a custom delimiter.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| csv | String | A CSV formatted string |
| delimiter | Char | The delimiter character to use |

**Return** — String[][]: A 2D array of strings representing CSV data.

### parseDate(date: String, timeZone: String, format: String) → Date

Parses the provided string date according to the specification described in the Java Standard Edition SimpleDateFormat class.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| date | String | The date string to parse |
| timeZone | String | The timezone for parsing |
| format | String | The format string to use |

**Return** — Date: The parsed Date object.

### sleep(milliseconds: Integer) → void

Sleeps for specified number of milliseconds.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| milliseconds | Integer | The number of milliseconds to sleep |

**Return** — void

### ungzip(blob: BlobSource) → Blob

Uncompresses a Blob object and returns a Blob containing the uncompressed data.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| blob | BlobSource | A Blob containing gzip-compressed data |

**Return** — Blob: A new Blob containing the uncompressed data.

### unzip(blob: BlobSource) → Blob[]

Takes a Blob representing a zip file and returns its component files.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| blob | BlobSource | A Blob representing a zip file |

**Return** — Blob[]: An array of Blob objects representing the files in the zip archive.

### zip(blobs: BlobSource) → Blob

Creates a new Blob object that is a zip file containing the data from the Blobs passed in.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| blobs | BlobSource | Blob objects to include in the zip file |

**Return** — Blob: A new Blob representing a zip archive.

### zip(blobs: BlobSource, name: String) → Blob

Creates a new Blob object that is a zip file containing the data from the Blobs passed in.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| blobs | BlobSource | Blob objects to include in the zip file |
| name | String | The name for the resulting zip Blob |

**Return** — Blob: A new Blob representing a zip archive.

## Deprecated Methods

### jsonParse(jsonString: String) → Object

*Deprecated.*

Return an object corresponding to the JSON string passed in.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| jsonString | String | A JSON formatted string |

**Return** — Object: An object parsed from the JSON string.

### jsonStringify(obj: Object) → String

*Deprecated.*

Return a JSON string of the object passed in.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| obj | Object | An object to stringify |

**Return** — String: A JSON representation of the object.

## Properties

None. (This class exposes the enums `Charset`, `DigestAlgorithm`, `MacAlgorithm`, and `RsaAlgorithm` as nested types, documented separately — see Charset.md, DigestAlgorithm.md, MacAlgorithm.md, RsaAlgorithm.md.)
