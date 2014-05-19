Ansible playbook for a Drupal Cluster
=================================
- Requires [Ansible](http://docs.ansible.com/) 1.5
- Expects Debian Wheezy

This playbook configures a Drupal cluster. Hosts are configured in the
'hosts' file, grouped by purpose.

- [lbservers] for load balancers
- [webservers] for application servers
- [dbservers] for database servers

### Checking cluster configuration

    ansible-playbook site.yml --check

### Applying changes to the cluster

    ansible-playbook site.yml


### Ad-hoc operations on the cluster

    ansible -i hosts -a "apt-get install -y -q mc" webservers

Troubleshooting
---------------

### Switch MySQL master if db01 fails

Login to db02 and issue

    # echo "STOP SLAVE; RESET MASTER;" | mysql

Then. edit 'settings.php' to point the database to db02

### Nice to have

- automatic load balancer failover
- automatic mysql failover
- Drupal master/slave configuration with autoslave module
