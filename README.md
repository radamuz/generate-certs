#### Desplegar contenedor para crear los certificados necesarios:
```bash
docker run -v $PWD/certs:/certs \
  -e SSL_SUBJECT=... \ # host.domain.local
  -e SSL_DNS=... \ # host.domain.local
  -e SSL_IP=... \ # IP de servidor Rancher 
  -e CA_EXPIRE=... \ # Días en los que expira la Autoridad Certificadora
  -e SSL_EXPIRE=60 \ # Días en los que expira el SSL
  superseb/omgwtfssl
```

#### Desplegar rancher con los certificados creados anteriormente:
```bash
docker run -d \
  --restart=unless-stopped \
  -p 81:80 -p 444:443 \
  -v /root/certs/cert.pem:/etc/rancher/ssl/cert.pem \
  -v /root/certs/key.pem:/etc/rancher/ssl/key.pem \
  -v /root/certs/ca.pem:/etc/rancher/ssl/cacerts.pem \
  --privileged \
  rancher/rancher
```