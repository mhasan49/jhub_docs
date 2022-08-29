Proxy-Server
===========================

It is a simple wrapper around node-http-proxy. node-http-proxy is an HTTP programmable proxying library
that supports websockets and is suitable for implementing components such as reverse 
proxies and load balancers. 

Manual Installation
####################

``Prerequisite: Node.js ≥ 10``

If you're installing configurable-http-proxy in Linux, you can follow the instruction of 
nodesource to install arbitrary version of Node.js.

To install the configurable-http-proxy package globally using npm:

.. code:: bash
    
     npm install configurable-http-proxy -g

To install from the source code found in this GitHub repo:

.. code:: bash

     git clone https://github.com/jupyterhub/configurable-http-proxy

     cd configurable-http-proxy
     
     npm install  # Use 'npm install -g' for global install

For more information on configurable-http-proxy, see the official documentation:
`configurable-http-proxy <https://github.com/jupyterhub/configurable-http-proxy>`_

Auto Installation
####################

In order to use ansible script to install the proxy-server, we will use:

.. code:: bash
    
    make install_proxyserver
