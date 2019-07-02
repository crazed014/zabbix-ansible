### zabbix ansible playbook

This playbook runs Zabbix in Docker using a self-signed SSL certificate

### Installation:

1. Install the Ansible roles that are dependencies for the playbook to run:

This is on the docker container running awx. -- remember this

You can use `docker exec -it awx_tasks bash` to get a terminal on it.

Then you git clone the repo down. 

Then run:

`ansible-galaxy install -r requirements.yml`


2. Edit the variables in `inventory` to reflect the values appropriate for your install.


3. Edit the Nginx config in `./files/nginx.conf` as needed.

_Note: It would be recommended to only change the configuration under the server directive in the config. Also, the playbook creates a self-signed SSL certificate and key and mounts them at /tmp/server. Don't change the values for the paths to the keys unless you modify the actual Ansible playbook._

4. Run the playbook:

`ansible-playbook -i inventory zabbix.yml`

### Post-install:

Access the web interface for Zabbix on the SSL port of the remote server that was set in the inventory.

### Additional information:

You can replace the cert in `/opt/zabbix-docker/` on the remote server as needed with a valid certificate on the remote server and then re-run the playbook to re-initialize the Nginx docker container using the new SSL cert.
