# dropIndex()

This method drops the index and its corresponding index file in the collection.

```javascript
new milvusClient(MILUVS_ADDRESS).indexManager.dropIndex(DropIndexReq);
```

### DropIndexReq

| Parameters      | Description                                                                            | Type   |
| --------------- | -------------------------------------------------------------------------------------- | ------ |
| collection_name | Collection name                                                                        | String |
| field_name      | Field name                                                                             | String |
| index_name?     | Index name                                                                             | String |
| timeout?        | This parameter is used to specify the length of time, in milliseconds, that the RPC (Remote Procedure Call) is allowed to run. If no value is provided, the default is undefined. | Number |

## Example

```javascript
import { MilvusClient } from "@zilliz/milvus2-sdk-node";

new milvusClient(MILUVS_ADDRESS).indexManager.dropIndex({
  collection_name: "my_collection",
});
```

### Response

```javascript
// dropIndex returns
```