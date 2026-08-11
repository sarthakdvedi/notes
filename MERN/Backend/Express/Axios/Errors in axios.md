jab error ata hai, axios ek err object deta h

## `err` object -
1. err.message
2. err.config
3. err.request
4. err.response

### `response` object -
1. status
2. headers
3. data  - `it contains jo backend se data send kia hoga as it is`


## errorHandler middleware -
- it sends a res for errors
- vo res, err.response.data m pada hoga