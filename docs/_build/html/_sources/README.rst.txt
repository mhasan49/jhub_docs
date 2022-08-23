JupyterHub
==========

With JupyterHub you can create a **multi-user Hub** which spawns, manages,
and proxies multiple instances of the single-user
`Jupyter notebook <https://jupyter-notebook.readthedocs.io/en/latest/>`_ server.
Due to its flexibility and customization options, JupyterHub can be used to
serve notebooks to a class of students, a corporate data science group, or a
scientific research group.


Three subsystems make up JupyterHub:

* a multi-user **Hub** (tornado process)
* a **configurable http proxy** (node-http-proxy)
* multiple **single-user Jupyter notebook servers** (Python/IPython/tornado)

JupyterHub's basic flow of operations includes:

- The Hub spawns a proxy
- The proxy forwards all requests to the Hub by default
- The Hub handles user login and spawns single-user servers on demand
- The Hub configures the proxy to forward URL prefixes to the single-user notebook servers


Contents
--------

**User Guide**

* :doc:`quickstart`
* :doc:`ansible-script`


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: User Guide

   quickstart
   ansible-script

   
