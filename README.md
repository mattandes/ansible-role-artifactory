Ansible Role: Artifactory
=========

[![Build Status](https://travis-ci.org/mattandes/ansible-role-artifactory.svg?branch=master)](https://travis-ci.org/mattandes/ansible-role-artifactory)

This role will install Artifactory via Docker and a docker-compose file.

Requirements
------------

Role requires `docker` and `docker-compose` python modules to be installed on the target machine.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    artifactory_data_dir: /data

Base directory on the target server that will be used to store persistent data for each of the containers.

    artifactory_docker_compose_template: docker-compose.yml.j2

Template file used to generate the docker-compose file that will be used to deploy Artifactory

    artifactory_docker_registry: docker.bintray.io

The Docker registry where the Docker images are stored

    artifactory_postgres_image: postgres

The name of the Postgres database container image.

    artifactory_postgres_image_tag: "9.5.2"

The image tag of the Postgres database container image to use.

    artifactory_postgres_db_user: artifactory

The Postgres database user.

    artifactory_postgres_db_password: artifactory

The password for the Postgres database user.

    artifactory_type: oss

The Artifactory version to run. Either `oss` or `pro`

    artifactory_image: "jfrog/artifactory-{{ artifactory_type | lower }}"

The name of the Artifactory container image.

    artifactory_image_tag: "6.5.9"

The image tag of the Artifactory container image to use.

    artifactory_nginx_image: jfrog/nginx-artifactory-pro

The name of the NGINX container image.

    artifactory_nginx_image_tag: "6.5.9"

The image tag of the NGINX container to use.

Dependencies
------------

Role requires Docker to be installed on the target system. This can be installed via the `geerlingguy/docker` role.

Example Playbook
----------------

    ---
    - hosts:
        - artifactory
      become: true
      roles:
        - role: geerlingguy.docker
          docker_install_compose: false
        - role: geerlingguy.repo-epel
        - role: geerlingguy.pip
          pip_install_packages:
            - name: docker
            - name: docker-compose
        - role: mattandes.artifactory

License
-------

MIT
