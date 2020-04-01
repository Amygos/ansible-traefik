Ansible Role: Traefik
=========

Install and manage Traefik

Role Variables
--------------

| Name 					| Default Value 			| Description 					|
|---------------------------------------|---------------------------------------|-----------------------------------------------|
| `traefik_version`			| 2.0.6					| Traefik version				|
| `traefik_config_dir`			| /etc/traefik				| Traefik configuration directory		|
| `traefik_user`			| "traefik"				| Traefik user					|
| `traefik_group`			| "traefik"				| Traefik group					|
| `traefik_watchdog_sec`		| 0					| Systemd watchdog timeout for traefik service 	|
| `traefik_static_configuration`	| entryPoints.http.address: 80`		| Traefik static configuration			|
| `traefik_configuration_provider_file`	| {}					| Traefik dynamic file configuration section	|
| `traefik_configuration_provider_files`| {}					| Traefik dynamic files configuration section	|

Example Playbook
----------------

Simple reverse proxy configuration, with file as dynamic configuration provider:

    - hosts: servers
      roles:
         - role: amygos.traefik
	   vars:
	     traefik_static_configuration:
               entryPoints:
                 http:
                   address: :
               providers:
                 file:
                   filename: /etc/traefik/traefik.yml
             traefik_configuration_provider_file:
               http:
                 routers:
                    endpoint_service:
                      rule: PathPrefix(`/`)
                 services:
                   backend_service:
                     loadBalancer:
                       servers:
                       - url: http://127.0.0.1:8080



License
-------

MIT
