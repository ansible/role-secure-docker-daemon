Secure Docker Daemon
====================

Use to generate the key files and certificates needed to secure the Docker daemon. Certificates
and keys are created on the target host, which will typically be the Docker daemon host.  If you
plan on connecting to the Docker daemon from a remote host, add a play in your playbook that 
uses the copy module to copy the client files to the remote host. 

Requirements
------------

The following packages should already be installed on the target host: 

- openssl 


Role Variables
--------------

dds_system_tmp
> Path to temporary file space. Defaults to '/tmp'.

dds_country
> Two character country abbreviation. Used in the server CSR. Defaults to 'US'. 

dds_state
> State or provence name. Used in the server CSR. Defaults to 'North Carolina'.

dds_locality
> City name. Used in the server CSR. Defaults to 'Durham'. 

dds_organization
> Organization or company name. Used in the server CSR. Defaults to 'Acme Corp'.

dds_host 
> The host name or IP address used to access the Docker daemon. Defaults to '127.0.0.1'.

dds_passphrase
> A password used to secure key files. Defauts to 'Phrase123!'.

dds_server_cert_path
> Path where server certificates will be created. Defaults to '/etc/docker'.

dds_client_cert_path
> Path where client certificates will be created. Defaults to '~/.docker'.

dds_env_shell_path
> Dest directory for an optional shell script that will set the DOCKER env variables used by
> clients when connecting to the Docker daemon. Defaults to '~' (the user's home directory).

dds_install_shell
> If true, will install a shell script named *docker_env.sh* that sets DOCKER env variables. Source the shell script
> in your .profile or .bashrc to set the variables automatically at login. Defaults to true.  

dds_restart_docker
> Set to true, if the docker daemon should be restarted after create the certificates. Defaults to true.

Example Playbook
----------------

Here's an example playbook that executes our role:

    - name: Secure the docker daemon
      hosts: localhost
      connection: local
      gather_facts: no
      become: yes
      roles:
        - role: ansible.secure-docker-daemon
          dds_host: 10.0.2.15
          dds_server_cert_path: /etc/default/docker
          dds_restart_docker: no

License
-------

MIT

Authors
-------

[@chouseknecht](https://github.com/chouseknecht)

