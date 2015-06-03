A [Dockerfile](./Dockerfile) adds a layer on top of `concourse/concourse-ci` and
into the directory `/usr/local/testutils/`.

**install-package** which will download the compiled package from BOSH and
install it on another job. This is useful when you need to reuse the package
from a job which is purely for testing and doesn't have any other templates
which would normally include this.

    $ install-package \
      target-host-ip \
      release-name-and-version \
      stemcell-name-and-version \
      package-name

    $ install-package \
      192.168.170.192 \
      logsearch/19 \
      bosh-aws-xen-hvm-ubuntu-trusty-go_agent/2978 \
      java8

**install-packages** exactly the same as `install-package` but allows you to
pass more than one package to install.

    $ install-package \
      192.168.170.192 \
      logsearch/19 \
      bosh-aws-xen-hvm-ubuntu-trusty-go_agent/2978 \
      java8 logstash

**get-deployment-stemcell** will do a simple grep to return the stemcell
used by the particular deployment. Useful for passing as the argument to
`install-package`.

    $ get-deployment-stemcell logsearch-sanity-test
    bosh-aws-xen-hvm-ubuntu-trusty-go_agent/2978

**silo-host** will switch to using the IP of the silo environment.
Useful for allowing your test runners to refer to DNS names instead of grepping
`bosh deployments` outputs.

    $ silo-host 0.standalone.silo-private.logsearch-sanity-test.bosh
    192.168.170.117

The [SSH files](./ssh/) are available for use and pre-installed. If you're using
the [`testutils/keys`](../release/) template, these are the keys which are added
by default.
