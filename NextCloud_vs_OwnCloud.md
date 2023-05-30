
### Docker and NextCloud

Research from May 2019

https://github.com/nextcloud/docker#base-version---apache  use image from: https://hub.docker.com/_/nextcloud/  

create in project dir  docker-compoe.yml file and make sure to set the variables MYSQL_ROOT_PASSWORD and MYSQL_PASSWORD before you run this setup.
```yaml
version: '2'

volumes:
  nextcloud:

services:

  app:
    image: nextcloud
    ports:
      - 80:80
    volumes:
      - nextcloud:/var/www/html
    restart: always
```

open in your browser: http://localhost:8080/ and create Amind account and if you like to use MariaDB instead of SQLite clik on
'Storage & database' in TAB 'MySQL/MariaDB' and fill fields

For SQLite storage dir is: /var/www/html/data




after first start you can't access yo LAN IP address: 'Access through untrusted domain'
to fix this : https://docs.nextcloud.com/server/15/admin_manual/installation/installation_wizard.html#trusted-domains

```
apt update
apt install vim
cd /var/www/html/config
vim config.php
```

find and update trusted_domains for eaxmple:
```
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => '192.168.101.10',
),
```



### Installing NextCloud with Vagrant and Ubuntu 18.04
crate new dir

create file with name Vagrantfile add this lines: 
```
    Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
end
```

open terminal and navigate to directory that contains new created file
run command:
> vagrant up

run
>vagrant ssh
>sudo apt update

follow steps  from official documentation [Example installation on Ubuntu 18.04 LTS server](https://docs.nextcloud.com/server/15/admin_manual/installation/source_installation.html#example-installation-on-ubuntu-18-04-lts-server)


> wget https://download.nextcloud.com/server/releases/nextcloud-16.0.1.zip

> sudo apt install unzip

> unzip nextcloud-16.0.1.zip



create snapshots:
> vagrant snapshot save 'my-project-date-time'
> vagrant snapshot restore 'my-project-date-time'


> vagrant global-status

Persistent Storage:https://github.com/kusnier/vagrant-persistent-storage
