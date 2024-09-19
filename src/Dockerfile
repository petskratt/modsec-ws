ARG MODSECURITY_TAG

FROM owasp/modsecurity-crs:$MODSECURITY_TAG

USER root

COPY etc/ /etc/
COPY html/ /usr/share/nginx/html/
COPY rules/* /opt/owasp-crs/rules
