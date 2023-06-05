# certbot install & cert config

## To use certbot, you'll need.
- a website is already online.
- open port 80.

## Install snapd

```bash

 # Ensure that your version of snapd is up to date
 sudo snap install core;sudo snap refresh core
 
 # Remove certbot-auto and any Certbot OS packages

sudo apt-get remove certbot,
sudo dnf remove certbot
sudo yum remove certbot.

# Install Certbot
sudo snap install --classic certbot 

# Prepare the Certbot command
sudo ln -s /snap/bin/certbot /usr/bin/certbot

# Choose how you'd like to run Certbot, or help to get more options.
sudo certbot --nginx (--manual)

# Test automatic renewal
sudo certbot renew --dry-run

# Confirm that certbot worked
visit https://yourwebsite.com/ in your browser and look for the lock icon in the URL bar.

```

from "https://certbot.eff.org/instructions?ws=nginx&os=ubuntubionic"