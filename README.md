# Dummy API

Dummy API is an API which behaviour is decided by the request headers and
query parameters. The purpose is to use it for testing and benchmarking API
gateways such as the Varnish API Engine.

## Headers and query parameters

The following request headers and query parameters will make an impact on the response.

### Delay

    header-delay = {int}             Delay in ms to first header byte
    body-delay = {int}               Delay in ms to first body byte

### Cache-control

    max-age = {int}                  Set the response max-age value
    s-maxage = {int}                 Set the response s-maxage value
    must-revalidate                  Set must-revalidate
    public                           Set public
    private                          Set private
    no-store                         Set no-store
    no-cache                         Set no-cache
    no-transform                     Set no-transform

### Misc

    x-parent=value                   Add the X-Parent response header
    x-trace=value                    Add the X-Trace response header
    x-debug=value                    Add the X-Debug response header
    connection=close                 Add connection=close response header
    content-length                   Set the content-length header, otherwise chunked transfer encoding is used
    random-content = {int}           Add random string to the response of given length
    predictable-content = {int}      Add predictable string to the response of given length
    response-status = {int}          Set the response status
    help                             Show help text

## Examples

    GET http://somehost/someurl?max-age=2&content-length&header-delay=1
    
    HTTP/1.1 200 OK
    Cache-control: max-age=2
    Connection: close
    Content-Type: application/json
    Content-length: 106
    Date: Fri, 01 May 2015 19:25:11 GMT
    Server: Dummy API
    
    {
        "content-length": true,
        "header-delay": 1000,
        "host": "somehost",
        "max-age": 2,
        "method": "GET",
        "uri": "/someurl"
    }

## Getting help

    GET http://somehost/?help

## Installation

    yum install golang
    go build dummy-api.go
    chmod +x dummy-api
    ./dummy-api

## Daemon options

    ./dummy-api -help
      -cert-file="": Certificate file.
      -host="127.0.0.1": Listen host.
      -key-file="": Certificate key file.
      -maxheaderbytes=1048576: Max header bytes.
      -port=1337: Listen port.
      -readtimeout=10: Read timeout in seconds.
      -tls=false: Enable TLS.
      -verbose=false: Verbose stdout.
      -writetimeout=10: Write timeout in seconds.
