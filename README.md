# ModSecurity Proxy for BT - BSides Tallinn workshop edition

## Summary

This is Docker setup to run a WAF as reverse proxy based on ModSecurity and OWASP Core Rules set (CRS) official image.
For BSides
Tallinn 2024 workshop a notably insecure webapp, FluentBit, Elastic+Kibana and Sumologic connector were added to make
experimenting with logging setup easy.

## Setup & running

* create `.env` and `modsec.env` based on `*.example` files
* if testing with Sumologic - register free account, add API credentials to `.env` and
  un-comment `docker-compose-sumologic.yaml` in main `docker-compose.yaml`.
* launch with `docker compose up`

Note: there appears to be a concurrency issue with docker logging driver and Fluent Bit, running `docker compose up`
again is temporary fix until better health check is added.

## Inescure components

* `petskratt/burn-after-reading` evals PHP code entered in form. This is intended behavior.
* Logging request/response and headers will log also credentials, session cookies and potentially confidential
  information. When using this template for production setup you can use `MODSEC_AUDIT_LOG_PARTS` in `modsec.env` to
  adjust logging or use example LUA script in `fluent-bit.conf` to sanitize logged data.

## Files and folders

Using the official OWASP image for ModSecurity-CRS as a base image.

**References:**

* [modsecurity-crs-docker](https://github.com/coreruleset/modsecurity-crs-docker)
