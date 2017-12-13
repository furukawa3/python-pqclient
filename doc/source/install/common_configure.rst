2. Edit the ``/etc/pqclient/pqclient.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://pqclient:PQCLIENT_DBPASS@controller/pqclient
