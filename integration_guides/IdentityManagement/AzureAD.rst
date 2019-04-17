Azure Active Directory SSO (SAML)
---------------------------------

Azure Active Directory Single Sign-on can be added as a Identity Source in |conduit| using the SAML Identity Source Type. The Azure AD SSO configuration is slightly different than other SAML providers, and this guide will assist in adding a Azure AD SSO Identity Source.

Create a Azure AD SAML Integration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Azure requires inputing the `Identifier (Entity ID)` and `Reply URL (Assertion Consumer Service URL)` in the Azure SSO configuration before it provides the Endpoints and Certificate neccessary to add the Integration into |conduit|. In order to get the `Identifier (Entity ID)` and `Reply URL (Assertion Consumer Service URL)` to input into Azure SSO config, we need to create a base SAML Integration in |conduit| first.

To add a base SAML integration:

#. Navigate to ``Administration -> Tenants``
#. Select a tenant.
#. Select IDENTITY SOURCES in the Tenant detail page
#. Select :guilabel:`+ ADD IDENTITY SOURCE`.
#. Select ``SAML (external login)`` from the TYPE field
#. Add a Name, optional Description and any value in the LOGIN REDIRECT URL field.
    Since we do not have the LOGIN REDIRECT URL from Azure yet, type any text such as ``test`` into the LOGIN REDIRECT URL field so the Identity Source Integration can be saved and the `Identifier (Entity ID)` and `Reply URL (Assertion Consumer Service URL)` generated. We will edit the Integration with the proper LOGIN REDIRECT URL after configuring SSO in Azure.
#. Select :guilabel:`SAVE CHANGES`.

Upon save the `Entity ID` (Identifier (Entity ID)) and `SP ACS URL` (Reply URL (Assertion Consumer Service URL)) will be provide in the Identity Source list view. Copy these for use in Azure SSO config.

Configure Azure SSO
^^^^^^^^^^^^^^^^^^^

This guide assumes an Azure AD Application has already been created in Azure, with a subscription level high enough to configure SSO in the application. Please refer to Azure documentation if this has not already been configured.

#. Next, in the Azure Active Directory Application details page, select ``Single sign-on`` in the Apps left hand nav, then enter the following:

   * Single Sign-on Mode dropdown
        Select ``SAML-based Sign-on``
   * Identifier (Entity ID)
        Enter the ``Entity ID`` URL from the |conduit| Identity Source Integration above.
   * Reply URL (Assertion Consumer Service URL)
        Enter the ``SP ACS URL`` from the |conduit| Identity Source Integration above.

#. Save and click the `Test SAML Settings` button. Azure will confirm conneciton with |conduit|
#. In Azure SSO config step 3, select ``user.userprincipalname`` as the User Identifier.
#. Also in step 3, select "View and edit all other user attributes" the copy the NAMESPACE url for the following:

   Name ``givenname`` Value: ``user.givenname``
      Namespace: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname
   Name: ``surname`` Value: ``user.surname``
      Namespace: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname
   Name: ``emailaddress`` Value: ``user.mail``
      Namespace: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress

   .. NOTE:: The Namespace URLs will be used in the `Role Attribute Value` section in the |conduit| Identity Source Integration.

#. In Azure SSO config step 4, if one has not been generated, select ``Create new certificate`` to generate a new SAML Signing Certificate.
#. Enter a valid email address to receive certificate expiration notifications at (not related to |conduit|).
#. In Azure SSO config step 5, select ```Configure {AD App Name}``
#. In the `Configure sign-on` pane, copy the following:

   * SAML Single Sign-On Service URL
      This will be used for the LOGIN REDIRECT URL in the |conduit| Identity Source Integration settings
   * Sign-Out URL
      This will be used for the LOGOUT POST URL in the |conduit| Identity Source Integration settings
   * Click on the ``SAML XML Metadata`` link, open the xml file, and copy the key between the ``<X509Certificate>`` and ``</X509Certificate>``.
      This will be used for the `SIGNING PUBLIC KEY` in the |conduit| Identity Source Integration settings

      Example Key (the key has been altered and is not valid):

     .. code-block:: bash

      MIIC8ECCAdigAwIBAgIQEOZXlNx5wY9Dc6OwlsKEMzANBgkqhkiG9w0BAQsFADA0MTIwMAYDVQQDEylNaWNyb3NvZnQgQXp1cmUgRmVkZXJhdGVkIFNTTyBDZXJ0aWZpY2F0ZTAeFw0xODAyMTYxNTU4NTlaFw0yMTAyMTYxNTU4NTlaMDQxMjAwBgNVBAMTTU1pY3Jvc29mdCBBenVyZSBGZWRlcmF0ZWQgU1NPIENlcnRpZmljYXRlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA2k/V6GcBpRkoxJd0DLbhubwd0kp65LD9IIh5PUY2ohBHvrFAy3SZ04mXoH7LWvY3oNrqxaNAksbYF6phOkONf/XeTdzor14xdGnTuD9zRqPsJHHisyfFBUG/CxYxzO6w9fAPzJGLzc0Y7o5lMW2OjINaqI4R/pqp3qw+nYf7DXSzY6tf1Sspk64jfZDt1jSVjD7upMItKPeOCRmeBUcnebjzwXqFBO7l4Vf5g1oEJvftT7Wpr4VVmoLh8rFGWbQ1wlmtsK9RrWTqdt3su2H9uNrEjWiZ62x6ate2fs0dXnz17KoV7RQOpqYtjom76jNUzorcl73D5AGwW6x+2wIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQCSjf2IOG6O3wdOmkfJ/pH6xzQVRz0GZQpol9ViQJJbJJqhLm4LjWT9VU2lYqdi0NdgtK7QthZo4J0ZFdUG6qfFTfPKqVn0AEHxiM4JWxfigzdMJUutHcRRoaJ8VvywZYJKE91e4TDuBOw8XqdBiBx627ZybXCuR/y56+ksYSRP87XdOcVvTftHYmQnDOf0qKrpgMK7LtmsEwqc7rKX7nTCenZnBEBOCFDBVH4QEzMrAznEPdJnQs9nJZBNCYJUrCRXbPKpXE9u8MlTVq4swFm96xsXkfeP8NFsgrXmzOn3BsHaBXqdhrrkbwq85VPWUaoIomlhAWQq/seC

