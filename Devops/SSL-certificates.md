# SSL (HTTPS) certificates

Each website will require a new SSL certificate once a year. You'll get the following files

- Crt (website certificate). This can also be extracted from the PFX file if necessary
- Ca-bundle (certificates for the higher-up certificate signing authorities)
- Pfx (contains private key - encrypted with password)

Basically what you should do:

## Merge CRT and CA-BUNDLE

```sh
cat <certificate>.crt <ca-bundle>.ca-bundle | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > fullchain.pem
```

You may need to rename files or change their extension.

e.g.:
```sh
cat ster.vlpdata.be.crt ca-bundle.ca-bundle | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > fullchain.pem
```

## Extract private key from PFX

```sh
openssl pkcs12 -in <pfx>.pfx -nocerts -out encrypted.key
```

Password can be asked from MAPA (ask them to send it by sms! We don't want both password and certificates through the same communication channel!).

Decrypt the file now

```sh
openssl rsa -in encrypted.key -out decrypted.key
```

## Install on server

Upload the `fullchain.pem` and `decrypted.key` to the relevant folder in `/etc/ssl`. After this edit the necessary nginx configs in `/etc/nginx/sites-available` and change the `ssl_certificate` and `ssl_certificate_key` paths.

Now restart the NGINX server using `sudo service nginx restart`. If something was configured incorrectly it'll tel you it can't start things and it'll also tell you how to see the logs.