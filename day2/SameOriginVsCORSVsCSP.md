Two URLs are said to have the same origin if they have the same protocol (HTTP/HTTPS etc), port and host.

## Same Origin Policy
Same origin policy blocks scripts on one origin from accessing or modifying resources on other origins. It prevents DOM access, storage (localStorage, sessionStorage, IndexedDB) access and the reading of cross-origin responses unless explicitly permitted.

## CORS (Cross Origin Resource Sharing)
CORS is a mechanism that allows the server to indicate origins other than itself, from which the browser should allow read access to resources. It relies on a preflight mechanism (for non-simple requests like `POST`, `PUT`, `PATCH`, `DELETE`) in which the browser first sends an `OPTIONS` request that contains the headers and HTTP method of the actual request, to check whether that server allows it or not.

### Response Headers for Access Control Requests
| Header | What it specifies |
| ------ | ----------------- |
|`Access-Control-Allow-Origin`| Origin(s) that are allowed to access the resource. `*` indicates that all origins are allowed. |
|`Access-Control-Expose-Headers`| Header(s) that scripts on the browser can access. |
|`Access-Control-Max-Age`| Maximum duration for which the response of preflight request can be cached. |
|`Access-Control-Allow-Credentials`| Whether the actual request can be made using credentials. |
|`Access-Control-Allow-Methods`| Method(s) allowed in requests for accessing the resource. |
|`Access-Control-Allow-Headers`| Header(s) that can be used while making the actual request (after preflight). |

### Request Headers used in CORS
| Header | What it specifies |
| ------ | ----------------- |
|`Origin`| Origin of the access or preflight request. |
|`Access-Control-Request-Method`| During preflight request, to specify the method of the actual access request. |
|`Access-Control-Request-Headers`| During preflight request, to specify the headers of the actual access request. |