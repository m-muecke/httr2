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
#> last-modified: Fri, 02 Oct 2026 21:20:06 GMT
#> access-control-allow-origin: *
#> etag: W/"6ac02006-4c24"
#> expires: Sat, 03 Oct 2026 08:55:00 GMT
#> cache-control: max-age=600
#> content-encoding: gzip
#> x-proxy-cache: MISS
#> x-github-request-id: 1234:14D60D:14C008E:166F7A3:6AC0C08C
#> x-github-edge-region: iad
#> accept-ranges: bytes
#> date: Sat, 03 Oct 2026 08:59:32 GMT
#> via: 1.1 varnish
#> age: 17
#> x-served-by: cache-iad-kiad7000162-IAD
#> x-cache: HIT
#> x-cache-hits: 4
#> x-timer: S1791017973.563707,VS0,VE0
#> vary: Accept-Encoding
#> x-fastly-request-id: 348606501665a4366efcdcd1415a6d20e1f10c7f
#> content-length: 4860
resp |> resp_headers("x-")
#> <httr2_headers>
#> x-proxy-cache: MISS
#> x-github-request-id: 1234:14D60D:14C008E:166F7A3:6AC0C08C
#> x-github-edge-region: iad
#> x-served-by: cache-iad-kiad7000162-IAD
#> x-cache: HIT
#> x-cache-hits: 4
#> x-timer: S1791017973.563707,VS0,VE0
#> x-fastly-request-id: 348606501665a4366efcdcd1415a6d20e1f10c7f

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