#. Save the SSO config in Azure AD app and return to |conduit|

Edit the existing Azure AD SAML Integration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   Now that we have the required information, we can finalize the Azure AD SAML Integration in |conduit|

#. Edit the existing Azure AD SAML Integration created above and populate the following:

   LOGIN REDIRECT URL
      Add the SAML Single Sign-On Service URL copied from Azure SSO config.
   LOGOUT POST URL
      Add the Sign-Out URL copied from Azure SSO config.
   SIGNING PUBLIC KEY (uncheck "Do not validate SAMLResponse signatures" if desired)
      Add the SAML XML Metadata key copied from Azure SSO config.
   GIVEN NAME ATTRIBUTE NAME
      Enter the ``givenname`` Namespace url from Azure SSO config: http://schemas.xmlsoap.org/ws/2005/05/identity/claims
   EMAIL ATTRIBUTE NAME
    Enter the ``surname`` Namespace url from Azure SSO config: http://schemas.xmlsoap.org/ws/2005/05/identity/claims
   SURNAME ATTRIBUTE NAME
    Enter the ``emailaddress`` Namespace url from Azure SSO config: http://schemas.xmlsoap.org/ws/2005/05/identity/claims

Configure Role Mappings
^^^^^^^^^^^^^^^^^^^^^^^

Role mappings will map Azure AD Groups to Conduit Roles. Azure AD users will be assigned Roles in |conduit| upon signing based on their Group Membership in Azure AD.

.. IMPORTANT:: Use an Azure Groups ``Object ID``, not Group name, when entering Role Mappings. Example: ``7626a4a2-b388-4d9b-a228-72ce9a33bd4b``

DEFAULT ROLE
  Role a Azure AD user will be assigned by default upon signing in to |conduit| using this Identity Source.
ROLE ATTRIBUTE NAME
  Enter ``http://schemas.microsoft.com/ws/2008/06/identity/claims/groups`` for Azure AD SSO
REQUIRED ROLE ATTRIBUTE VALUE
  Object ID of Azure AD Group a user must be a member of to be authorized to sign in to |conduit|. Users not belonging to this Group will not be authorized to login to |conduit|. This field is optional, and if left blank, any user from the Azure AD App will be able to sign in to |conduit| and will be assigned the Default Role if no Role Mappings match AD Group membership.
Additional Role Mappings
  The existing Roles in |conduit| will be listed. To map a |conduit| Role to an Azure AD Group, enter the Object ID of the desired Azure AD Group in the `Role Attribute Value` field for the corresponding |conduit| Role.

.. IMPORTANT:: Use an Azure Groups ``Object ID``, not Group name, when entering Role Mappings. Example: ``7626a4a2-b388-4d9b-a228-72ce9a33bd4b``

Once populated, select :guilabel:`SAVE CHANGES` and the SAML identity source integration will be added. The Identity Source can be edited anytime to deactivate or change Role Mappings or other values.

.. NOTE:: If Role mappings are edited after Azure AD SSO users have signed into |conduit|, currently logged in users will need to log out of |conduit| for the new Role mappings to take effect, when applicable.

Signing In to |conduit|
^^^^^^^^^^^^^^^^^^^^^^^^

When there is an active SAML/Azure AD SSO Identity Source Integration, a new button will appear on the |conduit| login page below LOGIN WITH with the name of the Identity Source Integration as the button title. Example: :guilabel:`AZURE AD`. Another button titled "USERNAME AND PASSWORD" is also added in place of the standard Username and Password fields.

* SAML/Azure AD SSO users can log into |conduit| by clicking the SAML button
      This will redirect the User to Azure AD app sign in url. If they are currently signed into Azure and authorized, the user will be instantly signed into |conduit|.
* Local |conduit| users can select "USERNAME AND PASSWORD" to sign in with their local credentials as before.
      If no local users other than the System Admin have been created, "USERNAME AND PASSWORD" option will not be displayed, only the SAML option.
