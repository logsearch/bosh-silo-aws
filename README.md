Create a very simple, standalone network to send off BOSH deployments for testing.

We didn't want to open-source our full network, so at least this way we can provide the exact environment we're testing under in case you're curious or want to use it yourself.


## Environment

The network uses `192.168.170.0/24`, split into three subnets:

 * Public (Internet-connected): `192.168.170.64/26`
 * Private (Internet-routeable): `192.168.170.128/26`
 * Internal (LAN-only): `192.168.170.192/26`

Two servers are provisioned:

 * Gateway - `192.168.170.4`
 * BOSH Director - `192.168.170.68`

BOSH has a login:

 * Username: `admin`
 * Password: `admin`

BOSH has networks and resource pools configured:

 * Networks: `silo-public`, `silo-private`, `silo-internal`
 * Resource Types: `silo-{cpi-type}-{network}`... (e.g. `silo-c4-xlarge-private`)


## Deployment

Make sure the following commands are installed...

 * [`aws`](http://aws.amazon.com/cli/)
 * [`bosh-init`](https://bosh.io/docs/install-bosh-init.html)
 * [`jq`](http://stedolan.github.io/jq/)

Provide some configuration values (see [`cloudformation.json`](./cloudformation.json) for descriptions)...

    $ cp cloudformation-config.default.json cloudformation-config.json
    $ vim cloudformation-config.json

Provision the environment...

    $ ./deploy

It should take about 5 minutes to provision the network in AWS, then 10 - 30 minutes to provision the director.


## Notes

If you're peering this to another VPC, don't forget to update your other VPC and...

 * accept the VPC Peering Connection request
 * add routes back to this VPC in your existing route tables
 * add appropriate security group rules to allow access to/from this VPC network

If you need to adjust the configuration values, the `deploy` script can safely be re-run afterwards to update things.

To tear down the network, director, and deployments, you can run...

    $ ./destroy

Environment is stored in `.env` - if you `source .env` you can use the variables within your own shell commands. You really should avoid commiting them though - they contain AWS credentials and your other identifiers.
