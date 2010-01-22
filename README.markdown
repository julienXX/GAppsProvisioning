# Provisioning API v2.0 Ruby client library

Provisioning API v2.0 Ruby client library for Google Apps. Based on GData API v2.0.

running even behind authenticated http proxies
using REXML (no extra module dependency)

[On-line documentation](http://www.iut-rodez.fr/gappsprovisioning/doc/)

Authors :	Jérôme Bousquié, Roberto Cerigato  
Ruby version :	from 1.8.6  
Licence :	Apache Licence, version 2  


### Usage :

     #!/usr/bin/ruby
     require 'gappsprovisioning/provisioningapi'
     include GAppsProvisioning
     adminuser = "root@mydomain.com"
     password  = "PaSsWo4d!"
     myapps = ProvisioningApi.new(adminuser,password)

     new_user = myapps.create_user("jsmith", "john", "smith", "secret", nil, "2048")
     puts new_user.family_name
     puts new_user.given_name

Want to update a user ?

     user = myapps.retrieve_user('jsmith')
     user_updated = myapps.update_user(user.username, user.given_name, user.family_name, nil, nil, "true")

Want to add an alias or nickname ?

     new_nickname = myapps.create_nickname("jsmith", "john.smith")

### NEW!!!

Want to manage groups ? (i.e. mailing lists)

     new_group = myapps.create_group("sales-dep", ['Sales Departement'])
     new_member = myapps.add_member_to_group("jsmith", "sales-dep")
     new_owner = myapps.add_owner_to_group("jsmith", "sales-dep")
     #     (ATTENTION: a owner is added only if it's already member of the group!)

Want to handle errors ?

     begin
             user = myapps.retrieve_user('noone')
             puts "givenName : "+user.given_name, "familyName : "+user.family_name, "username : "+user.username"
             puts "admin ? : "+user.admin
     rescue GDataError => e
             puts "errorcode = " +e.code, "input : "+e.input, "reason : "+e.reason
     end

Email lists ? (deprecated)

     new_list = myapps.create_email_list("sales-dep")
     new_address = myapps.add_address_to_email_list("sales-dep", "bibi@ruby-forge.org")
     
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
