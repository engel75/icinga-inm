Description
===========

Shell script to allow Icinga/Nagios notification with delay at night time.

Requirements
============

OS
--
* bash
* atd
* awk

Icinga/Nagios
-------------
* macros disabled  (enable_environment_macros=0)
* mk_livestatus
* all services and hosts need custom macro:
 _INM 0
* all contacts need a pager number
* a contact can have the following custom macros:
 _INMOKS <some sender name> (name of the SMS sender if notification type is OK)
 _INMPRS <some sender name> (name of the SMS sender if notification type is PROBLEM)
 _INMASB <some number> (Admin sleep buffer time in minutes)
 _INMAWT <some number> (Admin awake time, eg. 730 would be 07:30 am)

SMS server
----------
* Kannel


Configuration
==============

* SMS server configuratuion is stored in ./sms.config
* Please edit default settings on top of the script
* The Icinga command would look like this (host and service):


     define command{
        command_name    notify-inm
        command_line    \
                ICINGA__CONTACTINMASB='$_CONTACTINMASB$' \
                ICINGA__CONTACTINMAWT='$_CONTACTINMAWT$' \
                ICINGA__CONTACTINMOKS='$_CONTACTINMOKS$' \
                ICINGA__CONTACTINMPRS='$_CONTACTINMPRS$' \
                ICINGA_CONTACTNAME='$CONTACTNAME$' \
                ICINGA_CONTACTPAGER='$CONTACTPAGER$' \
                ICINGA_HOSTADDRESS='$HOSTADDRESS$' \
                ICINGA_HOSTNAME='$HOSTNAME$' \
                ICINGA_HOSTNOTIFICATIONID='$HOSTNOTIFICATIONID$' \
                ICINGA_HOSTOUTPUT='$HOSTOUTPUT$' \
                ICINGA_HOSTSTATE='$HOSTSTATE$' \
                ICINGA_NOTIFICATIONCOMMENT='$NOTIFICATIONCOMMENT$' \
                ICINGA_NOTIFICATIONTYPE='$NOTIFICATIONTYPE$' \
                ICINGA_SERVICECHECKCOMMAND='$SERVICECHECKCOMMAND$' \
                ICINGA_SERVICEDESC='$SERVICEDESC$' \
                ICINGA_SERVICENOTIFICATIONID='$SERVICENOTIFICATIONID$' \
                ICINGA_SERVICEOUTPUT='$SERVICEOUTPUT$' \
                ICINGA_SERVICESTATE='$SERVICESTATE$' \
                ICINGA_SERVICESTATEID='$SERVICESTATEID$' \
                ICINGA_SHORTDATETIME='$SHORTDATETIME$' \
                ICINGA_TOTALHOSTSDOWNUNHANDLED='$TOTALHOSTSDOWNUNHANDLED$' \
                ICINGA_TOTALSERVICESCRITICALUNHANDLED='$TOTALSERVICESCRITICALUNHANDLED$' \
                /data/icinga/etc/scripts/inm
      }

* A contact would look like this:

      define contact {
	contact_name                     unix-fen
	use                              unix-contact
	host_notifications_enabled       1
        service_notifications_enabled    1
	alias                            Florian Engelmann
	email                            florian.engelmann@somecompany.some
	pager                            076xxxxx61
	_INMOKS                          ewok
	_INMPRS                          ewalarm
	_INMASB                          10
	_INMAWT                          700
        service_notification_options     c,r
        host_notification_options        d,u,r
	host_notification_commands       notify-inm
	service_notification_commands    notify-inm
      }



License and Author
==================

Author:: Florian Engelmann (<engelmann@d-g-c.de>)

Copyright:: 2013 

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
