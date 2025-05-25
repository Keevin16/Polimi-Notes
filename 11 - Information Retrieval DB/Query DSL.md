The communication is done with Elasticsearch through request to REST endpoints.
***
Important differences:
- **Post** doesn't require the ID of the resource, consequently if it's omitted, Elasticsearch takes care of creating and assigning IDs to document.
``` json
POST /index_name/_doc
```
- **PUT** requires the ID of the resource
``` json
PUT /index_name/_doc/document_id
```

### Create a Index
``` json
PUT /my_index
{
	"settings": {
	"number_of_replicas": 3,
	"number_of_shards": 3
	}
}
```
Elasticsearch will provide some metadata describing whether the index was successfully created or not. 

#### Explicit Mapping 
It's possible to define the **explicit mapping** during the creation of the index.
``` json
PUT /my_index
{
	"mappings": {
		"properties":{
			"age": {"type": "integer"},
			"email": {"type": "keyword"},
			"name": {"type": "text"}
		}
	}
}
```
In any case is possible to **add fields** to an index!
``` json
PUT /my_index/_mapping
{
	"properties": {
	"surname": {"type": "text"},
	"index": "false"
	}
}
```
Important notes during the development:
- **Update** the mapping of a field could **invalidate the data**! To avoid problems is necessary to **create** a new index and **reindex** the data.
- Instead of renaming a field, that could lead to an invalidation, it's better to **add a new alias** to that field

### Visualize a mapping
``` json
GET /my_index/_mapping

GET /my_index/_mapping/field/my_field
```

### Types (of the Fields)

| **Type**    | **Description**                                                                    |
| ----------- | ---------------------------------------------------------------------------------- |
| `binary`    | Binary value encoded as a **Base64 string**.                                       |
| `boolean`   | A **true or false** value.                                                         |
| `keyword`   | For structured content like **IDs, emails, tags** — **not analyzed**.              |
| `long`      | **Signed 64-bit integer** (e.g., `-9223372036854775808` to `9223372036854775807`). |
| `double`    | **64-bit double-precision floating-point**, must be **finite** (no NaN/Inf).       |
| `date`      | A **string-formatted date**, internally stored in **UTC** (e.g., ISO 8601).        |
| `object`    | A standard **JSON object** (e.g., `{"name": "ke", "age": 23}`).                    |
| `text`      | For **full-text search**, this type is **analyzed** using tokenizers.              |
| `geo_point` | A **latitude/longitude pair** (e.g., `{ "lat": 45.0, "lon": 7.0 }`).               |

### Analyzers (of the Text)

| **Analyzer** | **Description**                                                                                                       | **Lowercase?** | **Stop Words Removal?** |
| ------------ | --------------------------------------------------------------------------------------------------------------------- | -------------- | ----------------------- |
| `standard`   | Default analyzer. Uses **Unicode Text Segmentation (UTS)** to split on word boundaries. Removes most **punctuation**. | ✅ Yes          | ✅ Yes                   |
| `simple`     | Splits text on **non-letter characters**.                                                                             | ✅ Yes          | ❌ No                    |
| `whitespace` | Splits text on **whitespace only**. Does **not** remove punctuation.                                                  | ❌ No           | ❌ No                    |
| `stop`       | Like `simple`, but also removes **stop words**.                                                                       | ✅ Yes          | ✅ Yes                   |
| `pattern`    | Splits text using a **custom regex pattern**.                                                                         | ✅ Optional     | ✅ Optional              |
| `language`   | **Language-specific analyzers** (e.g., `english`, `french`). Include **stemming**.                                    | ✅ Yes          | ✅ Yes                   |
``` json
POST _analyze
{
	"analyzer": "standard",
	"text": "I really like tables"
}
```
https://webeep.polimi.it/pluginfile.php/1259265/mod_resource/content/4/E05%20-%20Elasticsearch-2.pdf