Terraform
---------

Requirements
~~~~~~~~~~~~

Role Access
^^^^^^^^^^^

* In order to see the Terraform Blueprint type option and create Terraform App Blueprints in `Provisioning -> Blueprints`, the Conduit user must have Role permissions for `Provisioning: Blueprints - Terraform` set to `Full`.

* In order to provision Terraform Apps in `Provisioning -> Apps`, the Conduit user must have Role permissions for `Provisioning: Blueprints - Terraform` set to `Provision` or `Full`.

* Existing Terraform Blueprints must be added before they can be provisioned from `Provisioning -> Apps`.

Github/Git Repo
^^^^^^^^^^^^^^^

* To use .tf files from a Git repo a Git or Github integration needs to be configured in `Administration - Integrations`. If one is not configured .tf or .tf.json files can be manually added to Terraform App Blueprints.

Supported App Provisioning Targets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* VMware
* AWS
* Oracle Cloud

.. NOTE::  Additional clouds will be available in later releases.


Terraform Installation
^^^^^^^^^^^^^^^^^^^^^^

|conduit| will automatically install Terraform locally upon the first Terraform App provision. It is possible on some operating system configurations for the automated terraform installation to fail, in which case it can be manually installed (run ``terraform --version`` to verify).

To manually install and configure terraform on the Conduit Appliance:

#. Run the following curl on the |conduit| Appliance to install Terraform:

   .. code-block:: bash

    curl -k -s "https://applianceServerUrl/api/server-script/terraform-install?local=true" | bash


   .. NOTE:: Replace applianceServerUrl with your |conduit| appliance url or ip.

#. Create a working directory for Terraform, and change owner to ``conduit-app``.

   .. code-block:: bash

    sudo mkdir /var/opt/conduit/conduit-ui/terraform

    sudo chown conduit-app.conduit-app /var/opt/conduit/conduit-ui/terraform

   The default location is ``/var/opt/conduit/conduit-ui/terraform`` but can be changed.

#. Add the Terraform working path to ``/opt/conduit/conf/application.yml``

   .. code-block:: bash

    sudo vi /opt/conduit/conf/application.yml

   Add the following to the application.yml config below and in-line with the repo section:

   .. code-block:: bash

    terraform:
        location: '/var/opt/conduit/conduit-ui/terraform'

   Example application.yml config with Terraform location added:

   .. code-block:: bash

    repo:
        git:
            location: '/var/opt/conduit/conduit-ui/repo/git'
        local:
            location: '/var/opt/conduit/conduit-ui/repo/local'
    terraform:
        location: '/var/opt/conduit/conduit-ui/terraform'
    bitcan:
        backup:
            destination:
                root: '/var/opt/conduit/bitcan/backup'
                working: '/var/opt/conduit/bitcan/working'

   .. IMPORTANT:: Uses spaces not tabs to indent or ui startup will fail. If you used a different path than the default location, enter that path instead.

#. Restart the conduit-ui to apply the ``application.yml`` config.

   .. code-block:: bash

    sudo conduit-ctl restart conduit-ui


Terraform is now installed and configured, and Terraform apps can be provisioned from Conduit.


Creating Terraform App Blueprints
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to provision Terraform apps, Terraform App Blueprints must be created first.

.. IMPORTANT:: In |conduit| versions 3.3.0 and 3.3.1 VMware cloud types are supported for Terraform App provisioning targets. Additional clouds will be available in later releases.

#. Navigate to `Provisioning -> Blueprints`
#. Select :guilabel:`+ ADD`
#. Name the Blueprint and select `Terraform` type.

   .. NOTE:: In order to see the Terraform Blueprint type option, the |conduit| user must have Role permissions for `Provisioning: Blueprints - Terraform` set to `Full`.

#. Select :guilabel:`NEXT`
#. Configure the following:

   NAME
       Name of the
   DESCRIPTION
       Description for you App Blueprints shown in the Apps list (optional)
   CATEGORY
       App Category (optional)
   IMAGE
    Add reference image/picture for your App Blueprint (optional)
   CONFIG TYPE (select Terraform, Terraform.json, or Git Repository)
    Terraform (.tf)
     CONFIG
      Paste in the .tf contents in the config section. Variables will be presented as input fields during App provisioning, or auto-populated with matching values if contained in a selected TFVAR Secret file added to the Cypher service.
    Terraform JSON (.tf.json)
      Paste in .tf.json contents in the config section. Variables will be presented as input fields during App provisioning, or auto-populated with matching values if contained in a selected TFVAR Secret file added to the Cypher service.
    Git Repository
      SCM Integration
        Select a Github SCM integration that has been added in `Administration - Integrations`. If using a Git Repository integration from `Administration - Integrations` this filed can be skipped.
      Repository
        Select repository from selected SCM integration, or Git Repository integration from `Administration - Integrations` if no SCM/Github Integration is selected.
      BRANCH OR TAG
        i.e. master (default)
      WORKING PATH
        Enter the repo path for the .tf files (s). ``./`` is default.
      CONFIG
        .tf files found in the working path will populate in the CONFIG section.

        .. NOTE:: If no files are found please ensure your Github or Git integration is configured properly (Private repos need to have a key pair added to |conduit|, the keypair selected on the integration in |conduit|, and the keypair's public key added to the GitHub users SSH keys in github or to the git repo).
   TFVAR SECRET
    Select a tfvars secret for .tf variables. Tfvars secrets can be added in `Services -> Cypher` using the tfvars/name mountpoint. This allows sensitive data and passwords to be encrypted and securely used with Terraform Blueprints.
   OPTIONS
    example ``-var 'instanceName=sampleTfApp'``

#. Select :guilabel:`SAVE`

Your Terraform App is ready to be provisioned from `Provisioning -> Apps`.

Provisioning Terraform Apps
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. NOTE:: An existing Terraform App Blueprints must be added to `Provisioning -> Blueprints` before it can be provisioned.

.. NOTE:: In order to provision Terraform Apps in `Provisioning -> Apps`, the Conduit user must have Role permissions for `Provisioning: Blueprints - Terraform` set to `Provision` or `Full`.

#. Navigate to `Provisioning -> Apps`
#. Select :guilabel:`+ ADD`
#. Choose and existing Terraform App Blueprint
#. Select :guilabel:`NEXT`
#. Enter a NAME for the App and select the Group, Default Cloud and Environment (optional)
#. Select :guilabel:`NEXT`
#. Populate any required variables in the `Terraform Variables` section.
   ..TIP:: If the tf CONFIG data needs to be edited, select the `RAW` section, edit, and then select the `BUILDER` section again. The CONFIG changes from the RAW edit will be updated in the CONFIG section.
#. Select :guilabel:`COMPLETE`

The Terraform App will begin to provision.

Once provisioning is completed, note the TERRAFORM tab in the App details page (`Provisioning -> Apps` -> select the App). This section contains State and Plan output:

.. image:: /images/apps/terraform/terraform_sample.png
