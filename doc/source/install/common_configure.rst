2. Edit the ``/etc/openstack-publiccloud-wg/openstack-publiccloud-wg.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://openstack-publiccloud-wg:OPENSTACK-PUBLICCLOUD-WG_DBPASS@controller/openstack-publiccloud-wg
