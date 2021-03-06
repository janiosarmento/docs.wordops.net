# F.A.Q

## General

#### What is WordOps ?

WordOps is a command line tool which ease server administration and WordPress deployment by providing the ability to setup an optimized LEMP stack (Nginx, PHP, MySQL) with simple command like `wo stack install --nginx`.

#### What are WordOps main features ?

WordOps not only installs and configures the packages needed to deploy a site (Nginx, PHP, MariaDB) but it also takes care of creating Nginx vhosts and the database, installing WordPress and even get a Let's Encrypt SSL certificate, all in one command line. It support multiple cache backend for WordPress, including Nginx fastcgi_cache, Redis cache (full-page cache + object cache) or wp-super-cache, based on a highly optimized Nginx configuration and an hardened security with strict location directives.

#### Which operating systems are supported by WordOps ?

WordOps can be installed on Ubuntu LTS (Long Term Service) releases (16.04 & 18.04) as well as on Debian 8 (Jessie) or Debian 9 (stretch) Support for other linux distribution isn't planned.

#### Are you planning to add support for other operating systems ?

We will probably try to add support for Raspbian (Debian on raspberry pi) as our Nginx package already support this platform. Otherwise, adding support for other operating systems isn't planned.

## Technical

#### Which version of PHP does WordOps support ?

WordOps support PHP 7.2 (default) and PHP 7.3.

#### What is the best caching solution for WordPress ?

There is no "best solution", because there are benefits/disadvantage for each caching solution and it depend on your usage.

Here some informations :

Cache backend  | command argument | description
-------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
fastcgi_cache  | `--wpfc`         | the simplest solution, because it do not rely on any plugin excepted nginx_helper used to purge cache after content updates                                                  |
redis-cache    | `--wpredis`      | powerful solution which support multi-server setup and it provide full-page cache in redis via Nginx + object-cache via Redis-Object-Cache plugin (also used to purge cache)
wp-super-cache | `--wpsc`         | basic solution based on a plugin which create and serve static html files.                                                                                                   |

#### Does WordOps support WP-Rocket ?

At the moment, WP-Rocket works properly on WordOps but do not receive any performance boost from our Nginx configuration. We are going to work on it and to provide additional Nginx configurations for WP-Rocket.

#### Why do I get warning from my web browser when opening WordOps backend ?

At the moment, WordOps backend is secured with a self-signed SSL certificate, which provide the same level of encryption than any other certificate but do not come from a certificate authority. Your Web browser only warn you about the fact that the certificate wasn't issued by a trusted certificate authority. We are already working on adding the ability to secure WordOps backend with a letsencrypt SSL certificate.

#### Does Nginx-wo support TLSv1.3 ?

No, currently our custom Nginx package isn't built with OpenSSL 1.1+ and Nginx-wo only support TLSv1.0 TLSv1.1 and TLSv1.2.

#### Why gzip compression is disabled by default ?

We disabled gzip compression by default due to gzip related security issues when using TLS connection. More informations here [BREACH CVE](https://en.wikipedia.org/wiki/BREACH). We replaced gzip by brotli, which provide better performance and compression than gzip.
