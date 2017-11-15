# Drupal 8 Varnish integration

This repository contains the reference configuration files to integrate Varnish with Drupal 8 using the two modules: purge and varnish_purge.

Files:

- default.vcl - Varnish VCL file tailored for Drupal
- varnish.params - Varnish configuration file
- varnish_purger.settings.UNIQUEID.yml - Purger configuration file

**Important** - The BAN requests must be made to the proper virtual host of your server one that will return HTTP 200 and properly direct the request to Varnish. This means that the `hostname` parameter in the purger must point to `your-domain.org`, and not to `www.your-domain.org` which does a redirect 301 to `your-domain.org`.

A typical deployment setup for a simple site (no load balancing) is:

```
| nginx:80 | ===> | varnish:6081 | ===> | nginx:8080 | ===> | php-fpm unix:/socket |
                                                     | ===> | static/files/on/disk |
```
