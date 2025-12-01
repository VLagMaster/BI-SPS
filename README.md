# BI-SPS
## OpenSSL
* https://gist.github.com/Soarez/9688998
### certificate signature request
* openssl genrsa -out zahorec.fit.key 4096 # generate key
* openssl rsa -in zahorec.fit.key -noout -text # inspect key

* openssl rsa -in zahorec.fit.key -pubout -out zahorec.fit.pubkey # extract public key
* openssl rsa -in zahorec.fit.pubkey -pubin -noout -text # show public key

* openssl req -new -key zahorec.fit.key -out zahorec.fit.csr # create CSR
* openssl req -in zahorec.fit.csr -noout -text # view CSR content
### creating CA

* openssl genrsa -out ca.key 4096
* openssl req -new -x509 -key ca.key -out ca.crt

### Signing CSR

* openssl x509 -req -in zahorec.fit.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out zahorec.fit.crt
* openssl x509 -req -in zahorec.fit.csr -CA ../CA-self/ca.crt -CAkey ../CA-self/ca.key -CAcreateserial -copy_extensions copyall -out zahorec.fit.cr # if you trust and want to copy extensions
* openssl x509 -in zahorec.fit.crt -noout -text # examine signed ceritificate
* cat zahorec.fit.crt ca.crt > zahorec.fit.bundle.crt # Create bundle
