ROLE ICINGA2\_MASTER
====================

[![image](https://img.shields.io/github/license/adfinis-sygroup/ansible-role-icinga2_master.svg?style=flat-square)](https://github.com/adfinis-sygroup/ansible-role-icinga2_master/blob/master/LICENSE)

[![image](https://img.shields.io/travis/com/adfinis-sygroup/ansible-role-icinga2_master.svg?style=flat-square)](https://travis-ci.com/adfinis-sygroup/ansible-role-icinga2_master)

[![image](https://img.shields.io/badge/galaxy-adfinis--sygroup.icinga2_master-660198.svg?style=flat-square)](https://galaxy.ansible.com/adfinis-sygroup/icinga2_master)

This role configures icinga2 to act as a master. Furthermore, this role
takes care of the configuration for all clients.

Requirements
------------

When icinga2\_master\_ido\_enabled is turned on the role tries to
activate the [IDO
feature](https://icinga.com/docs/icinga2/latest/doc/14-features/#db-ido)
for icinga2. This needs a running database, either already existing or
using the
[adfinis-sygroup.mariadb](https://galaxy.ansible.com/adfinis-sygroup/mariadb)
role. Note: When using a multi-master setup, only one database must be
used for both instances!

Role Variables
--------------

``` {.sourceCode .yaml}
# The icinga2 master zone
icinga2_master_master_zone: monitoring-master

# A list of all icinga2 api users
icinga2_master_api_users: []
#  - username: root
#    password: 'passw0rd'
#    permissions: '*'
#  - username: token-generator
#    password: 'passw0rd'
#    permissions: 'actions/generate-ticket'
```

Templates can be adjusted using variables.

``` {.sourceCode .yaml}
## Template settings

# If you have own templates for the configuration files in /etc/icinga2/conf.d
# consider adjusting the names here and add your template to
# templates/etc/icinga2/conf.d in the root of your playbook folder.
icinga2_master_template_confd_notifications: "notifications.conf"
icinga2_master_template_confd_templates: "templates.conf"
icinga2_master_template_confd_commands: "commands.conf"
icinga2_master_template_confd_groups: "groups.conf"
icinga2_master_template_confd_timeperiods: "timeperiods.conf"
icinga2_master_template_confd_users: "users.conf"

# These variables can be adjusted if you have custom templates for the global
# templates directory which gets synced to all clients.
icinga2_master_tempalte_globaltemplates_services: "services.conf"
icinga2_master_tempalte_globaltemplates_templates: "templates.conf"
```

If you want to use [Twilio](https://www.twilio.com) for the alerting,
you can create an account. After that, you can receive an Application
SID and Auth token from the twilio console. If you plan to make phone
calls, please create a [TwiML](https://www.twilio.com/docs/voice/twiml)
application.

``` {.sourceCode .yaml}
## Twilio alerting

# The account sid from https://www.twilio.com/console
#icinga2_master_twilio_account_sid: 'account_sid'

# The auth token from https://www.twilio.com/console
#icinga2_master_twilio_auth_token: 'auth_token'

# Whether twilio sms are enabled or not
icinga2_master_twilio_sms_enabled: False

# The twilio phone numer used to send sms
#icinga2_master_twilio_sms_from: '+41123456789'

# Whether twilio calls are enabled or not
icinga2_master_twilio_phone_enabled: False

# The twilio phone number used to make calls
#icinga2_master_twilio_phone_from: '+41123456789'

# The twilio application sid on how to handle the call
# https://www.twilio.com/docs/voice/make-calls
#icinga2_master_twilio_phone_application_sid: 'application_sid'
```

Dependencies
------------

This role depends on the role
[adfinis-sygroup.icinga2\_agent](https://galaxy.ansible.com/adfinis-sygroup/icinga2_agent),
which installs the icinga2 binary.

Example Playbook
----------------

``` {.sourceCode .yaml}
- hosts: monitoring-master
  roles:
     - { role: adfinis-sygroup.icinga2_agent }
     - { role: adfinis-sygroup.icinga2_master }
```

License
-------

[GPL-3.0](https://github.com/adfinis-sygroup/ansible-role-icinga2_master/blob/master/LICENSE)

Author Information
------------------

icinga2\_master role was written by:

-   Adfinis SyGroup AG \| [Website](https://www.adfinis-sygroup.ch/) \|
    [Twitter](https://twitter.com/adfinissygroup) \|
    [GitHub](https://github.com/adfinis-sygroup)
