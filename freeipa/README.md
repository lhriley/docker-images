# Docker container for the FreeIPA server with FreeNAS metadata

**This container will work on FreeNAS and non-FreeNAS docker implementations**

This container follows the latest FreeIPA current stable/general availability release.

This container is built from the official `freeipa/freeipa-server` Docker Hub repository, and defaults to the `latest` tag (`fedora-25`).

## Usage

The container only has a single environment variable to pass to the container
* `TZ` - Configures the timezone, e.g. "America/Chicago"
- If you don't know your timezone value, you can look it up (see: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

This container exposes one volume:
* `/data` - FreeIPA data

This container exposes the following ports (see: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Linux_Domain_Identity_Authentication_and_Policy_Guide/installing-ipa.html#prereq-ports):
* `HTTP/HTTPS  80, 443 TCP`
* `LDAP/LDAPS  389, 636  TCP`
* `Kerberos  88, 464 TCP/UDP`
* `DNS 53  TCP/UDP`
* `NTP 123 UDP`
* `7389 9443 9444 9445 TCP`

You must set the `Advanced -> Hostname` to a valid FQDN or FreeIPA will refuse to start.

### Setup

By default, the `ipa-server-install` command is interactive. However, you can put a `ipa-server-install-options` file with command line parameters to append to the `ipa-server-install` command into the directory mounted as `/data`.

`ipa-server-install-options` example:

```
-U
--domain=<domain.test>
--realm=<EXAMPLE.TEST>
--ds-password=<The-directory-server-password>
--admin-password=<The-admin-password>
```

For more details see: https://hub.docker.com/r/freeipa/freeipa-server/

**If you're having trouble** tail `<FreeIPA Dataset>/data/var/log/ipaserver-install.log` for more information.


## Upgrading

**It is highly recommended to backup your data prior to installing updates.**

## Additional information:

* https://www.freeipa.org/page/Documentation
* https://www.freeipa.org/page/Docker
* https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Linux_Domain_Identity_Authentication_and_Policy_Guide/index.html
* https://hub.docker.com/r/freeipa/freeipa-server/