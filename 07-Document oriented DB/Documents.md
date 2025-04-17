>It consist of **key-value pairs** which are the basic unit of data in MongoDB.

Note:
- These [[Documents]] are Json-like. 
- I cannot put a [[Documents]] outside of **one and only one** [[Collections]]
- They must have an _**_id**, which is the **Primary key**
- It's possible to have embedded **sub-document** which don't have an _**_id
- Max size of one [[Documents]] is of 16 MB
	- possible to handle larger document with GridFS

example of a document:
```json
{
"business_id": "rncjoVoEFUJGCUoC1JgnUA",
"full_address": "8466 W Peoria Ave\nSte 6\nPeoria, AZ 85345",
"open": true,
"categories": ["Accountants", "Professional Services", "Tax Services",],
"city": "Peoria",
"review_count": 3,
"name": "Peoria Income Tax Service",
"neighborhoods": [],
"longitude": -112.241596,
"state": "AZ",
"stars": 5.0,
"latitude": 33.581867000000003,
"type": "business“
}
```
Each row is called **Field**


Remark:
>The fact that's write in JSON increases the **Readability** but makes it take up more **space** and **time** to compile, instead the [[BSON]] makes the opposite.



#MongoDB