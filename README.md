ANSIBLE-CMDBUILD 3.2

Centos 7 / RedHat

CMDBuild 3.2 installation playbook
Please refer CMDBuild Technical Manual for details of installation process.
https://www.cmdbuild.org/file/manuali/technical-manual-in-english
This playbook intend to use for evaluation or development use.
DO NOT USE FOR PRODUCTION ENVIRONMENT!!

Prerequisist: Ansible >2.0 installed system
Target system:
 CentOS/RHEL 7 64bit minimal installed
 8GB RAM and 100GB storage available are recommended
Login as ansible or other user what you set is host file
Basic configurations can be edited in "hosts.yml" file.

Usage:
1. Copy all files to Ansible executable directory and optionally download CMDBuild or Ready2use source (war) into "files" folder.
2. Edit "hosts.yml" file and replace "cmdbuild_hostname" to your target hostname or IP address
3. Invoke command;

**Vars: group_vars/cmdbuild.yml**  
*download_war: false*   ( If you have downloaded war file, set this option. )
*offline_source: files/ready2use-2.0-3.2.war*  ( Offline war file and path )
*db_type: empty*      ( Production or demo data set.  empty | demo )


```
ansible-playbook -i hosts.yml site.yml --ask-pass 
```

4. Playbook is Installing;
- Oracle JDK 11
- Postgres 10
- PostGIS 2.4-10
- Tomcat 9.0.31
- CMDBuild 3.2 / Ready2Use 2.0 - 3.2

5. After completed playbook, 
Check Tomcat logs to find "Server startup in XXXXXX ms"
```
tail -f /opt/tomcat/logs/catalina.out
```

6. Access from your browser
http://TARGET IP:8080/cmdbuild
to start GUI installation for CMDBuild.

7. On GUI setup,
CMDBuild database name: cmdbuild
Create Shark schima: yes
Postgres Host: localhost
Postgres port: 5432
Postgres user: postgres
Password: postgres
Login user: admin
Login password: admin

8. if you have something wrong, 
check /opt/tomcat/logs/catalina.out, cmdbuild.log
then restart tomcat.
```
# systemctl restart tomcat
```
Enjoy CMDBuild!

