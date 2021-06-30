# Known issues in the OpenShift on ARM developer preview

## [openshift-marketplace pods are in a non-ready state](https://github.com/openshift/ocp-on-arm/issues/1)

  **Description:** When starting a cluster on ARM, warnings are generated that various `openshift-marketplace` pods are in a non-ready state.

  **Workaround:** `oc patch operatorhub.config.openshift.io/cluster -p='{"spec":{"disableAllDefaultSources":true}}' --type=merge`

## [Various conformance tests may fail due to missing images on ARM](https://github.com/openshift/ocp-on-arm/issues/6)

  **Description:** A number of conformance tests will fail due to being unable to pull the images used by the tests.

  **Workaround:** `openshift-tests run openshift/conformance/parallel --from-repository quay.io/multi-arch/community-e2e-images`

