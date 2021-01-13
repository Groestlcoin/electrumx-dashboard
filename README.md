# ElectrumX Dashboard

ElectrumX Dashboard (EXD) is a lightweight dashboard for [ElectrumX](https://github.com/spesmilo/electrumx) servers.
Check out [Groestlcoin Node Manager](https://github.com/Groestlcoin/groestlcoin-node-manager) as a Groestlcoin Core server dashboard.

## Features

- Dashboard with general information about the server, established sessions and known peers
- List of all established sessions (including traffic, client country, isp, ...)
- List of all known peers (including client, country, isp, ...)
- Create rules to manage sessions
  - Disconnect or log sessions that violate rules
  - Set global events that trigger the execution of rules, run rules manually or set up a cron job

## Requirements

- ElectrumX 1.11.0+ (https://github.com/spesmilo/electrumx)
- Apache Web server (sudo apt install apache2)
- PHP 7.2 (sudo apt install php libapache2-mod-php)
- cURL extension for Apache (sudo apt-get install php-curl)

Restart apache after packages are installed: `sudo systemctl restart apache2`

## Installation

1. [Download](https://github.com/Groestlcoin/electrumx-dashboard/releases) EXD or clone this repository.
2. Copy `src/Config.sample.php` and remove `.sample`. Open `src/Config.php` and set your EXD password.
3. Make sure the EXD folder is in your web servers folder (e.g. `/www/html/`). If the server is publicly accessible, I recommend renaming the EXD folder to something unique. Although EXD is password protected and access can be limited to a specific IP, there can be security flaws and bugs.
4. Open the URL to the folder in your browser and login with the password choosen in `src/Config.php`.
5. Optional: Run `chmod -R 770 /path-to-folder/{data, src, views}`. Only necessary for non Apache servers (`AllowOverride All` necessary), that are publicly accessible. For more information, read next section.

## Security

- All pages and control functionality are only accessible for logged in users. The only exception is if you use the `Rules` cron job functionality. But a password based token is required and the functionality is only able to apply rules.
- Access to EXD is by default limited to localhost. This can be expanded to a specific IP or disabled. If disabled, make sure to protect the EXD folder (.htaccess or rename it to something unique that an attacker will not guess). An attacker could "guess" your password, since there is no build-in brute force protection.
- The `data` folder contains your rules, logs and geo information about your peers. Make sure to protect (e.g. `chmod -R 770 data`) this sensitive information if your web server is publicly accessible. The previously mentioned IP protection doesn't work here. If you use `Apache` you are fine, since the folder is protected with `.htaccess` (make sure `AllowOverride All` is set in your Apache config file).

## Roadmap

- [ ] Improve project structure
- [ ] Improve error handling
- [ ] Display expanded peer/session info (popup)
- [ ] Highlight suspicious sessions
