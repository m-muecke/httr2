# Extract headers from a response

- `resp_headers()` retrieves a list of all headers.

- `resp_header()` retrieves a single header.

- `resp_header_exists()` checks if a header is present.

## Usage

``` r
resp_headers(resp, filter = NULL)

resp_header(resp, header, default = NULL)

resp_header_exists(resp, header)
```

## Arguments

- resp:

  A httr2 [response](https://httr2.r-lib.org/dev/reference/response.md)
  object, created by
  [`req_perform()`](https://httr2.r-lib.org/dev/reference/req_perform.md).

- filter:

  A regular expression used to filter the header names. `NULL`, the
  default, returns all headers.

- header:

  Header name (case insensitive)

- default:

  Default value to use if header doesn't exist.

## Value

- `resp_headers()` returns a list.

- `resp_header()` returns a string if the header exists and `NULL`
  otherwise.

- `resp_header_exists()` returns `TRUE` or `FALSE`.

## Examples

``` r
resp <- request("https://httr2.r-lib.org") |> req_perform()
resp |> resp_headers()
#> <httr2_headers>
#> server: GitHub.com
#> content-type: text/html; charset=utf-8
#> last-modified: Mon, 05 Oct 2026 21:25:26 GMT
#> access-control-allow-origin: *
#> etag: W/"6ac415c6-4c24"
#> expires: Mon, 05 Oct 2026 21:37:45 GMT
#> cache-control: max-age=600
#> content-encoding: gzip
#> x-proxy-cache: MISS
#> x-github-request-id: 52DE:42AF3:6BDC5:7A135:6AC4164E
#> x-github-edge-region: westus3
#> accept-ranges: bytes
#> date: Mon, 05 Oct 2026 21:27:58 GMT
#> via: 1.1 varnish
#> age: 13
#> x-served-by: cache-bur-kbur8200072-BUR
#> x-cache: HIT
#> x-cache-hits: 4
#> x-timer: S1791235679.707640,VS0,VE0
#> vary: Accept-Encoding
#> x-fastly-request-id: e56fbc9b19bd2e1f31f12734a5593209eb063047
#> content-length: 4860
resp |> resp_headers("x-")
#> <httr2_headers>
#> x-proxy-cache: MISS
#> x-github-request-id: 52DE:42AF3:6BDC5:7A135:6AC4164E
#> x-github-edge-region: westus3
#> x-served-by: cache-bur-kbur8200072-BUR
#> x-cache: HIT
#> x-cache-hits: 4
#> x-timer: S1791235679.707640,VS0,VE0
#> x-fastly-request-id: e56fbc9b19bd2e1f31f12734a5593209eb063047

resp |> resp_header_exists("server")
#> [1] TRUE
resp |> resp_header("server")
#> [1] "GitHub.com"
# Headers are case insensitive
resp |> resp_header("SERVER")
#> [1] "GitHub.com"

# Returns NULL if header doesn't exist
resp |> resp_header("this-header-doesnt-exist")
#> NULL
```
