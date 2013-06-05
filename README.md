Description
===========

Shell script to allow Icinga/Nagios notification with delay at night time.

Requirements
============

OS:
--
* bash

Icinga/Nagios:
--------------
* macros enabled  (enable_environment_macros=1)
* mk_livestatus
* all services and hosts need custom macro:
 _INM 0
* all contacts need a pager number
* a contact can have the following custom macros:
 _INMOKS <some sender name> (name of the SMS sender if notification type is OK)
 _INMPRS <some sender name> (name of the SMS sender if notification type is PROBLEM)
 _INMASB <some number> (Admin sleep buffer time in minutes)
 _INMAWT <some number> (Admin awake time, eg. 730 would be 07:30 am)

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
