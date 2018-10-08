Sentry running on OpenShift
---------------------------

This project was adopted with changes from
`https://github.com/rhdt/error-tracking`_ repository. Thanks for awesome job!

There are provisioned:
* Sentry CronJob
* Sentry Worker
* Sentry Web
* Redis
* PostgreSQL

There are required 2 persistent volumes - one for PostgreSQL, another one for
Redis.

If you are provisioning onto Upshift, do not forget to add secret for mounting
the configured storage class. If not, revisit storage class configuration in
the deployment configs to respect your cluster configuration.

Once the deployment is done, there is run a database populator job (a one time
job) that setups PostgreSQL database.


Provisioning
============

.. code-block:: console

  # Clone this repo and run:
  OCP_URL=$(oc whoami --show-server) OCP_TOKEN=$(oc whoami --show-token) SENTRY_NAMESPACE='sentry-namespace' ansible-playbook playbooks/provision.yaml


Deprovisioning
==============

.. code-block:: console

  ansible-playbook playbooks/deprovision.yaml --extra-vars SENTRY_NAMESPACE=sentry-namespace

The persistent volumes used are left untouched and need to be deleted manually
if needed.

