OpenLDAP Ansible role for install, create, delete, search users
===============================================================

At this point the role only supports SHA512 encryption and the passwordhash can be obtained using bash:
```bash
echo -n 'your_password' | openssl dgst -sha512 -binary | openssl enc -base64
```
for install openldap-server
```bash
ansible-playbook openldap.yml -t install_server
```

for instance, for a username john.doe create with password 'my_password' you would need
```bash
ansible-playbook openldap.yml -t create_user  -e "firstName=John" -e "lastName=Doe" -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ=="
```

when you need to delete users on a running LDAP instance, you can just add them here and run the role again as
every run will wipe out all the directory and start again
```bash
ansible-playbook openldap.yml -t delete_user -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ==" 
```
when you need list of users on a running LDAP instance, you can do this

```bash
ansible-playbook openldap.yml -t search
```

for install openldap-client
```bash
ansible-playbook openldap.yml -t install_client
```

for create group 

```bash
 ansible-playbook openldap.yml -t create_group   -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ=="
```

for add user to group:
1) use search for take uid
2)

```bash
 ansible-playbook openldap.yml -t add_user_to_group  -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ=="
```
delete user from group
1) use search for take uid
2)
```bash
 ansible-playbook openldap.yml -t delete_user_from_group  -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ=="
```

delete group
```bash
 ansible-playbook openldap.yml -t delete_user_from_group  -e "passwordHash={SHA512}3ajDRohg3LJOIoq47kQgjUPrL1/So6U4uvvTnbT/EUyYKaZL0aRxDgwCH4pBNLai+LF+zMh//nnYRZ4t8pT7AQ=="
```