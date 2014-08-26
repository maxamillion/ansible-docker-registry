docker-registry
=========

Deploy and configure a [docker-registry](https://github.com/docker/docker-registry)

Requirements
------------

If this is being used to deploy on RHEL/CentOS (or a derivative distro such as Scientific Linux, Amazon Linux, etc) then EPEL is required. There are many ansible roles to satisfy this, two recommendations are: goozbach.EPEL or Rackspace_Automation.epel 

NOTE: bennojoy.redis installs EPEL for EL6 and is a dependency, at this time that requirement is deferred.

If this is being used to deploy on Fedora, no requirements necessary. All needed packages are in the Fedora repositories.

Role Variables
--------------

    # Docker Registry profile:
    #   Available Options:
    #     -
    docker_registry_profile: dev

    # Docker Registry Storage path:
    #   Depends on storage profile
    docker_registry_storage_path: /var/lib/docker-registry

    # Docker Registry bind address:
    #   What address to bind to and listen on
    docker_registry_bind_address: 0.0.0.0

    # Docker Registry bind port:
    #   What port to bind to and listen on
    docker_registry_bind_port: 5000


    # Docker Registry gunicorn workers:
    #   Number of gunicorn workers to spawn
    #
    #   For more information and recommendations:
    #     http://gunicorn.org/#docs
    #
    docker_registry_gunicorn_workers: 8

    # Docker Registry log level
    #   default: info
    #
    #   `loglevel`: string, level of debugging. Any of python's
    #      [logging](http://docs.python.org/2/library/logging.html) module levels:
    #         `debug`, `info`, `warn`, `error` or `critical`
    docker_registry_loglevel: info


    # Docker Registry AWS S3 specific items
    #   These only need to be populated in the event you are using AWS S3
    #     https://aws.amazon.com/s3/
    docker_registry_s3_region: REPLACEME
    docker_registry_s3_bucket: REPLACEME
    docker_registry_s3_encrypt: true
    docker_registry_s3_secure: true
    docker_registry_s3_access_key: REPLACEME
    docker_registry_s3_secret_key: REPLACEME

    # Docker Registry Google Cloud Storage specific items
    #   These only need to be populated in the event you are using GCS
    # Google Cloud Storage Configuration
    # See:
    #   https://developers.google.com/storage/docs/reference/v1/getting-startedv1#keys
    # for details on access and secret keys.
    docker_registry_gcs_bucket: REPLACEME
    docker_registry_gcs_secure: true
    docker_registry_gcs_access_key: REPLACEME
    docker_registry_gcs_secret_key: REPLACEME
    docker_registry_gcs_oauth2: false

    # Docker Registry OpenStack Swift
    # These only need to be populated if you are using one of the following:
    #   - swift
    #   - glance-swift
    #   - openstack-swift
    #
    # For more information:
    #   http://docs.openstack.org/developer/swift/
    docker_registry_os_auth_url: REPLACEME
    docker_registry_os_container: REPLACEME
    docker_registry_os_username: REPLACEME
    docker_registry_os_password: REPLACEME
    docker_registry_os_tenant_name: REPLACEME
    docker_registry_os_region_name: REPLACEME

    # Docker Registry Elliptics configuration
    # These only need to be populated if you are using elliptics storage
    # For more information:
    #   http://reverbrain.com/elliptics/
    docker_registry_elliptics_nodes: REPLACEME
    docker_registry_elliptics_wait_timeout: 60
    docker_registry_elliptics_check_timeout: 60
    docker_registry_elliptics_io_thread_num: 2
    docker_registry_elliptics_net_thread_num: 2
    docker_registry_elliptics_nonblocking_io_thread_num: 2
    docker_registry_elliptics_groups: REPLACEME
    docker_registry_elliptics_verbosity: 4
    docker_registry_elliptics_logfile: /dev/stderr
    docker_registry_elliptics_addr_family: 2


Dependencies
------------

Fedora:
    - None

RHEL/CentOS:
    - EPEL: This is pulled in by bennojoy.redis

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: docker-registry-servers
      roles:
         - { role: maxamillion.docker-registry, 
                docker_registry_profile: local,
                docker_registry_storage_path: /srv/docker-registry }

License
-------

Apache v2.0

Author Information
------------------

Adam Miller <maxamillion@fedoraproject.org>
