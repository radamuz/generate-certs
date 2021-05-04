#### Desplegar contenedor para crear los certificados necesarios:
```
docker run -v $PWD/certs:/certs \
  -e SSL_SUBJECT=... \
  -e SSL_DNS=... \
  -e SSL_IP=... \
  -e CA_EXPIRE=... \
  -e SSL_EXPIRE=... \
  superseb/omgwtfssl
```

#### Desplegar rancher con los certificados creados anteriormente:
```
docker run -d \
  --restart=unless-stopped \
  -p 81:80 -p 444:443 \
  -v /root/certs/cert.pem:/etc/rancher/ssl/cert.pem \
  -v /root/certs/key.pem:/etc/rancher/ssl/key.pem \
  -v /root/certs/ca.pem:/etc/rancher/ssl/cacerts.pem \
  --privileged \
  rancher/rancher
```