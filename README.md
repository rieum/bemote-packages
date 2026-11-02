# BeMote

BeMote is a bastion for SSH, RDP and web (HTTP) servers, used entirely from the browser. It replaces Apache Guacamole with a chat-style interface: projects hold their servers in folders, members see who is connected, sessions can be shared and watched together, and every session can be recorded and played back. Sign-in works with local accounts, LDAP/Active Directory or single sign-on (OIDC), with TOTP two-factor authentication. Server credentials are stored encrypted and are never shown to users.

BeMote ships as an appliance: a CentOS Stream 10 ISO that installs everything (BeMote, guacd, PostgreSQL) without network access.

This repository only distributes the built packages. The source code is not public.

## Download

- **Latest ISO**: [bemote-x86_64.iso](https://github.com/rieum/bemote-packages/releases/latest/download/bemote-x86_64.iso) ([SHA256SUMS](https://github.com/rieum/bemote-packages/releases/latest/download/SHA256SUMS)). This link always gives the newest release; its version is in the [release notes](https://github.com/rieum/bemote-packages/releases/latest).
- **Older versions and RPMs**: see [Releases](https://github.com/rieum/bemote-packages/releases). Each release lists `SHA256SUMS` and the signing key.
- **Updates**: appliances installed from the ISO update with `dnf update`, or from **Admin → Updates** in BeMote. The dnf repository is published here with GitHub Pages: `https://rieum.github.io/bemote-packages/10/x86_64/`.

Packages and repository metadata are signed with the key in [`RPM-GPG-KEY-bemote`](RPM-GPG-KEY-bemote). To add the repository to an existing CentOS Stream 10 host:

```
rpm --import https://rieum.github.io/bemote-packages/RPM-GPG-KEY-bemote
dnf install -y epel-release
dnf --repofrompath=bemote-tmp,https://rieum.github.io/bemote-packages/10/x86_64/ --repo=bemote-tmp install -y bemote-release
dnf install -y bemote
```

## Legal notices

### BeMote

BeMote (the `bemote` and `bemote-release` packages, and the BeMote web interface) is proprietary software. Copyright © 2026 the BeMote authors. All rights reserved. You may download and install these packages to run BeMote; no other right to copy, modify or redistribute BeMote is granted. BeMote is provided "as is", without warranty of any kind.

### Apache Guacamole (guacd)

The `guacd` package is the guacd proxy daemon of [Apache Guacamole](https://guacamole.apache.org/), built without changes from the official source release (guacamole-server 1.6.0, [download](https://archive.apache.org/dist/guacamole/1.6.0/source/)), with telnet and Kubernetes support left out. BeMote talks to guacd over its documented protocol and does not include Guacamole's web application.

Apache Guacamole is Copyright © The Apache Software Foundation, and is licensed under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0). The package installs Guacamole's `LICENSE` and `NOTICE` files in `/usr/share/licenses/guacd/`. Apache, Apache Guacamole and Guacamole are trademarks of The Apache Software Foundation. BeMote is not affiliated with or endorsed by The Apache Software Foundation.

guacd links to system libraries from CentOS Stream and EPEL, under their own licenses, among them FreeRDP (Apache-2.0), libssh2 (BSD-3-Clause), LibVNCServer (GPL-2.0-or-later), Cairo and Pango (LGPL), libjpeg-turbo, libpng and libwebp.

### Components built into BeMote

| Component | License |
|---|---|
| [Go](https://go.dev/) standard library | BSD-3-Clause |
| [golang.org/x/crypto, oauth2, sync, text](https://cs.opensource.google/go/x) | BSD-3-Clause |
| [github.com/jackc/pgx](https://github.com/jackc/pgx), pgpassfile, pgservicefile, puddle | MIT |
| [github.com/coder/websocket](https://github.com/coder/websocket) | ISC |
| [github.com/coreos/go-oidc](https://github.com/coreos/go-oidc) | Apache-2.0 |
| [github.com/go-jose/go-jose](https://github.com/go-jose/go-jose) | Apache-2.0 |
| [github.com/go-ldap/ldap](https://github.com/go-ldap/ldap), [go-asn1-ber](https://github.com/go-asn1-ber/asn1-ber) | MIT |
| [github.com/Azure/go-ntlmssp](https://github.com/Azure/go-ntlmssp) | MIT |
| [github.com/google/uuid](https://github.com/google/uuid) | BSD-3-Clause |
| [guacamole-common-js](https://guacamole.apache.org/) (Apache Guacamole) | Apache-2.0 |
| [React](https://react.dev/), react-dom | MIT |
| [highlight.js](https://highlightjs.org/) | BSD-3-Clause |
| [node-qrcode](https://github.com/soldair/node-qrcode) | MIT |
| [Figtree](https://github.com/erikdkennedy/figtree) and [JetBrains Mono](https://www.jetbrains.com/lp/mono/) fonts (via Fontsource) | SIL Open Font License 1.1 |

The full license texts of these components are available from the links above.

### The ISO

Besides BeMote and guacd, the ISO contains unmodified packages from [CentOS Stream 10](https://www.centos.org/centos-stream/) and [EPEL 10](https://docs.fedoraproject.org/en-US/epel/) (among them the Linux kernel, PostgreSQL, Firefox, cage and wayvnc), each under its own license, recorded in its RPM header (`rpm -qi <package>`) and license files under `/usr/share/licenses/`. Their source code is available from the CentOS Stream and EPEL source repositories (`dnf download --source <package>`), and on request. The boot menu is relabelled "BeMote"; CentOS is a trademark of Red Hat, Inc., and BeMote is not affiliated with or endorsed by Red Hat or the CentOS Project.
