# Improved Nginx configuration files <!-- omit in toc --> 

These are configuration files for Nginx with some settings to improve aspects such as performance and security, as well as handling some possible errors. Designed for a setup based on server blocks as seen [here](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04).

*Last tested on Nginx 1.18.0 on Ubuntu 20.04.*

## Table of contents <!-- omit in toc --> 

- [Usage](#usage)
  - [First time only](#first-time-only)
  - [For every site](#for-every-site)
    - [Prerequisites](#prerequisites)
    - [Nginx configuration](#nginx-configuration)
- [Sources](#sources)

## Usage

### First time only

The steps in this section are only done when setting up the server for the first time.

Disable the `default` file:

`sudo rm /etc/nginx/sites-enabled/default`

Back up the default `nginx.conf` configuration file:

`sudo mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bck`

Recreate it:

`sudo nano /etc/nginx/nginx.conf`

Paste the contents of the improved [nginx.conf](https://raw.githubusercontent.com/ManuelFte/Improved-Nginx-configuration-files/master/nginx.conf) file from this repository.

Test that the configuration is correct:

`sudo nginx -t`

Reload to apply changes:

`sudo systemctl reload nginx`

### For every site

The steps in this section should be done for every site you want to add.

Note: In all the following commands, replace `example.com` with your domain.

#### Prerequisites

This configuration file assumes that your site's files reside in `/var/www/example.com/html`. If this is not the case, do the following:

Create that directory:

`sudo mkdir -p /var/www/example.com/html`

Give it the appropriate permissions:

`sudo chown -R $USER:$USER /var/www/example.com/html`

`sudo chmod -R 755 /var/www`

Upload your files into that directory.

#### Nginx configuration

Open the contents of [example.com.conf](https://raw.githubusercontent.com/ManuelFte/Improved-Nginx-configuration-files/master/example.com.conf) with a text editor and use `CTRL` + `H` to replace all instances of `example.com` with your domain.

On the server, create a new file for the domain you're going to set up:

`sudo nano /etc/nginx/sites-available/example.com`

Paste the contents of the previous file there (note that the file in this repository has a `.conf` extension merely for code-highlighting purposes, the file in your server must not have this extension).

Enable it:

`sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/`

Test that the configuration is correct:

`sudo nginx -t`

Reload to apply changes:

`sudo systemctl reload nginx`

Your website should now be live in your domain.

## Sources

* https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-nginx-on-centos-7
* https://geekflare.com/nginx-production-configuration/
* https://gist.github.com/plentz/6737338
* https://stackoverflow.com/questions/9824328/why-is-nginx-responding-to-any-domain-name/9826635
* https://nginx.org/en/docs/http/ngx_http_gzip_module.html
* https://www.codetd.com/en/article/6286848
* https://nginx.org/en/docs/ngx_core_module.html
* https://docs.nginx.com/nginx/admin-guide/monitoring/logging/
* https://nginx.org/en/docs/http/ngx_http_core_module.html
* https://medium.com/staqu-dev-logs/optimizations-tuning-nginx-for-better-rps-of-an-http-api-de2a0919744a
* https://www.digitalocean.com/community/tutorials/how-to-optimize-nginx-configuration
* https://www.digitalocean.com/community/tutorials/how-to-host-a-website-using-cloudflare-and-nginx-on-ubuntu-20-04
* https://jekyllrb.com/tutorials/custom-404-page/#hosting-on-nginx-server