webi
====

`webi` is an alternate specification of python web applications interface to web servers.

It builds upon WSGI, PEP 444, Rack, PSGI/Plack, ring and other similar specifications.

## Interface

A `webi` application can be implemented by any python callable, with `environment` argument, which returns a tuple of `status`, `headers` and `body` as a response.

```python
def application(environment):
  status = 200
  headers = {'Content-Type': 'text/plain'}
  body = [environment['REQUEST_METHOD']]
  return status, headers, body
```
### environment

`environment` must be dictionary of CGI-like headers such as `REQUEST_METHOD`, `SCRIPT_NAME`, `PATH_INFO`, `QUERY_STRING`, `SERVER_NAME`, `SERVER_PORT`, `HTTP_ Variables` etc. In addition, environment must also contain `webi` specific headers prefixed with `webi.`.

### response

#### status
Is one of the http status codes, such as 200, 404, 500, 303 etc.

#### headers
Is a dictionary, with keys and values as string, except for multiple header values, where the value is a list of strings.

#### body
Is an iterable which yields string values.
