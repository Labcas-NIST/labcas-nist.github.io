Mock vs Real Single-Sign On
===========================

This document describes the differences between the single-sign on (SSO) solution for the `Laboratory Catalog and Archive System`_ for the `National Institutes of Standards and Technology`_.


Mock SSO
--------

The mock SSO solution for NIST LabCAS uses the ``mock-auth`` service to simulate an SSO solution by acting as a sample identity provider.

The service_ is launched from the `docker-compose.yml`_ file in the `labcas-docker`_ repository. The service_ is implemented as a Node_ application that listens on TCP port 3001 and responds to authentication requests over HTTP and returns a fixed JWT_ response token with the following hard-coded fields:

- ``userId``: ``testUser``
- ``userEmail``: ``user@example.com``
- ``userName``: ``Test``
- ``userLastName``: ``User``
- ``winId``: ``test1``
- ``Group``: ``Mock Auth Group``

The token is always named ``dummy-jwt-token-value`` and is returned on request to ``/sso/saml/login``.

.. note::
    The backend will not accept the ``dummy-jwt-token-value`` as valid unless it's started with the ``ACCEPT_ANY_JWT`` environment variable set to the word ``DANGEROUS``. This is a reminder that the mock SSO solution is not secure as it authenticates any and every user as valied and returns the ``dummy-jwt-token-value`` JWT for all users.


Actual SSO
----------

The actual SSO solution for NIST LabCAS is yet to be determined. NIST runs a large user database and has an identity provider whose details are not yet known. What is known is that this SSO solution will provided JWT tokens with non-mock values (such as those listed above), and will be cryptographically signed by a private key. The only fields in the token that are guaranteed to be present are ``userId`` and ``userEmail``.

Once the LabCAS user interface receives its redirection from the NIST SSO login screen, it is also given the signed JWT. The JWT can then be passed to the backend, which will use it to determine the user's identity and permissions. Note that NIST SSO does not indicate group membership, so the backend will use LDAP at ``ldaps://edrn-ds.jpl.nasa.gov`` to look up group memberships for the user ID (using the ``userId`` field from the JWT)and use that information to check and enforcepermissions.

Administrators can manage group memberships using Biokey_, a convenient web application for interacting with the LDAP server used by LabCAS (and used for group memberships only—although currently it is also used for users, as integration with the actual NIST SSO is ongoing).


.. References:
.. _Laboratory Catalog and Archive System: https://github.com/jpl-labcas
.. _National Institutes of Standards and Technology: https://labcas-nist.github.io/
.. _docker-compose.yml: https://github.com/Labcas-NIST/labcas-docker/blob/5678ac464a7c15b82426002046523267f030133b/docker-compose.yml#L68
.. _labcas-docker: https://github.com/Labcas-NIST/labcas-docker
.. _service: https://github.com/Labcas-NIST/labcas-docker/tree/master/mock-auth
.. _Node: https://nodejs.org/
.. _JWT: https://jwt.io/
.. _Biokey: https://edrn-labcas.jpl.nasa.gov/biokey/nist/
