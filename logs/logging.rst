Logs
====

Overview
--------

The logging architecture backing |conduit| uses the latest and greatest technologies and standards to be able to service large amounts of log traffic as well as facilitate easy viewing. Utilizing elasticsearch behind the scenes and buffered log transmission protocols |conduit| provides a highly efficient and highly scalable solution for capturing log data from anything provisioned via the system. By utilizing common formats (syslog) it is also very easy to forward logs to external third party log services.

Configuration
^^^^^^^^^^^^^

Logging configuration can be setup in the ``Admin -> Logs`` section. There are a couple useful settings here including customizing the retainment policy (by default 7 days). This could be expanded to years for PCI Compliance purposes or other potential requirements an organization might have.

.. NOTE:: When increasing the retainment policy of the logging system it may be necessary to scale out the elasticsearch cluster. Please refer to the relevant information with regards to scaling elasticsearch and advanced installation options for externalizing the elasticsearch cluster.

This area of administration also provides options for setting custom syslog forward rules. These rules are applied on each individual host therefore keeping the |conduit| appliance itself out of the data plane. For information on different syslog formatting rules please refer to the http://www.rsyslog.com/sending-messages-to-a-remote-syslog-server/[rsyslog] documentation.

Usage
^^^^^^^^
|conduit| automatically sets up and configures logging for all of the standard catalog items provisioned through conduit. This includes both Docker containers as well as virtual machines. Simple view instance specific logs in instance detail via the "Logs" tab.

There are several filtering capabilities built into the logging ui with more being added continually. Easily toggle log level filters from the dropdown or change the date range filter using the handy date filter component. A chart is also displayed above logs representing the log counts by level over the selected time range (default last 24 hours). A handy pattern search is also available with some rather capable features based on Lucene search syntax.

.. TIP:: It may be useful to review the Lucene search query syntax for powerful use cases: https://lucene.apache.org/core/2_9_4/queryparsersyntax.html[Syntax Guide]

There are several other places logs can be viewed. Not only can they be viewed across an application in app detail but also across all instances in the account. The main level ``Logs`` section provides an ability to query all logs produced by the system. It is also possible to view host specific logs on a docker host by viewing the host detail page via ``Infrastructure``.

.. NOTE:: New features are on the roadmap for the main logs section including saved searches, and handy charting dashboards for garnering insights out of log data.

Integrations
-------------

While the built in logging solution provided by |conduit| is sufficient for most, there are some scenarios in which a more advanced logging system may be desired or already in place. To facilitate this |conduit| makes it easy to add custom syslog rules as well as built in direct integrations with Splunk and LogRhythm. All integrations pertaining to logging can be configured in the ``Administration -> Logging`` section.

Splunk
^^^^^^^^^

To configure Splunk simply create a syslog listener configuration in Splunk. Then it is simply a matter of expanding the section in Logging settings pertaining to Splunk and filling out the host and port of the appender. Once saved, all hosts managed by |conduit| will be configured to forward logs to the target Splunk listener.

LogRhythm
^^^^^^^^^^^^

Configuring LogRhythm is much like configuring Splunk. Simply toggle the enabled flag in the LogRhythm section to enabled and fill in the Host, and Port information for the LogRhythm listener.

Exporting Logs
---------------

Log Settings
^^^^^^^^^^^^^
There are three main log areas in |conduit|

* Agent Logs

* |conduit| Server Logs

* Activity / Audit Logs

Agent Logs
-----------

When instances are deployed through |conduit|, the agent that is installed, captures Application logs and sends them back to the |conduit| Server.

While the built-in logging solution provided by |conduit| is sufficient for most, there are some scenarios in which a more advanced logging system may be desired or already in place. To facilitate this |conduit| makes it easy to add custom syslog rules as well as built in direct integrations with Splunk and LogRhythm. All integrations pertaining to logging can be configured in the Administration -> Logging section.

Splunk
^^^^^^

To configure Splunk simply create a syslog listener configuration in Splunk. Then it is simply a matter of expanding the section in Logging settings pertaining to Splunk and filling out the host and port of the appender. Once saved, all hosts managed by |conduit| will be configured to forward logs to the target Splunk listener.

LogRhythm
^^^^^^^^^

Configuring LogRhythm is much like configuring Splunk. Simply toggle the enabled flag in the LogRhythm section to enabled and fill in the Host, and Port information for the LogRhythm listener.

|conduit| Server Logs
----------------------

