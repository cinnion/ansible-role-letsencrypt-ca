# Ansible Role: Let's Encrypt CA root certificates

An Ansible Role which installs the Let's Encrypt CA certificates to hosts,
rebuilds the SSL CA certificate bundle, and then restarts the SSSD process on
RHEL hosts.

For the actual distribution of certificates for services, see my [letsencrypt-certs](https://github.com/cinnion/letsencrypt-certs)
role.

## Requirements

This role has been developed using Ansible 2.6, and presently only works with
RHEL/CentOS 6.x and 7.x.

It requires downloading the CA certificates for Let's Encrypt from their
[Chain of Trust](https://letsencrypt.org/certificates/) page and placing them
in the `files` directory of this role, with their extension changed to just 
'.pem'

N.B.: At this time, the certificates being pushed are the

* The ISRG Root X1 (self-signed) certificate.
* The Let’s Encrypt Authority X3 (IdenTrust cross-signed) certificate
* Let’s Encrypt Authority X3 (IdenTrust cross-signed)

A future version may include automatically downloading these files, or
may just include them as a part of the role source, if no issues with copyright
are found.

## Role Variables:

The following platform-specific variables are defined in the files under the
`vars` directory (see `vars/RedHat.yml`).

    ca_trusted_dir: /etc/pki/ca-trust/source/anchors

The directory where CA certificates are placed for incorporation into the
CA bundle.

    ca_update_command: update-ca-trust

The command to be run to rebuild the CA bundle.

## Dependencies

None.

## Example Playbook

```
    ---
    - hosts: all
      roles:
        - { role: letsencrypt-ca }
    ...
```

## License

This software is open-sourced software licensed under the
[Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0).

## Author Information

This role was created 2018 Dec 1 by [Douglas Needham](https://www.ka8zrt.com/).
