# Dummy API

## Headers and query parameters

The following request headers and query parameters will make an impact on the response.

### Delay

    header-delay = {float}           Delay to first header byte
    body-delay = {float}             Delay to first body byte

### Cache-control

    max-age = {int}                  Set the response max-age value
    s-maxage = {int}                 Set the response s-maxage value
    must-revalidate                  Set must-revalidate
    public                           Set public
    private                          Set private
    no-store                         Set no-store
    no-cache                         Set no-cache

### Misc

    response-status = {int}          Set the response status
    content-length                   Set the content-length, otherwise chunked encoding is used
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
        "header-delay": 1,
        "host": "somehost",
        "max-age": 2,
        "method": "GET",
        "uri": "/someurl"
    }

## Help

    GET http://somehost/?help

## Installation

    wget http://openresty.org/download/ngx_openresty-1.7.10.1.tar.gz
    tar -xvzf ngx_openresty-1.7.10.1
    cd ngx_openresty-1.7.10.1
    ./configure --with-pcre-jit --with-luajit --error-log-path=/var/log/api/error.log --http-log-path=/var/log/api/access.log --prefix=/srv/dummy-api/openresty/
    gmake
    gmake install 

