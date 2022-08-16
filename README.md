OpenLDAP Ansible role for install, create, delete, search users
===============================================================

# openldap_users should be an array of user objects with 3 properties: firstName, lastName and passwordHash
#
# At this point the role only supports SHA512 encryption and the passwordhash can be obtained using bash:
#  echo -n 'your_password' | openssl dgst -sha512 -binary | openssl enc -base64
#
#  for instance, for a username john.doe with password 'my_password' you would need

ansible-playbook openldap.yml -t create -e "firstName=John" -e "lastName=Doe" -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ=="


# when you need to delete users on a running LDAP instance, you can just add them here and run the role again as
# every run will wipe out all the directory and start again

ansible-playbook openldap.yml -t delete -e "firstName=John" -e "lastName=Doe" 

# when you need list of users on a running LDAP instance, you can do this

ansible-playbook openldap.yml -t search
