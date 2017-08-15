2. Edit the ``/etc/PublicCloudWG/PublicCloudWG.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://PublicCloudWG:PUBLICCLOUDWG_DBPASS@controller/PublicCloudWG
