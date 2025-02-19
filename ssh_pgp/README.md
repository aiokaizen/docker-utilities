# SSH server with PGP support


## Usage

### Build and run the container

docker build -t ubuntu-ssh-pgp .

### Run the container

docker run -d -p 2222:22 --name ubuntu_gpg_container ubuntu-ssh-gpg

- user: sshuser
- password: admin@123


## PGP Commands

### generate a key 

gpg --full-generate-key
gpg --armor --export <key-id> > hps_public_key.asc

gpg --armor --export-secret-keys <key-id> > private.asc

### sign file

gpg --armor --detach-sign <file-to-sign>

### verify the sign file 

gpg --verify example.txt.asc example.txt

### encryption commandes

gpg --import hps_public_key.asc 
gpg --list-keys
gpg --encrypt --recipient "hps_user" hello.txt 

gpg --encrypt --sign --recipient "hello_test" --default-key "hi_test" file.txt


### decrypt commandes: 

gpg --pinentry-mode loopback --passphrase 'dzadzadzadazzda' --output hello.txt --decrypt hello.txt.gpg


### delete public key

gpg --delete-key <key-id>


### delete private key 

gpg --delete-secret-key <key-id>


### delete private and public key

gpg --delete-secret-and-public-key <key-id>


### delete all private and public keys

```bash
gpg --list-keys --with-colons | grep '^fpr' | cut -d':' -f10 > keys.list.tmp
gpg --batch --delete-secret-and-public-key --yes $(cat keys.list.tmp)
rm -f keys.list.tmp
```


### Example config file:
```
%echo Generating an OpenPGP key
Key-Type: RSA
Key-Length: 4092
Subkey-Type: RSA
Subkey-Length: 4092
Name-Real: KeyIdentifier
Name-Email: mouadkommir@gmail.com
Name-Comment: PGP with low security
Expire-Date: 1y
Passphrase: verystrong
%commit
%echo done
```


### Unatended generation
gpg --batch --generate-key path/to/pgp.conf

### Unatended export of public key
gpg --armor --export <real-name> > path/to/public.asc

### Unatended export of secret key with passphrase
gpg --pinentry-mode loopback --passphrase <passphrase> --armor --export-secret-keys <real-name> > path/to/secret.asc

### Unatended export of secret key without passphrase
gpg --armor --export-secret-keys <real-name> > path/to/secret.asc


### Extract PGP key fingerprint
gpg --list-keys --with-colons "<real-name>" | grep "^fpr" | cut -d":" -f10