The main |conduit| server log is in ``/var/log/conduit/conduit-ui`` and the latest log file is named current. This log is archived every 24hrs. There are a number of other log files for the individual infrastructure components as well.

If you wish to export these to an external syslog platform, do the following:

#. Once you have configured your syslog destination (edit rsyslog.conf), create a conduit-syslog.conf file in the ``/etc/rsyslog.d`` directory and add the following entries

   .. code-block:: bash

     module(load="imfile" PollingInterval="50")
     input(type="imfile" File="/var/log/conduit/conduit-ui/current" Tag="conduit-ui" ReadMode="2" Severity="info" StateFile="conduit-ui")
     input(type="imfile" File="/var/log/conduit/check-server/current" Tag="check-server" ReadMode="2" Severity="info")
     input(type="imfile" File="/var/log/conduit/guacd/current" Tag="guacd" ReadMode="2" Severity="info")
     input(type="imfile" File="/var/log/conduit/elasticsearch/current" Tag="elasticsearch" ReadMode="2")
     input(type="imfile" File="/var/log/conduit/mysql/current" Tag="mysql" ReadMode="2" Severity="info")
     input(type="imfile" File="/var/log/conduit/nginx/current" Tag="nginx" ReadMode="2" Severity="info")
     input(type="imfile" File="/var/log/conduit/rabbitmq/current" Tag="rabbitmq" ReadMode="2" Severity="info")
     input(type="imfile" File="/var/log/conduit/redis/current" Tag="redis" ReadMode="2" Severity="info")

#. Restart rsyslog

The logfiles will now be to the destination you have defined.

This configuration is valid for an ‘all-in-one’ |conduit| server. If the infrastructure components are running on separate servers /clusters, you will need to create the relevant redirects for the logs on those boxes.

Activity Log
-------------

The final log type that may require export is the |conduit| Activity log. This tracks system changes made by users, for example create and delete instances etc.

#. To set up CEF/SIEM auditing export, you should edit the following file: ``logback.groovy`` located at ``/opt/conduit/conf/logback.groovy``.

#. Copy the below configuration to the bottom of the logback.groovy configuration file, save and then exit.

   .. code-block:: javascript

     appender("AUDIT", RollingFileAppender) {
       file = "/var/log/conduit/conduit-ui/audit.log"
        rollingPolicy(TimeBasedRollingPolicy) {
          fileNamePattern = "/var/log/conduit/conduit-ui/audit_%d{yyyy-MM-dd}.%i.log"
          timeBasedFileNamingAndTriggeringPolicy(SizeAndTimeBasedFNATP) {
            maxFileSize = "50MB"
          }
          maxHistory = 30
        }
        encoder(PatternLayoutEncoder) {
          pattern = "[%d] [%thread] %-5level %logger{15} - %maskedMsg %n"
        }
      }

      logger("com.conduit.AuditLogService", INFO, ['AUDIT'], false)

#. Once you have done this, you need to restart the |conduit| Application server. To do this, do the following:

   .. code-block:: bash

      conduit-ctl stop conduit-ui

   .. NOTE:: Please be aware this will restart the web interface for |conduit|.

#. Once the service has stopped enter the following at the shell prompt to restart (if the service does not stop, replace stop with graceful-kill and retry)

   .. code-block:: bash

      conduit-ctl start moprheus-ui

#. To know when the UI is up and running you can run the following command

   .. code-block:: bash

      conduit-ctl tail moprheus-ui

Once you see the ASCI art show up you will be able to log back into the User Interface. A new audit file will have been created called audit.log and will found in the default |conduit| log path which is ``/var/log/conduit/conduit-ui/``

Instead of writing the output to a logile, you could create an Appender definition for your SIEM audit database product


conduit-ssl nginx logs
------------------------

.. NOTE:: Conduit does not put a logrotate in for Conduit-ssl access logs

svlogd will only rotate the current file, nginx is setup to write the access logs to separate files and not stdout.

Implementation of a log rotate is left up to up to end users for files outside of the services.  This is done in case end users have a log management solution.


Below is what a suggested configuration looks like for the file ``/etc/logrotate.d/conduit-nginx``:

     .. code-block:: bash

       /var/log/conduit/nginx/conduit*access.log {
               daily
               rotate 14
               compress
               delaycompress
               missingok
               notifempty
               create 644 conduit-app conduit-app
               postrotate
                       [ ! -f /var/run/conduit/nginx/nginx.pid ] || kill -USR1 `cat /var/run/conduit/nginx/nginx.pid`
               endscript
       }
