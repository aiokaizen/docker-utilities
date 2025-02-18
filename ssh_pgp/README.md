# SSH server with PGP support


## Usage
### Build and run the container
docker build -t ubuntu-ssh-gpg .

### Run the container
docker run -d -p 2222:22 --name ubuntu_gpg_container ubuntu-ssh-gpg


- user: sshuser
- password: admin@123


## PGP Commands
generate a key 
gpg --full-generate-key
gpg --armor --export <key-id> > hps_public_key.asc

gpg --armor --export-secret-keys > private.asc

sign file
gpg --armor --detach-sign <file-to-sign>

verify the sign file 
gpg --verify example.txt.asc example.txt

encryption commandes
gpg --import hps_public_key.asc 
gpg --list-keys
gpg --encrypt --recipient "hps_user" hello.txt 

gpg --encrypt --sign --recipient "hello_test" --default-key "hi_test" file.txt


decrypt commandes: 

gpg --pinentry-mode loopback --passphrase 'dzadzadzadazzda' --output hello.txt --decrypt hello.txt.gpg




delete public key
gpg --delete-key <key-id>

delete private key 
gpg --delete-secret-key <key-id>
