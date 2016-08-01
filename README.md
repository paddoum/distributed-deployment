# Distributed Deployment of OSM2VectorTiles

Using traditional Ansible scripts to manage
fleet of CoreOS host. Supports preparing the
host for `docker-compose` and copying a
remote db to a local SSD.

## Configure

Configure the `group_vars/all.yml` file with the various settings.
Most important are the AWS settings and information about where
the local and master data block device reside.

## Install Workers

First bootstrap Ansible on CoreOS.

```bash
ansible-galaxy install defunctzombie.coreos-bootstrap
ansible-playbook -i inventory bootstrap.yml
```

Now install the workers.

```bash
ansible-playbook -i inventory install-worker.yml
```

## Copy from Master to Local

Copy the raw master DB data to the local disk.
This will take a long time.

```bash
ansible-playbook -i inventory copy-to-local-db.yml
```
