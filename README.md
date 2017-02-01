docker-stackstorm
=================
Contains the files required to run Stackstorm on Docker.

Based heavily on the [Stackstorm st2-dockerfiles repository](https://github.com/stackstorm/st2-dockerfiles)
but simplified and modified slightly for my own ease of use, and to use Docker Hub's auto-build functionality.

##Usage
Generate or copy the requisite SSH keys to the `data` directory:

```bash
ssh-keygen -f data/id_rsa
```
or
```bash
cp -p ~/.ssh/id_rsa* data/
```

Also copy a `known_hosts` file which contains the SSH key hashes for any hosts you wish to connect
to over SSH, such as Github and Bitbucket:

```bash
cp ~/.ssh/known_hosts data/
```

Modify or recreate the `htpasswd` file for your Stackstorm user (on Ubuntu, this tool comes from
the `apache2-utils` package):

```bash
# Truncate the file first if you wish to remove the default st2admin user:
> data/htpasswd
htpasswd data/htpasswd <yourusername>
```

Bring the stack up with `docker-compose`:
```bash
docker-compose up -d
```

##Packs
Once the services have started up and you're able to run commands with the `st2` CLI client, you may
want to install a list of packs which your organisation uses.

Create a file listing your requirements (`packs.txt`):
```
ansible
git@bitbucket.org:0x07ltd/pack-yourpack.git
git@bitbucket.org:0x07ltd/pack-yourotherpack.git
```

Install the packs:
```bash
xargs st2 pack install < packs.txt
```
