# python3 install & open env

```
## instal python & pip3
apt-get install -y python3.8  python3.8-distutils  python3-pip
pip3 install --upgrade pip


## install virturalenv
pip3 install virtualenv

## use env
cd /var/www/your_project_name
virtualenv -p python3 py-env
source py-env/bin/activate


## install module.
pip3 install Flask

## exit env

deactivate
```