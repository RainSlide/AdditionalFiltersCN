# Optional rules

## Click2load Youtube iframes

``` adblock
! Click2load Youtube iframes
||youtube.com$3p,frame,redirect=click2load.html
||youtube-nocookie.com$3p,frame,redirect=click2load.html
```

Infomation & source code location of `click2load.html` can be found on [uBlock Origin wiki's Resources Library page](https://github.com/gorhill/uBlock/wiki/Resources-Library#available-resources).

## Block Google Map iframes

``` adblock
! Block Google Map iframe on ipinfo.io
||www.google.com/maps/embed/*$subdocument,domain=ipinfo.io
```
