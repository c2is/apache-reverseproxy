# Apache Reverse Proxy container

# Generate certificate

To use this container you need to generate the certificate.

If you decide to extends the container add this line in your Dockerfile.
The `-subj` option is used to configure the certificate:
C (Country Name)
ST (State or Province Name)
L (Locality)
O (Organization Name)
CN (Common Name like FQDN)

exemple:
```
# Dockerfile
FROM c2is/apache-reverseproxy

RUN openssl req \
    -new \
    -newkey rsa:4096 \
    -days 365 \
    -nodes \
    -x509 \
    -subj "/C=FR/ST=c2is/L=Lyon/O=c2is/CN=www.exemple.com" \
    -keyout /etc/apache2/ssl/proxy.key \
    -out /etc/apache2/ssl/proxy.crt
```

If you decide to just use the image in docker-compose.yml add the command to the declaration:

```
reverseproxy:
    image: c2is-apache-reverseproxy
    command: openssl req -new -newkey rsa:4096 -days 365 -nodes -x509 -subj "/C=FR/ST=c2is/L=Lyon/O=c2is/CN=www.exemple.com" -keyout /etc/apache2/ssl/proxy.key -out /etc/apache2/ssl/proxy.crt
```
