Some tools to help automate testing of BOSH deployments used within the context
of Concourse CI.

Components (they play well together):

 * [**silo-network**](./silo-network/) - quickly set up a reproducible director
   in a reproducible network where you can write test deployments against
 * [**release**](./release/) - a release with templates for allowing tests to
   execute against jobs via SSH, with root access, and referencing custom data
 * [**automation**](./automation/) - a container with scripts to help test
   runners interact with and execute tasks on test jobs
