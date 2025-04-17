>BSON (Binary JSON) is a binary encoded serialization of the JSON-like document.
>It's optimized for **storage, parsing, and transport**.

- **Binary format** of JSON  
	Easier to **parse, transmit, and store** efficiently than plain-text JSON.

- **Stores zero or more key-value pairs**  
    Like JSON objects (`{ "name": "Alice", "age": 25 }`)

- **Each element = field name + type + value**  
    Enables fast type detection during parsing.

- **Length prefixing**  
    BSON includes the size of objects and arrays, enabling **fast skipping** and **efficient scans**.

Note:
- It's possible to have more that one Json inside one BSON


#MongoDB