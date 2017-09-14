# Ansible Role: MSMTP

Installs MSMTP on Linux.

**msmtp is an SMTP client developing by Martin Lambers**

[http://msmtp.sourceforge.net/](http://msmtp.sourceforge.net/)

In the default mode, it transmits a mail to an SMTP server (for example at a
free mail provider) which takes care of further delivery.
To use this program with your mail user agent (MUA), create a configuration
file with your mail account(s) and tell your MUA to call msmtp instead
of /usr/sbin/sendmail.

Features include:

* Sendmail compatible interface (command line options and exit codes)
* Support for multiple accounts
* TLS/SSL support including client certificates
* Many authentication methods
* Support for Internationalized Domain Names (IDN)
* Fast SMTP implementation using command pipelining
* DSN (Delivery Status Notification) support
* SOCKS proxy support

msmtp is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 3 of the License, or (at your option) any later
version.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

At least 'default' account MUST be present

    msmtp_accounts: []

    - name: 'default'
  
      #
      # GENERAL
      #
    
      # The SMTP server to send the mail to. The argument may be a host name or
      # a network address. Every account definition must contain this command.    
      # host: (host)
      host: 'smtp.yourdomain.tld'
  
      # The port that the SMTP server listens on. The default is 25 ("smtp"), unless
      # TLS without STARTTLS is used, in which case it is 465 ("smtps").
      # port: (port)
      port: '25'
  
      # Set or unset a network timeout, in seconds. The argument ‘off’ means that
      # no timeout will be set, which means that the operating system default will be
      # used.    
      # timeout: (off|seconds)
      timeout: 'off'
  
      # Use a SOCKS proxy. All network traffic will go through this proxy host, includ-
      # ing DNS queries, except for a DNS query that might be necessary to resolve    
      # the proxy host name itself (this can be avoided by using an IP address as proxy
      # host name). An empty argument disables proxy usage. The supported SOCKS
      # protocol version is 5.
      # proxy_host: [IP|hostname]
      proxy_host: 'localhost'
  
      # Set the port number for the proxy host. An empty ‘number’ argument resets
      # this to the default port, which is 1080 ("socks").
      # proxy_port: [number]
      proxy_port: '1080'
  
      # Set the protocol to use. Currently only SMTP and LMTP are supported.
      # SMTP is the default.
      # protocol: (smtp|lmtp)
      protocol: 'smtp'
      
      # This command sets the argument of the SMTP EHLO (or LMTP LHLO) com-
      # mand. The default is ‘localhost’, which is stupid but usually works. Try to
      # change the default if mails get rejected due to anti-SPAM measures. Possi-
      # ble choices are the domain part of your mail address (provider.example for
      # joe@provider.example) or the fully qualified domain name of your host (if
      # available).
      # domain: yourdomain.tld
      domain: 'yourdomain.tld'
      
      #
      # AUTHENTICATION
      #
      
      # Enable or disable authentication and optionally choose a method to use. The
      # argument ‘on’ chooses a method automatically. Accepted methods are ‘plain’,
      # ‘scram-sha-1’, ‘cram-md5’, ‘gssapi’, ‘external’, ‘digest-md5’, ‘login’, and
      # ‘ntlm’.
      # auth: [(on|off|method)]
      auth: 'on'
  
      # Set the user name for authentication. An empty argument unsets the user
      # name. Authentication must be activated with the ‘auth’ command.
      # user: [username]
      user: 'admin@yourdomain.tld'
  
      # Set the password for authentication. An empty argument unsets the pass-
      # word. Consider using the ‘passwordeval’ command or a key ring instead of
      # this command, to avoid storing plain text passwords in the configuration file.
      # password: [secret]
      password: 'secretpassword'
  
      # Set the password for authentication to the output (stdout) of the command eval.
      # This can be used e.g. to decrypt password files on the fly or to query key rings,
      # and thus to avoid storing plain text passwords.
      # passwordeval: [eval]
      passwordeval: 'eval-password-command'
      
      # Set a domain for the ‘ntlm’ authentication method. This is obsolete.    
      # ntlmdomain: [ntlmdomain]
      ntlmdomain: 'ntlmdomain'
      
      #
      # TLS
      #
      
      # Enable or disable TLS (also known as SSL) for secured connections. You also
      # need ‘tls_trust_file’ or ‘tls_fingerprint’, and for some servers you may
      # need to disable ‘tls_starttls’.
      # tls: [(on|off)]
      tls: 'on'
      
      # Choose the TLS variant: start TLS from within the session (‘on’, default), or
      # tunnel the session through TLS (‘off’).
      # tls_starttls: [(on|off)]
      tls_starttls: 'off'
  
      # Activate server certificate verification using a list of truted Certification Au-
      # thorities (CAs). The file must be in PEM format. Some systems provide
      # a system-wide default file, e.g. /etc/ssl/certs/ca-certificates.crt on
      # Debian-based systems with the ‘ca-certificates’ package. An empty ar-
      # gument disables this. You should also use ‘tls_crl_file’.
      # tls_trust_file: [file]
      tls_trust_file: '/etc/ssl/certs/ca-certificates.crt'
  
      # Set a certificate revocation list (CRL) file for TLS, to check for revoked certifi-
      # cates. An empty argument disables this.
      # tls_crl_file: [file]
      tls_crl_file: '/etc/ssl/certs/tls-crl-file'
      
      # Set the fingerprint of a single certificate to accept for TLS. This certificate will
      # be trusted regardless of its contents. The fingerprint should be of type SHA256,
      # but can for backwards compatibility also be of type SHA1 or MD5 (please avoid
      # this). The format should be 01:23:45:67:....
      # tls_fingerprint: [fingerprint]
      tls_fingerprint: '01:23:45:67'
      
      # Send a client certificate to the server (use this together with ‘tls_cert_file’).
      # The file must contain the private key of a certificate in PEM format. An empty
      # argument disables this feature.
      # tls_key_file: [file]
      tls_key_file: 'tls-key-file'
      
      # Send a client certificate to the server (use this together with ‘tls_key_file’).
      # The file must contain a certificate in PEM format. An empty argument disables
      # this feature.
      # tls_cert_file: [file]
      tls_cert_file: 'tls-cert-file'
      
      # Enable or disable checks of the server certificate.
      # WARNING: When the checks are disabled, TLS sessions will be vulnerable to
      # man-in-the-middle attacks!
      # tls_certcheck: [(on|off)]
      tls_certcheck: 'on'
      
      # Set or unset the minimum number of Diffie-Hellman (DH) prime bits accepted
      # for TLS sessions. The default is set by the TLS library and can be selected by
      # using an empty argument to this command. Only lower the default (for example
      # to 512 bits) if there is no other way to make TLS work with the remote server.
      # tls_min_dh_prime_bits: [bits]
      tls_min_dh_prime_bits: '512'
      
      # Set the priorities for TLS sessions. The default is set by the TLS library and
      # can be selected by using an empty argument to this command. See the GnuTLS
      # documentation of the ‘gnutls_priority_init’ function for a description of the
      # priorities string.
      # tls_priorities: [priorities]
      tls_priorities: 'TLS1.1'
  
      #
      # SENDMAIL
      #
      
      # Set the envelope-from address. This is usually required, but sometimes
      # ‘auto_from’ is a useful alternative.
      # from [address]
      from: 'noreply@yourdomain.tld'
  
      # Enable or disable automatic envelope-from addresses. The default is ‘off’.
      # When enabled, an envelope-from address of the form user@domain will be gen-
      # erated. The local part will be set to USER or, if that fails, to LOGNAME or, if that
      # fails, to the login name of the current user. The domain part can be set with
      # the ‘maildomain’ command; if that is empty, the address not have a domain
      # part.
      # auto_from: [(on|off)]
      auto_from: 'off'
  
      # Set a domain part for the generation of an envelope-from address.
      # maildomain: [domain]
      maildomain: 'yourdomain.tld'
  
      # Set the condition(s) under which the mail system should send DSN (Delivery
      # Status Notification) messages. The argument ‘off’ disables explicit DSN re-
      # quests, which means the mail system decides when to send DSN messages. This
      # is the default. The condition must be ‘never’, to never request notification, or
      # a comma separated list (no spaces!) of one or more of the following: ‘failure’,
      # to request notification on transmission failure, ‘delay’, to be notified of message
      # delays, ‘success’, to be notified of successful transmission. The SMTP server
      # must support the DSN extension.
      # dsn_notify: (off|condition)
      dsn_notify: 'failure'
  
      # This command controls how much of a mail should be returned in DSN (Deliv-
      # ery Status Notification) messages. The argument ‘off’ disables explicit DSN
      # requests, which means the mail system decides how much of a mail it returns
      # in DSN messages. This is the default. The amount must be ‘headers’, to just
      # return the message headers, or ‘full’, to return the full mail. The SMTP server
      # must support the DSN extension.
      # dsn_return: (off|amount)
      dsn_return: 'full'
      
      # This command controls whether to add a From header if the mail does not have
      # one. The default is to add it.
      # add_missing_from_header: [(on|off)]
      add_missing_from_header: 'on'
  
      # This command controls whether to add a Date header if the mail does not have
      # one. The default is to add it.
      # add_missing_date_header: [(on|off)]
      add_missing_date_header: 'on'
      
      # This command controls whether to remove Bcc headers. The default is to
      # remove them. See hundefinedi [Header handling], page hundefinedi.
      # remove_bcc_headers: [(on|off)]
      remove_bcc_headers: 'on'
  
      #
      # LOGGING
      #
      
      # Enable logging to the specified file or syslog logging
      # log: (syslog|file)
      log: 'syslog'
      
      # Enable or disable syslog logging. The facility can be one of ‘LOG_USER’,
      # ‘LOG_MAIL’, ‘LOG_LOCAL0’, . . ., ‘LOG_LOCAL7’. The default is ‘LOG_USER’.
      # Syslog logging is disabled by default.
      # syslog_facility: (on|off|facility)
      syslog_facility: 'LOG_MAIL'
  
      # Enable logging to the specified file. An empty argument disables logging.
      logfile: '/path/to/log/file'
  
      #
      # ALIASES
      #
      
      # Replace local recipients with addresses in the aliases file. The aliases file is a
      # plain text file containing mappings between a local address and a list of domain
      # addresses. A local address is defined as one without an ’@’ character and a
      # domain address is one with an ’@’ character. The mappings are of the form:
      # local: someone@example.com, person@domain.example
      # Multiple domain addresses are separated with commas.
      #
      # The local address ‘default’ has special significance and is matched if the local
      # address is not found in the aliases file. If no ‘default’ alias is found, then the
      # local address is left as is.
      
      # An empty argument to the aliases command disables the replacement of local
      # addresses. This is the default.
      
      aliases:
        - user: 'default'
          emails: 'root@yourdomain.tld'

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - Akman.msmtp

*Inside vars/main.yml*:

    msmtp_accounts:
      - name: 'default'
        host: 'smtp.yandex.ru'
        port: '465'
        domain: 'yourdomain.tld'
        auth: 'on'
        user: 'user@yourdomain.tld'
        password: 'supersecretpassword'
        tls: 'on'
        tls_starttls: 'off'
        tls_trust_file: '/etc/ssl/certs/ca-certificates.crt'
        from: 'noreply@yourdomain.tld'
        log: 'syslog'
        syslog_facility: 'LOG_MAIL'
        aliases:
          - user: 'default'
            emails: 'root@yourdomain.tld'

## License

MIT / BSD

## Author Information

This role was created in 2017 by Alexander Kapitman
