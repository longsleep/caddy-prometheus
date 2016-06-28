# Metrics

This module enables prometheus metrics for Caddy.

## Use

In your `Caddyfile`:

~~~
prometheus
~~~

For each virtual host that you want to see metrics for.

It optionally takes an address where the metrics are exported, the default
is `localhost:9180`. The metrics path is fixed to `/metrics`.

With `caddyext` you'll need to put this module early in the chain, so that
the duration histogram actually makes sense. I've put it at number 0.

## Metrics

The following metrics are exported:

* caddy_http_request_count_total{host, family, proto}
* caddy_http_request_duration_seconds{host, family, proto}
* caddy_http_response_size_bytes{host}
* caddy_http_response_status_count_total{host, status}

Each counter has a label `host` which is the hostname used for the request/response.

The `status_count` metrics has an extra label `status` which holds the status code.

The `request_count_total` and `request_duration_seconds` also has the protocol family in the
`family` label, this is either 1 (IP version 4) or 2 (IP version 6) and the HTTP protocol major and
minor version (in the `proto` label) used: 1.x or 2 signifying HTTP/1.x or HTTP/2.
