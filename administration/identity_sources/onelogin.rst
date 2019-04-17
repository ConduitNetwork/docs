OneLogin
--------

Adding OneLogin Identity Source Integration

#. Navigate to Administration -> Tenants
#. Select the Tenant to add the Identity Source Integration
#. Select :guilabel:`IDENTITY SOURCES`
#. Select :guilabel:`+ IDENTITY SOURCE`
#. Enter the following:

   TYPE
      OneLogin
   NAME
      Name of the Identity Source Integration in Conduit
    DESCRIPTION
      Optional Description of the Identity Source
    ONELOGIN SUBDOMAIN
      example: conduit-dev
        .. WARNING:: Please verify the subdomain carefully. An invalid subdomain will cause authentication attempts by OneLogin users to fail.
    ONELOGIN REGION
      Speciify US or EU region
    API CLIENT SECRET
      OneLogin API Client Secret from the Settings - API section in OneLogin portal
    API CLIENT ID
      OneLogin API Client ID from the Settings - API section in OneLogin portal
    REQUIRED ROLE
      Enter a role if OneLogin users logging into conduit must have at least this OneLogin role to gain access to Conduit.
    DEFAULT ROLE
      The default Conduit Role applied to users created from OneLogin Integration if no other role mapping is specified below
    ROLE MAPPINGS
      Existing Conduit Roles will be listed with fields to enter OneLogin Roles to map to. Users with OneLogin roles matching the role mappings will be assigned the appropriate Role(s) in Conduit when signing in.

#. Select :guilabel:`SAVE CHANGES` and the OneLogin Integration will be added.

Users can now login to Conduit with OneLogin credentials. The first Login will create a user in Conduit matching the Username, email and Password from OneLogin. If a REQUIRED ROLE is specified in the Identity Source settings, only users with that Role in OneLogin will be able to login to Conduit.

.. IMPORTANT:: OneLogin users will not authenticate in Conduit if there is an existing Conduit User with matching username or email address.
