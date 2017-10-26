# Bson

> **BSON** is a binary format in which zero or more ordered key/value pairs are stored as a single entity. We call this entity a document.

Bson [spec](http://bsonspec.org/spec.html).

### Why Bson when we have JSON?

- efficient in space(in most cases)
- fast to encode and decode
- additional data types such as BinData, Date

Examples from [FAQ](http://bsonspec.org/faq.html):

```bash
The following are some example documents (in JavaScript / Python style syntax) and their corresponding BSON representations.

 {"hello": "world"}

  \x16\x00\x00\x00                   // total document size
  \x02                               // 0x02 = type String
  hello\x00                          // field name
  \x06\x00\x00\x00world\x00          // field value
  \x00                               // 0x00 = type EOO ('end of object')

 {"BSON": ["awesome", 5.05, 1986]}

  \x31\x00\x00\x00
  \x04BSON\x00
  \x26\x00\x00\x00
  \x02\x30\x00\x08\x00\x00\x00awesome\x00
  \x01\x31\x00\x33\x33\x33\x33\x33\x33\x14\x40
  \x10\x32\x00\xc2\x07\x00\x00
  \x00
  \x00
```

