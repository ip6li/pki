# Simple PKI

This is a simple PKI solution based on Bash and OpenSSL.

# Usecases

This script collection ca be used for

* Developers which want to test their software regarding real life certificate szenarios.
* Home and SOHO users which wants to get back control about their certificates.

# Limitiations

* It does not create CRLs (for now)
* It does provide a OCSP server.
* It is not for use in enterprise environments.

# mk-csr

This script is for creating PKCS#10 certificate request. It is able to accept
subject alternative names, which are required for official server certificates.

## Options

```
-r | --rsa             creates a RSA keys
-e | --prime256v1      creates a prime256v1 key
--secp521r1            creates a secp521r1 key
--alg <alg>            creates a <alg> key, <alg> must be supported by OpenSSL
--client               creates a CSR for a client certificate (No SNI)
--server               creates a CSR for a server certificate (SNI/DNS accepted)
--mod <bits>           uses <bits> for RSA key
```

## Examples

    ./mk-csr --rsa --mod 2048  test1.example.com test2.example.com test3.example.com
    ./mk-csr --prime256v1  test1.example.com test2.example.com test3.example.com

# mk-crt

This script creates a selfsigned CA certificate. Options similar to mk-csr.

# mk-pkcs12

Create from <file>.key, <file>.crt and ca.crt a PKCS#12 keystore. It my be usable to install
a certificate chain into appliances or for Java applications.

## Options

```
--name <name>          Friendly name for certificate
--cafile <ca file>     Use an other CA file, e.g. intermediate CA certificate
```


# PKI

This creates a directory structure for a small PKI if you need a certificaty hierarchy.
Script ./sign allows you to sign certificates with generated CA certificates.

## gen-ca

Creates a directory structure for a small PKI, options similar to mk-csr.

## sign

Signs CSR. Options:

```
-c | --client    Sets key usage attributes for a client certificate.
-s | --server    Sets key usage attributes for a server certificate.
--ca             Sets key usage attributes for a CA certificate and sets CA=true.
--signca         Sign with an other CA, e.g. intermediate CA.
```

