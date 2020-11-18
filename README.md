# Ansible Role: Postfix

[![CI](https://github.com/geerlingguy/ansible-role-postfix/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-postfix/actions?query=workflow%3ACI)

Installs postfix on RedHat/CentOS or Debian/Ubuntu.

## Requirements

If you're using this as an SMTP relay server, you will need to do that on your own, and open TCP port 25 in your server firewall.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    postfix_config_file: /etc/postfix/main.cf

The path to the Postfix `main.cf` configuration file.

    postfix_service_state: started
    postfix_service_enabled: true

The state in which the Postfix service should be after this role runs, and whether to enable the service on startup.

    postfix_inet_interfaces: localhost
    postfix_inet_protocols: all

Options for values `inet_interfaces` and `inet_protocols` in the `main.cf` file.

The domain and origin of the mail domain. Change them in the event that your domain of your machine is not the same as your mail domain. 
	mydomain: $mydomain
	myorigin: $myhostname

The masquerade domain also needs to be changed to the mail domain 
	masquerade_domains: $mydomain

The MyDestination also needs to be pointed to your mail relay or mail server.
The list of domains that are delivered via the $local_transport mail delivery transport. By default this is the Postfix local delivery agent.
	mydestination: $myhostname, localhost.$mydomain, localhost

The next-hop destination(s) for non-local mail; overrides non-local domains in recipient addresses.
relayhost: $mydomain

smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated reject_unauth_destination

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - geerlingguy.postfix

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
This role was modified in 2020 by PenguinPerk to refactor to run with Freebsd and Linux.
