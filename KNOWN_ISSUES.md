# Known issues in the OpenShift on ARM developer preview

## [No OperatorHub items found](https://github.com/openshift/ocp-on-arm/issues/1)

  **Description:** The default `CatalogSource`s used by OperatorHub are not installed by default on ARM.

  **Workaround:** Update the cluster to at least 4.9.10.

## [ImageStream, ImageStreamTag, and Template selection is limited on ARM](https://github.com/openshift/ocp-on-arm/issues/10)

  **Description:** Fewer `ImageStream`s, `ImageStreamTag`s, and `Template`s are available on ARM, based on the availability of the underlying container images.
  In particular, anything dependent on RHEL 7 or UBI 7 is not available on ARM.
  
  **Workaround:** Update templates to use only `-ubi8` or `-el8` suffixed `ImageStreamTag`s.

## [Various conformance tests may fail due to missing images on ARM](https://github.com/openshift/ocp-on-arm/issues/6)

  **Description:** A number of conformance tests will fail due to being unable to pull the images used by the tests.

  **Workaround:** `openshift-tests run openshift/conformance/parallel --from-repository quay.io/multi-arch/community-e2e-images`

## Recommendation to change network provider before installation

  **Description:** The intended default network provider for a future release of OpenShift on ARM is OVN-Kubernetes, however, the installer currently defaults to OpenShift SDN.
  
  **Workaround:** It is recommended that you set `network.networkType` in the `install-config.yaml` to `OVNKubernetes` before creating your cluster.
  A cluster created with the default value of `OpenShiftSDN` will still be operational.  Migrating an existing cluster has not been tested on ARM.

