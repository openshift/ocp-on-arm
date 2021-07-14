OpenShift on ARM Developer Preview
==================================

***OpenShift*** is Red Hat's distribution of [Kubernetes](https://kubernetes.io) optimized for continuous application development and multi-tenant deployment. OpenShift adds developer and operations-centric tools on top of Kubernetes to enable rapid application development, easy deployment and scaling, and long-term lifecycle maintenance for small and large teams.

This repository provides installation instructions and an issue tracker for the developer preview release of OpenShift on ARM.

Please note that this developer preview is based on a nightly build of OpenShift 4.9, and therefore is neither feature nor bug complete.


Getting Started
---------------

To obtain the openshift installer and client, visit [cloud.redhat.com](https://cloud.redhat.com/openshift/install/aws/arm).  Please note that the Linux binaries on that page are for x86_64; if you need Linux ARM binaries, they are available at [mirror.openshift.com](https://mirror.openshift.com/pub/openshift-v4/aarch64/clients/ocp-dev-preview/pre-release/).

Extract the downloaded tarballs and copy the binaries into your PATH. Then run the following from an empty directory:

```
$ openshift-install create install-config
```

You'll be prompted to choose a platform to install to - AWS is the only available public cloud option for ARM at this time.

You will need to have cloud credentials set in your shell properly before installation.  The account setup steps for AWS are identical to an x86_64 install, and are described in [the installer documentation](https://github.com/openshift/installer/tree/master/docs/user/aws#readme).

When selecting a region, note that ARM instances are available in [most, but not all, AWS regions](https://aws.amazon.com/about-aws/whats-new/2021/02/aws-graviton2-m6g-c6g-r6g-instances-available-additional-regions/).

You will also be prompted for a pull-secret that will be made available to all of of your machines - get this from [cloud.redhat.com](https://cloud.redhat.com/openshift/install/aws/arm).

This will create an install-config.yaml file which defines the installation.  Please verify that both `architecture` values are set to `arm64`.  Also, it is recommended to change `network.networkType` to `OVNKubernetes`, but the default value of `OpenShiftSDN` will still work.

Now, to create the cluster, run

```
$ openshift-install create cluster
```

Once the install completes successfully (usually 45m on AWS) the console URL and an admin username and password will be printed. If your DNS records were correct, you should be able to log in to your new OpenShift on ARM cluster!

To undo the installation and delete any cloud resources created by the installer, run

```
$ openshift-install destroy cluster
```

[Learn more about the installer](https://github.com/openshift/installer/blob/master/docs/user/overview.md)

The OpenShift client tools for your cluster can be downloaded from the web console.

Please note that pre-releases may be pruned over time. If the pre-release that you installed was pruned, the cluster may be unable to pull necessary images and may show errors for various functionality (including updates). In that case, you will need to redeploy with a new pre-release.


Contributing
------------

OpenShift is built from many different open source projects - Red Hat CoreOS, the UBI RPM ecosystems, cri-o, Kubernetes, and many different extensions to Kubernetes. The `openshift` organization on GitHub holds active development of components on top of Kubernetes and references projects built elsewhere. Generally, you'll want to find the component that interests you and review their README.md for the processes for contributing.

Issues with OpenShift on ARM can be [opened in this repository](https://github.com/openshift/ocp-on-arm/issues).

Our unified continuous integration system tests pull requests to the ecosystem and core images, then builds and promotes them after merge. To see the latest development releases of OpenShift on ARM, visit [our continuous release page](https://arm64.ocp.releases.ci.openshift.org/). These releases are built continuously and expire after a few days.

All contributions are welcome - OpenShift uses the Apache 2 license and does not require any contributor agreement to submit patches.  Please open issues for any bugs or problems you encounter, or get involved in the [Kubernetes project](https://github.com/kubernetes/kubernetes) at the container runtime layer.


Security Response
-----------------
If you've found a security issue that you'd like to disclose confidentially
please contact Red Hat's Product Security team. Details at
https://access.redhat.com/security/team/contact


Known Issues
------------
Known issues and possible workarounds are documented on this page:
[Known Issues](./KNOWN_ISSUES.md)


License
-------
OpenShift is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/). Some components may be licensed differently - consult individual repositories for more.
