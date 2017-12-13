Prerequisites
-------------

Before you install and configure the python-pqclient service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``pqclient`` database:

     .. code-block:: none

        CREATE DATABASE pqclient;

   * Grant proper access to the ``pqclient`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON pqclient.* TO 'pqclient'@'localhost' \
          IDENTIFIED BY 'PQCLIENT_DBPASS';
        GRANT ALL PRIVILEGES ON pqclient.* TO 'pqclient'@'%' \
          IDENTIFIED BY 'PQCLIENT_DBPASS';

     Replace ``PQCLIENT_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``pqclient`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt pqclient

   * Add the ``admin`` role to the ``pqclient`` user:

     .. code-block:: console

        $ openstack role add --project service --user pqclient admin

   * Create the pqclient service entities:

     .. code-block:: console

        $ openstack service create --name pqclient --description "python-pqclient" python-pqclient

#. Create the python-pqclient service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        python-pqclient public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        python-pqclient internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        python-pqclient admin http://controller:XXXX/vY/%\(tenant_id\)s
