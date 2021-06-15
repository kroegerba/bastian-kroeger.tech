---
title: Certificates & Keys
description: 15.06.2021
---
# OpenSSL
#### Creating Certificate Signing Requests (CSRs)
```bash
openssl req -new -config myserver.cnf -keyout myserver.key -out myserver.csr
```
example file: https://www.phcomp.co.uk/Tutorials/Web-Technologies/example.cnf.txt
#### Bundling Certificates as PKCS #12

```bash
openssl pkcs12 -export -out domain.name.pfx -inkey domain.name.key -in domain.name.crt
```
If you have a root CA and intermediate certs, then include them as well using multiple -in params:
```bash
openssl pkcs12 -export -out domain.name.pfx -inkey domain.name.key -in domain.name.crt -in intermediate.crt -in rootca.crt
```
source: https://stackoverflow.com/a/17284371
# SSH
#### SSH-Keys In General
I would personally rather create a keypair with OpenSSH from the beginning.
#### WinSCP (OpenSSH -> PuTTY)
WinSCP supports [command-line conversion of private keys from the OpenSSH (or ssh.com) format to the PuTTY `.ppk` format.](https://winscp.net/eng/docs/commandline#keygen)
```bash
winscp.com /keygen mykey.pem /output=mykey.ppk
```
source: https://superuser.com/a/912618
#### OpenSSH (PuTTY -> OpenSSH)
If all you have is a public key from a user in PuTTY-style format, you can convert it to standard openssh format like so:
```bash
ssh-keygen -i -f keyfile.pub > newkeyfile.pub
```
source: https://stackoverflow.com/a/10015651
#### PuTTY (PuTTY -> OpenSSH)
To generate the private key:
```bash
puttygen id_dsa.ppk -O private-openssh -o id_dsa
```
and to generate the public key:
```bash
puttygen id_dsa.ppk -O public-openssh -o id_dsa.pub
```
source: https://superuser.com/a/232365
#### OpenSSH (OpenSSH <-> SSH2)
Convert OpenSSH key to SSH2 key:
```bash
ssh-keygen -e -f ~/.ssh/id_dsa.pub > ~/.ssh/id_dsa_ssh2.pub
```
Convert SSH2 key to OpenSSH key:
```bash
ssh-keygen -i -f ~/.ssh/id_dsa.pub > ~/.ssh/id_dsa_openssh.pub
````
source: https://burnz.wordpress.com/2007/12/14/ssh-convert-openssh-to-ssh2-and-vise-versa/