Authenticator
===========================

The Authenticator is the mechanism for authorizing users to use the Hub and single user notebook servers.

Native Authenticator
######################

This is a relatively simple authenticator for small or medium-sized JupyterHub applications. 
Signup and authentication are 
implemented as native to JupyterHub without relying on external services.

Documentation
The latest documentation is always on readTheDocs, available here.

Running tests
To run the tests locally, you can install the development dependencies like so:

pip install -r dev-requirements.txt
Then run tests with pytest:

pytest

ldapauthenticator
######################

Simple LDAP Authenticator Plugin for JupyterHub

Installation
You can install it from pip with:

pip install jupyterhub-ldapauthenticator
...or using conda with:

conda install -c conda-forge jupyterhub-ldapauthenticator