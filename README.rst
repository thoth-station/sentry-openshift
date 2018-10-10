Sentry running on OpenShift
---------------------------

This project was adopted with changes from
`https://github.com/rhdt/error-tracking`_ repository. Thanks for awesome job!

Once the deployment is done, there is run a database populator job (a one time
job) that setups PostgreSQL database.

The default credentials are (see the configuration stated in the ``provision.yaml``):
* Username: noreply@redhat.com
* Password: 123456

Provisioning
============

.. code-block:: console

  # Clone this repo and revisit the provisioning configuration:
  vim playbooks/provision.yaml
  # If all looks ok, run the provision playbook:
  OCP_URL=$(oc whoami --show-server) OCP_TOKEN=$(oc whoami --show-token) SENTRY_NAMESPACE='sentry-namespace' ansible-playbook playbooks/provision.yaml


Deprovisioning
==============

.. code-block:: console

  ansible-playbook playbooks/deprovision.yaml --extra-vars SENTRY_NAMESPACE=sentry-namespace

The persistent volumes used are left untouched and need to be deleted manually
if needed.

Troubleshooting
===============

If you are unable to log into Sentry after provisioning with an error message
"CSRF Verification Failed", check route configuration. It should use TLS.
