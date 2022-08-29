Quickstart - Installation
===========================
**Prerequisites**

*Before installing JupyterHub and the Makefile file to work *, you will need:

- `Alma Linux <https://almalinux.org/>`_ 8.6 or greater
   
  A fresh installation of this distribution.Inside the the folder `auto_deploy_RHEL`, the script has been customized to work with the Alma Linux 8.6. 
  and few other distribution of the same family, like `CentOS 7.6 <https://www.centos.org//>`_, 
  `RHEL <https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux/>`_, and others. 
   
- `Ansible <https://www.ansible.com/>`_ xx.x or greater

- `Python <https://www.python.org/downloads/>`_ 3.3 or greater

  An understanding of using `pip <https://pip.pypa.io/en/stable/>`_ or
  `conda <http://conda.pydata.org/docs/get-started.html>`_ for
  installing Python packages is helpful.

- `nodejs/npm <https://www.npmjs.com/>`_

  `Install nodejs/npm <https://docs.npmjs.com/getting-started/installing-node>`_,
  using your operating system's package manager. For example, install on Linux
  (Debian/Ubuntu) using:

The ``nodejs-legacy`` package installs the ``node`` executable and is currently required for npm to work on Debian/Ubuntu.

- Apart from the above mentioned requirements, we also have to install the following packages:
  
    ``make`` , ``curl``, ``git``


Auto-Installation
#############

One command to install all the required packages and jupyterhub, we will issue:

.. code-block:: bash

    make all

Step-by-Step Installation
#############

One command to install all the required packages and jupyterhub, we will issue:

.. code-block:: bash

    make software

One command to install all the required packages and jupyterhub, we will issue:

.. code-block:: bash

    make software

One command to install all the required packages and jupyterhub, we will issue:

.. code-block:: bash

    make software    


Manual Installation
#############

Before installing JupyterHub we have to install a proxy server, 
which can be installed with `pip` or `conda` or `npm`:


**make :**
 .. code-block:: bash

   make install_proxy
   
This will install the proxy server ``configurable-http-proxy``. 
or we can manually install it using:

**pip, npm:**
 .. code-block:: bash

   npm install -g configurable-http-proxy

make sure npm is configured properly, if the system is behind a proxy server.

**conda** (one command installs jupyterhub and proxy):

 .. code-block:: bash

   conda install -c conda-forge jupyterhub


To test your installation:

 .. code-block:: bash

   jupyterhub -h
   configurable-http-proxy -h


If you plan to run notebook servers locally, you will need also to install
Jupyter notebook:

**pip:**
 .. code-block:: bash
   
   python3 -m pip install notebook


**conda:**
 .. code-block:: bash

   conda install notebook


Start the Hub server
####################

To start the Hub server, run the command:

 .. code-block:: bash
   
   jupyterhub


Visit https://localhost:8000 in your browser, and sign in with your unix credentials.

To allow multiple users to sign into the Hub server, you must start `jupyterhub` as a *privileged user*, such as root:

 .. code-block:: bash

   sudo jupyterhub

The `wiki <https://github.com/jupyterhub/jupyterhubwiki>`_ Using-sudo-to-run-JupyterHub-without-root-privileges describes how to run the server as a *less privileged user*, which requires additional configuration of the system.


Basic Configuration
#####################

The [getting started document](docs/source/getting-started.md) contains
detailed information abouts configuring a JupyterHub deployment.

The JupyterHub **tutorial** provides a video and documentation that explains and illustrates the fundamental steps for installation and configuration.
`repo <https://github.com/jupyterhub/jupyterhub-tutorial>`_
`Tutorial documentation <http://jupyterhub-tutorial.readthedocs.io/en/latest/>`_

Generate a default configuration file

Generate a default config file:
 .. code-block:: bash

    jupyterhub --generate-config

**Customize the configuration, authentication, and process spawning**

Spawn the server on ``10.0.1.2:443`` with **https**:
 .. code-block:: bash

    jupyterhub --ip 10.0.1.2 --port 443 --ssl-key my_ssl.key --ssl-cert my_ssl.cert

The authentication and process spawning mechanisms can be replaced,
which should allow plugging into a variety of authentication or process
control environments. Some examples, meant as illustration and testing of this
concept, are:

- Using GitHub OAuth instead of PAM with `OAuthenticator <https://github.com/jupyterhub/oauthenticator>`_
- Spawning single-user servers with Docker, using the `DockerSpawner <https://github.com/jupyterhub/dockerspawner>`_

----

Alternate Installation using Docker

A ready to go `docker image for JupyterHub <https://hub.docker.com/r/jupyterhub/jupyterhub/>`_
gives a straightforward deployment of JupyterHub.

*Note: This `jupyterhub/jupyterhub` docker image is only an image for running the Hub service itself. It does not provide the other Jupyter components, such as Notebook installation, which are needed by the single-user servers.To run the single-user servers, which may be on the same system as the Hub or not, Jupyter Notebook version 4 or greater must be installed.*

Starting JupyterHub with docker
################################

The JupyterHub docker image can be started with the following command:

 .. code-block:: bash

    docker run -d --name jupyterhub jupyterhub/jupyterhub jupyterhub

This command will create a container named `jupyterhub` that you can
*stop and resume* with

.. code-block:: bash

   docker stop/start

The Hub service will be listening on all interfaces at port 8000, which makes this a good choice for *testing JupyterHub on your desktop or laptop*.

If you want to run docker on a computer that has a public IP then you should(as in MUST) *secure it with ssl* by adding ssl options to your docker configuration or using a ssl enabled proxy.

`Mounting volumes <https://docs.docker.com/engine/userguide/containers/dockervolumes/>`_ will allow you to *store data outside the docker image (host system) so it will be persistent*, even when you start a new image.

The command 
 .. code-block:: bash

   docker exec -it jupyterhub bash`

will spawn a root shell in your
docker container. You can *use the root shell to create system users in the container*.These accounts will be used for authentication in JupyterHub's default
configuration.
