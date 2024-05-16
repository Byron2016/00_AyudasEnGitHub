# Laravel Homestead

## Referencias

- [Laravel Homestead](https://laravel.com/docs/11.x/homestead)
- Errores

  - Error 01: No encuentra los rsa.

    - [Error 01](https://stackoverflow.com/questions/44463987/homestead-installation)

  - Error 02: Time out claves ssh

## Pasos instalación

- Installing Homestead

```Shell
git clone https://github.com/laravel/homestead.git ~/Homestead
```

- Checkout the release branch

```Shell
cd ~/Homestead

git checkout release
```

- Create the Homestead.yaml configuration file

```Shell
# macOS / Linux...
bash init.sh
```

- Configuring Homestead: Setting Your Provider

```Shell
provider: virtualbox
```

- Configuring Homestead: Configuring Shared Folders

```Shell
folders:
    - map: D:\dev_20220602\homestead_BASE_20240514\code\proyecto_00_HomesteadTest
    to: /home/vagrant/code/proyecto_00_HomesteadTest

    - map: ~/code/project1
      to: /home/vagrant/project1
```

- Configuring Nginx Sites

```Shell
sites:
  - map: prueba.test
    to: /home/vagrant/code/proyecto_00_HomesteadTest/public

    - map: homestead.test
      to: /home/vagrant/project1/public
```

> If you change the sites property after provisioning the Homestead virtual machine, you should execute the **vagrant reload --provision** command in your terminal to update the Nginx configuration on the virtual machine.

- Hostname Resolution

> Using automatic hostnames works best for per project installations of Homestead. If you host multiple sites on a single Homestead instance, you may add the "domains" for your web sites to the hosts file on your machine. The hosts file will redirect requests for your Homestead sites into your Homestead virtual machine. On macOS and Linux, this file is located at /etc/hosts. On Windows, it is located at C:\Windows\System32\drivers\etc\hosts. **Debe ser abierto como administrador** The lines you add to this file will look like the following:

```Shell
192.168.56.56  homestead.test
```

```HTML
http://homestead.test
```

- Configuring Services

```Shell
services:
    - enabled:
        - "postgresql"
    - disabled:
        - "mysql"
```

- Launching the Vagrant Box

```Shell
vagrant up
```

- sss
- sss

## Errores

### Error 01

- Check your Homestead.yaml (or Homestead.json) file, the path to your private key does not exist.

- Reproducir

```Shell
cd Homestead

vagrant up
```

- Solución

```Shell
cd ~/.ssh/

# Generate a ssh key

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Start ssh agent

eval "$(ssh-agent -s)"

# Add your SSH private key to the ssh-agent

ssh-add -k ~/.ssh/id_rsa

# Then run vagrant up

vagrant up
```

### Error 02

- Time out ssh private key

- Reproducir

```Shell
vagrant up
```

- Solución

- Tener abierto el **Virtual Box**
