# python-function

This is a basic Python Azure function that takes the file from the input and copies it to the output.


```
import logging

import azure.functions as func


def main(myblob: func.InputStream, outputBlob: func.Out[func.InputStream]):
    logging.info(f"Python blob trigger function processed blob \n"
                 f"Name: {myblob.name}\n"
                 f"Blob Size: {myblob.length} bytes")
    outputBlob.set(myblob)
```

The source and destination are defined in function.json

```
{
  "scriptFile": "__init__.py",
  "bindings": [
    {
      "name": "myblob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "samples-workitems/{name}",
      "connection": "jjblobtriggerfuncstore_STORAGE"
    },
    {
      "name": "outputBlob",
      "type": "blob",
      "direction": "out",
      "path": "output/{name}",
      "connection": "jjblobtriggerfuncstore_STORAGE"
    }
  ]
}
```

The connection **jjblobtriggerfuncstore_STORAGE** needs to be set in the configuration section of the Azure function.

![alt text](azure-function-configuration.png "Function configuration")
