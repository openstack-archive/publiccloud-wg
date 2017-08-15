Prerequisites
-------------

Before you install and configure the openstack-publiccloud-wg service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``openstack-publiccloud-wg`` database:

     .. code-block:: none

        CREATE DATABASE openstack-publiccloud-wg;

   * Grant proper access to the ``openstack-publiccloud-wg`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON openstack-publiccloud-wg.* TO 'openstack-publiccloud-wg'@'localhost' \
          IDENTIFIED BY 'OPENSTACK-PUBLICCLOUD-WG_DBPASS';
        GRANT ALL PRIVILEGES ON openstack-publiccloud-wg.* TO 'openstack-publiccloud-wg'@'%' \
          IDENTIFIED BY 'OPENSTACK-PUBLICCLOUD-WG_DBPASS';

     Replace ``OPENSTACK-PUBLICCLOUD-WG_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``openstack-publiccloud-wg`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt openstack-publiccloud-wg

   * Add the ``admin`` role to the ``openstack-publiccloud-wg`` user:

     .. code-block:: console

        $ openstack role add --project service --user openstack-publiccloud-wg admin

   * Create the openstack-publiccloud-wg service entities:

     .. code-block:: console

        $ openstack service create --name openstack-publiccloud-wg --description "openstack-publiccloud-wg" openstack-publiccloud-wg

#. Create the openstack-publiccloud-wg service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        openstack-publiccloud-wg public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        openstack-publiccloud-wg internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        openstack-publiccloud-wg admin http://controller:XXXX/vY/%\(tenant_id\)s
