# Tanzu Application Platform release notes

This topic describes the changes in Tanzu Application Platform (commonly known as TAP)
v{{ vars.url_version }}.

{{#unless vars.hide_content}}

This Handlebars condition is used to hide content.

In release notes, this condition hides content that describes an unreleased patch for a released minor.

{{/unless}}

## <a id='1-6-0'></a> v1.6.0

**Release Date**: 27 July 2023

### <a id='1-6-0-whats-new'></a> What's new in Tanzu Application Platform

This release includes the following platform-wide enhancements.

#### <a id='1-6-0-new-platform-features'></a> New platform-wide features

- New services available with the Bitnami Service package: MongoDB and Kafka.

#### <a id='1-6-0-new-components'></a> New components

- [Local Source Proxy](local-source-proxy/about.hbs.md) offers developers with a secure and
user-friendly solution that enables them to effortlessly upload their local source code to a registry,
which is pre-configured by an Operator during the installation of Tanzu Application Platform.
This component effectively eliminates the obstacles faced by developers when they had to manually specify
a registry and provide their credentials on their local systems for iterative inner loop workflows.

---

### <a id='1-6-0-new-features'></a> New features by component and area

This release includes the following changes, listed by component and area.
#### <a id='1-6-0-appacc'></a> Application Accelerator
- The Application Accelerator plug-in for IntelliJ is now GA on [Tanzu Network](https://network.tanzu.vmware.com/products/tanzu-application-platform/). The plug-in for IntelliJ now supports Git repo creation and dynamic options and embeds telemetry and bootstrapping provenance. For more information, see [Application Accelerator IntelliJ Plug-in](./application-accelerator/intellij.hbs.md)


#### <a id='1-6-0-alv'></a> Application Live View
- Application Live View supports secure access to sensitive operations that can be executed on a running application using the actuator endpoints at the user level. For more information, see [w](./app-live-view/improved-security-and-access-control.hbs.md)
- Developers can view the live information of natively compiled Spring applications via Application Live View for lightweight troubleshooting. The pages and metrics currently unavailable for natively compiled Spring applications include threads, heapdump, memory graphs, cache manager, conditions, schedules tasks and actuator information. For more information, see [Enable Spring Native apps for Application Live View]()

#### <a id='1-6-0-apps-cli-plugin-new-features'></a> Apps plug-in for Tanzu CLI

- Integrated with Local Source Proxy for seamless iterative inner-loop development using the CLI or IDE plugins.
  - `tanzu apps workload apply` and `tanzu apps workload create` can now seamlessly create a workload from
    local source using just the `--local-path` flag.
  - `--source-image` flag is now optional. if `--source-image` flag is used along with `--local-path`, the
    Local source proxy is not used and bypassed for backward compatibility.
  - Introducing a new command, `tanzu apps lsp health` which allows users to verify the status of the Local
    Source Proxy. This command performs several checks, including:
    - Verifying whether the developer has RBAC permissions to access the Local Source Proxy using their `kubeconfig`.
    - Checking if the Local Source Proxy is installed on the cluster.
    - Ensuring that the Local Source Proxy deployment is healthy and accessible.
    - Verifying that the Local Source Proxy is correctly configured and able to access the registry using the
      credentials set up by the operator during TAP installation.
- Implemented `autocompletion` functionality for workload types. Additionally, the default workload type has been
  set to `web`, making the `--type` flag optional. The flag is only required if the type is something other than `web`.
- Introduced the shorthand option `-e` as a convenient alternative for the `--export` flag.
- Enhanced the `tanzu apps workload get` command by including Git revision information in the overview section.
  This addition provides a quick reference to the Git revision associated with the workload.


#### <a id='1-6-0-appsso'></a> Application Single Sign-On (AppSSO)

- Incorporates the token expiry settings into the `AuthServer` resource. Service
  operators can customize the expiry settings of access, refresh, or identity
  tokens. For more information, see
  [Token settings](./app-sso/tutorials/service-operators/token-settings.hbs.md#token-expiry-settings).
- Enables the ability to:
  - Map custom user attributes or claims from upstream identity providers, such as OpenID, LDAP, and SAML.
  - Configure the internal unsafe provider with custom claims.
    For more information, see [Identity providers](./app-sso/tutorials/service-operators/identity-providers.hbs.md#id-token-claims-mapping).
- Adds `ClusterUnsafeTestLogin`, which is an unsafe, ready-to-claim AppSSO service offering you can
  use to get started with Application Single Sign-On in non-production environments.
  It is not safe for production.
  For more information, see [ClusterUnsafeTestLogin API](app-sso/reference/api/clusterunsafetestlogin.hbs.md).
- Adds `ClusterWorkloadRegistrationClass`, which exposes an `AuthServer` as a ready-to-claim AppSSO
  service offering.
  For more information, see [ClusterWorkloadRegistrationClass API](app-sso/reference/api/clusterworkloadregistrationclass.hbs.md).
- Adds `WorkloadRegistration`, which is a portable client registration which templates redirect URIs.
  For more information, see [WorkloadRegistration API](app-sso/reference/api/workloadregistration.hbs.md).
- Adds `XWorkloadRegistration`, which is an XRD and an integration API between Services Toolkit,
  Crossplane and AppSSO.
  For more information, see [XWorkloadRegistration API](app-sso/reference/api/xworkloadregistration.hbs.md).

#### <a id='1-6-0-bitnami-services'></a> Bitnami Services

The `bitnami.services.tanzu.vmware.com` package v0.2.0 includes the following:

- New services available: MongoDB and Kafka

#### <a id='1-6-0-crossplane'></a> Crossplane

The `crossplane.tanzu.vmware.com` package v0.2.1 includes the following:

- Includes updates to the following software components:

  - Updates Universal Crossplane (UXP) to v1.12.1-up.1, which includes new Crossplane features such
    as ObserveOnly resources, Composition Validation, and Pluggable Secret Stores.
    For the full release notes, see
    [universal-crossplane releases](https://github.com/upbound/universal-crossplane/releases/tag/v1.12.1-up.1)
    in GitHub.
  - Updates provider-helm to v0.15.0. For the full release notes, see
    [provider-helm releases](https://github.com/crossplane-contrib/provider-helm/releases/tag/v0.15.0)
    in GitHub.
  - Updates provider-kubernetes to v0.8.0. For the full release notes, see
    [provider-kubernetes releases](https://github.com/crossplane-contrib/provider-kubernetes/releases/tag/v0.8.0)
    in GitHub.

  For more information about versions of software comprising the Crossplane package, See
  [Version matrix for Crossplane](./crossplane/reference/version-matrix.hbs.md).

- The Crossplane package now more gracefully handles situations in which Crossplane is already
  installed to a cluster by using another method, for example, Helm install.
  For more information, see [Use your existing Crossplane installation](crossplane/how-to-guides/use-existing-crossplane.hbs.md).

- Includes kapp wait rules that match on `Healthy=True` for the Providers.
  This means that package installation now waits for the Providers to become healthy before reporting
  success.

- Adds support for installing Providers in environments that use custom CA certificates.

- Adds the `orphan_resources` package value to allow you to configure whether to orphan all Crossplane
  CRDs, providers, and managed resources when the package is uninstalled. Optional, defaults to `true`.

  **Caution**: setting this value to `false` causes all Crossplane CRDs, providers, and managed
  resources to be deleted when the `crossplane.tanzu.vmware.com` package is uninstalled.
  This might also cause any existing service instances also being deleted.
  For more information, see [Delete Crossplane resources when you uninstall Tanzu Application Platform](./crossplane/how-to-guides/delete-resources.hbs.md)

#### <a id='1-6-0-flux-sc'></a> FluxCD Source Controller

Flux Source Controller v0.36.1-build.2 release includes the following API changes:

- `GitRepository` API

    - `spec.ref.name` is the reference value for Git checkout. It takes precedence over Branch,
    Tag and SemVer, It must be a valid
    [Git reference](https://git-scm.com/docs/git-check-ref-format#_description).

        Examples:

        - `"refs/heads/main"`
        - `"refs/tags/v0.1.0"`
        - `"refs/pull/420/head"`
        - `"refs/merge-requests/1/head"`

    - `status.artifact.digest` represents the value of the file in the form of `ALGORITHM:CHECKSUM`.
    - `status.observedIgnore` represents the latest `spec.ignore` value. It indicates the ignore
    rules for building the current artifact in storage.
    - `status.observedRecurseSubmodules` represents the latest `spec.recurseSubmodules` value
    during the latest reconciliation.
    - `status.observedInclude` represents the list of `GitRepository` resources that produces
    the current artifact.

- `OCIRepository` API

    - `spec.layerSelector` specifies which layer is extracted from an OCI Artifact.
    This field is optional and set to extracting the first layer in the artifact by default.
    - `spec.verify` includes the secret name that holds the trusted public keys for signature verification.
    It also indicates the provider responsible for validating the authenticity of the OCI image.
    - `spec.insecure` enables connections to a non-TLS HTTP container image registry.

- `HelmChart` API

    - Add the new field `spec.verify`, which includes the secret name that holds
    the trusted public keys for signature verification.
    It also indicates the provider responsible for validating the authenticity of the OCI image.
    This field is only supported when using the HelmRepository source with the `spec.type` OCI.
    Chart dependencies, which are not bundled in the umbrella chart artifact, are not verified.

- `HelmRepository` API

    - Add the new field `spec.provider` for authentication purposes. Supported values are
    `aws`, `azure`, `gcp` or `generic`.
    `generic` is its default value. This field is only required when the `.spec.type` field is set to `oci`

- `Bucket` API

    - Add the new field `status.observedIgnore` which represents the latest `spec.ignore` value.
    It indicates the ignore rules for building the current artifact in storage.

#### <a id='1-6-0-namespace-provisioner-new-features'></a> Namespace Provisioner

- Implemented the capability to skip the creation of certain Out of the Box resources for the Namespace provisioner,
  providing greater flexibility for customization.
  - Enabled [easy deactivation of the default installation of the Grype scanner](namespace-provisioner/use-case4.hbs.md#deactivate-grype-install)
    by utilizing the `default_parameters` in the `tap-values.yaml` file or by utilizing namespace parameters.
  - Enhanced support for adding `secrets` and `imagePullSecrets` to the service account used by the Supply chains
    and Delivery components. This can be achieved using either `default_parameters` or namespace-level parameters.
    See [Customization Documentation](namespace-provisioner/use-case4.hbs.md#customize-service-accounts) for more information.
  - Introduced the option to [disable the creation of the LimitRange](namespace-provisioner/use-case4.hbs.md#deactivate-limitrange-setup)
    object out of the box in `full`, `iterate`, and `run` profile clusters.
- Added support for passing lists or objects via annotations for complex namespace parameters, simplifying the
  configuration process. More details on how to utilize this feature can be found in
  the [Reference Documentation](namespace-provisioner/parameters.hbs.md).
- The `path` value in `additional_sources` is now automatically generated, eliminating the need for users to
  provide it manually. This simplifies the configuration of external sources.


#### <a id='1-6-0-stk'></a> Services Toolkit (STK)

The `services-toolkit.tanzu.vmware.com` package v0.11.0 includes the following:

- Adds Kubernetes events to make debugging easier:
  - Normal events: CreatedCompositeResource, DeletedCompositeResource, ClaimableInstanceFound, NoClaimableInstancesFound
  - Warning events: ParametersValidationFailed, CompositeResourceDeletionFailed
- Updates reconciler-runtime to v0.11.1.

The Tanzu Service CLI plug-in v0.7.0 includes the following:

- The Tanzu Service plug-in is now compiled using the new tanzu CLI runtime (v0.90.0).
- No new features or changes to existing commands.

#### <a id='1-6-0-scst-scan'></a> Supply Chain Security Tools - Scan

- The source scanning step is removed from the out-of-box test and scan supply chain. For information about how to add the source scanning step to the test and scan supply chain, see [Scan Types for Supply Chain Security Tools - Scan](scst-scan/scan-types.hbs.md#source-scan).
- [Supply Chain Security Tools - Scan 2.0](scst-scan/app-scanning-beta.hbs.md) is promoted from `alpha` to `beta`.  This promotion primarily includes capabilities to integrate the SCST-Scan 2.0 component with other components of the Tanzu Application Platform, including: 
  - The ability to [enable](scst-scan/integrate-app-scanning.hbs.md#adding-app-scanning-to-default-test-and-scan-supply-chain) Supply Chain Security Tools (SCST) - Scan 2.0 in the out-of-the-box test and scan supply chain.
  - [AMR Observer (Alpha)](scst-store/amr/overview.hbs.md#amr-observer) observes scan results from SCST - Scan 2.0 and archives them to the [AMR (beta)](scst-store/amr/architecture.hbs.md) for long-term storage and reporting, and use by other Tanzu Application Platform Components.
  - Results from image scans with SCST - Scan 2.0 are now available in [Supply Chain Choreographer](tap-gui/plugins/scc-tap-gui.hbs.md) and [Security Analysis](tap-gui/plugins/sa-tap-gui.hbs.md) plug-ins for the Tanzu Developer Portal.
  - [Sample scan templates](scst-scan/ivs-custom-samples.hbs.md) are created to help users get started with examples of how to bring your own scanner.
    - [Carbon Black](scst-scan/ivs-carbon-black.hbs.md)
    - [Snyk](scst-scan/ivs-snyk.hbs.md)
    - [Prisma](scst-scan/ivs-prisma.hbs.md)
    - [Trivy](scst-scan/ivs-trivy.hbs.md)
    - [Grype](scst-scan/ivs-grype.hbs.md)
  - VMware encourages feedback about SCST - Scan 2.0. Email your Tanzu representative or [contact us here](https://tanzu.vmware.com/application-platform).

#### <a id='1-6-0-scst-store'></a> Supply Chain Security Tools - Store

- New report feature that links all packages, vulnerabilities, and ratings
  associated from a specific vulnerability scan SBOM to a Store report. When
  querying a report, it returns information linked to the original SBOM report
  instead of returning the aggregated data of all reports for the linked image
  or source.
  - `POST /api/v1/images` and `POST /api/v1/sources` APIs updated
    - New optional header request fields:
      - `Report-UID`: A unique identifier to assign to the report. If omitted, a
        unique identifier is randomly generated for the report. Supported
        characters: ALPHA DIGIT "-" / "." / "_" / "~".
      - `Original-Location`: The stored location of the original SBOM
        vulnerability scan result used to create this report.
    - New response field returned `ReportUID`, the report's unique identifier
      associated with the data submitted by this image.
  - `POST /api/v1/artifact-groups` API updated
    - New `ReportUID` optional body payload field which links an existing
      report, tagged by its UID, to this artifact group
  - New `GET /api/v1/report/{ReportUID}` API gets a specific report by its
    unique identifier.
  - New `GET /api/v1/reports` API queries for a list of reports with specified
    image digest, source SHA, or original location.
    - **Note**: When you request SPDX or CycloneDX format, the report date is
      set to the date of the original vulnerability scan SBOM. In addition, the
      tooling section includes the tool used to generate the original
      vulnerability scan report, if provided, and SCST - Store.
- Artifact Metadata Repository Observer (alpha). For more information, see the [Artifact Metadata Repository Overview](./scst-store/amr/overview.hbs.md)
  - Registers the cluster's location using user defined labels and the kube-system UID as the reference
  - Observe ImageVulnerabilityScan CustomResources from [SCST - Scan 2.0 package](scst-scan/app-scanning-beta.hbs.md)
  - Observe workload ReplicaSets which are ReplicaSets that have a container named workload as it is produced by the Out of the Box SupplyChains.
  - Sends CloudEvents for observed resources to the Artifact Metadata Repository CloudEvent Handler

- Artifact Metadata Repository CloudEvent Handler (alpha). For more information, see the [Artifact Metadata Repository Overview](./scst-store/amr/overview.hbs.md)
  - Artifact Metadata Repository Persister naming is being deprecated in favor of Artifact Metadata Repository CloudEvent Handler
  - Handles ImageVulnerabilityScan configured CloudEvents from the Artifact Metadata Repository Observer
  - Handles Location configured CloudEvents from the Artifact Metadata Repository Observer
  - Handles ReplicaSet configured CloudEvents from the Artifact Metadata Repository Observer

#### <a id='1-6-0-intellij-ext'></a> Tanzu Developer Tools for IntelliJ

- Added support for Local Source Proxy that eliminates the need to provide source image configuration
  for rapid iteration in the inner loop
- Tanzu Developer Tools for IntelliJ can now be used to rapidly iterate on Spring-native applications.
  Developers can Live Update and debug spring-native applications non-natively and then deploy
  to a cluster as a native image.
- Developers can now use Tanzu Developer Tools for IntelliJ to rapidly iterate and build Gradle
  projects in their preferred IDE

#### <a id='1-6-0-vscode-ext'></a> Tanzu Developer Tools for VS Code

- Added support for Local Source Proxy that eliminates the need to provide source image configuration
  for rapid iteration in the inner loop
- Tanzu Developer Tools for IntelliJ can now be used to rapidly iterate on Spring-native applications.
  Developers can Live Update and debug spring-native applications non-natively and then deploy
  to a cluster as a native image.
- Developers can now use Tanzu Developer Tools for IntelliJ to rapidly iterate and build Gradle
  projects in their preferred IDE

#### <a id='1-6-0-cnrs'></a> Cloud Native Runtimes

- New `default_external_scheme` configuration option:
  - Configures `default-external-scheme` on Knative's `config-network` ConfigMap with a default scheme you can use for Knative Service URLs. Supported values are either `http` or `https`. You cannot set this option at the same time as the `default_tls_secret` option.

#### <a id='1-6-0-contour'></a> Contour

- Add new parameters to specify `contour` and `envoy` resources requests and limits for CPU and memory. For more information, see [Install Contour](contour/install.hbs.md).
- For more information about the new features in v1.24.4, see [Contour release notes](https://github.com/projectcontour/contour/releases/tag/v1.24.4) in GitHub.
---

### <a id='1-6-0-breaking-changes'></a> Breaking changes

This release includes the following changes, listed by component and area.

#### <a id='1-6-0-apps-cli-plugin-bc'></a> Apps plug-in for Tanzu CLI

- The deprecated `tanzu apps workload update` command is removed from the CLI.
  Use the command `tanzu apps workload apply` instead.

#### <a id='1-6-0-appsso-bc'></a> Application Single Sign-On (AppSSO)

- Consume AppSSO service offerings using `ClassClaim` instead of the lower-level `WorkloadRegistration`
  or `ClientRegistration`.
- Crossplane is an installation and runtime dependency of AppSSO.
- The field `AuthServer.spec.tls.disabled` is removed. Use `AuthServer.spec.tls.deactivated` instead.
- The field `ClientRegistration.spec.redirectURIs` no longer defaults to
  `["http://127.0.0.0:8080"]`.

#### <a id='1-6-0-flux-sc-bc'></a> FluxCD Source Controller

- The format of the `status.artifact.revision` value in the `GitRepository` resource's
  status field is updated from `BRANCH/CHECKSUM` to `BRANCH@sha1:CHECKSUM`.
    - Example: `main/6db88c7a7e7dec1843809b058195b68480c4c12a` to `main@sha1:6db88c7a7e7dec1843809b058195b68480c4c12a`.

#### <a id='1-6-0-buildservice-bc'></a> Tanzu Build Service

- The full dependencies package is renamed and the installation process is modified.
  - You must remove existing full dependencies installations before installing the new version.
  - You must provide the tap-values file during the full dependencies package installation.
- The full dependencies package repository is tagged with the Tanzu Application Platform package version instead of the Tanzu Build Service package version.
- The Ubuntu Bionic stack is no longer shipped in Tanzu Application Platform and the Full Dependencies Package Repository.

#### <a id='1-6-0-cnrs-bc'></a> Cloud Native Runtimes
- **`provider` config option**: The deprecation of the `provider` configuration option has been announced in the [release notes of Cloud Native Runtimes 2.0](https://docs.vmware.com/en/Cloud-Native-Runtimes-for-VMware-Tanzu/2.0/tanzu-cloud-native-runtimes/GUID-release-notes.html).
  As part of this release, the option has been removed completely.

#### <a id='1-6-0-tap-gui-bc'></a> Tanzu Developer Portal (formerly named Tanzu Application Platform GUI)
- **`allowGuestAccess` config option**: Previously this was not needed in the configuration and would default to allow users to login without credentials. In 1.6.x+ this has been changed to require explicitly allowing guest users. The recommended values files in the installation sections have been updated to include this setting.

  Add the following lines to your `tap-values.yaml` in order to enable guest access explicitly:

  ```yaml
  #Existing tap-values.yaml settings
  tap_gui:
    app_config:
      auth:
        allowGuestAccess: true  #This will allow unauthenticated users to login to your portal. If you want to disable, make sure you configure an alternate auth provider.
  ```

---

### <a id='1-6-0-security-fixes'></a> Security fixes

This release has the following security fixes, listed by component and area.

#### <a id='1-6-0-COMPONENT-NAME-fixes'></a> COMPONENT-NAME

- Security fix description.

---

### <a id='1-6-0-resolved-issues'></a> Resolved issues

The following issues, listed by component and area, are resolved in this release.

#### <a id='1-6-0-apps-cli-plugin-ri'></a> Apps plug-in for Tanzu CLI

- Implemented validations to prevent the inclusion of multiple sources through flags in the `workload create`
  and `workload apply` commands.
- Modified the behavior of the commands when waiting to apply workload changes. If the workload was previously
  in a failed state, it will no longer immediately fail. When the `--wait` flag is used, the command will continue
  to wait until the workload either succeeds or fails again. When the `--tail` flag is used, the command will keep
  tailing logs from the Supply chain steps that were impacted by the workload update.

#### <a id='1-6-0-crossplane-ri'></a> Crossplane

- The Crossplane package now more gracefully handles situations in which Crossplane is already
  installed to a cluster by using another method, for example, Helm install.

  Previously the Crossplane Package assumed that Crossplane was not already installed on the cluster,
  which is not always true.
  Rather than fail, the package completed installing, which caused non-deterministic behavior.

  Now, if you attempt to install or upgrade the Crossplane package on a cluster that has
  Crossplane installed by other means, it fails with the error `Resource already exists`.
  In such cases, you can either exclude the Crossplane package from the Tanzu Application Platform
  installation, or set `adopt_resources` to true in the Crossplane package to adopt resources from
  your existing installation.
  For more information, see [Use your existing Crossplane installation](crossplane/how-to-guides/use-existing-crossplane.hbs.md).

#### <a id='1-6-0-namespace-provisioner-ri'></a> Namespace Provisioner

- Resolved an issue that prevented updates to the AWS IAM role from reflecting in the Service
  accounts utilized by Supply chains and Delivery components.
- Fixed a behavior where the Namespace provisioner would encounter failure if the same git secret
  was used multiple times within the `additional_sources` section of the `tap-values.yaml` file.
  **NOTE: This fix requires Cluster Essentials 1.6 or higher installed on the cluster.**
- Resolved an issue where a Namespace managed by the Namespace provisioner would become stuck in
  the `Terminating` phase during deletion if it contained a workload.
  **NOTE: This fix requires Cluster Essentials 1.6 or higher installed on the cluster.**

#### <a id='1-6-0-stk-ri'></a> Services Toolkit

- Resolved an issue that prevented the default cluster-admin IAM role on GKE clusters from claiming
  any of the Bitnami services.

  Previously, if a user with the cluster-admin role on a GKE cluster attempted to claim any of the
  Bitnami services, they received a validation error.

- Resolved an issue affecting the dynamic provisioning flow if you used a CompositeResourceDefinition
  that specified a schema that defined `.status` without also defining `.spec`.
  You can now use a CompositeResourceDefinition which only specifies `.status` in the schema.

  Previously, if you attempted to create a ClassClaim for a ClusterInstanceClass that referred to
  such a CompositeResourceDefinition, the ClassClaim did not transition into `Ready=True` and
  instead reported `unexpected end of JSON input`.

#### <a id='1-6-0-intellij-plugin-ri'></a> Tanzu Developer Tools for IntelliJ

- The `apply` action no longer stores the workload file path, which prevented modifying the workload
  file path later. Now this information is either computed or obtained by prompting the user as needed.

- In the Tanzu Activity Panel, the `config-writer-pull-requester` of the type `Runnable` is no longer
  incorrectly categorized as **Unknown**.

#### <a id='1-6-0-cnrs-ri'></a> Cloud Native Runtimes

- New toggle feature for how to make ConfigMap updates
  - For some ConfigMaps in Cloud Native Runtimes, such as config-features, the option to update using an overlay was not taking effect. This issue is fixed. With this version, the legacy behavior remains the same, but VMware introduced a configuration to opt-in into updating ConfigMaps using overlays in Cloud Native Runtimes. To configure this option, edit your `cnr-values.yaml` file to change the following configuration:

```yaml
allow_manual_configmap_update: false
```

---

### <a id='1-6-0-known-issues'></a> Known issues

This release has the following known issues, listed by component and area.

#### <a id='1-6-0-scc-ki'></a> Supply Chain Choreographer

- If the size of the resulting OpenAPIv3 specification exceeds a certain size, roughly 3KB, the Supply Chain does not function. If the operator is using the default Carvel Package parameters, they are fine with this value enabled. If they use custom Carvel Package parameters, they might run into this size limit. If they exceed the size limit, they can either deactivate this feature, or use a workaround. The workaround requires enabling a Tekton feature flag. See the [Tekton documentation](https://tekton.dev/docs/pipelines/additional-configs/#enabling-larger-results-using-sidecar-logs).

#### <a id='1-6-0-tap-gui-ki'></a> Tanzu Developer Portal (formerly named Tanzu Application Platform GUI)

- Ad-blocking browser extensions and standalone ad-blocking software can interfere with telemetry
  collection within the VMware
  [Customer Experience Improvement Program](https://www.vmware.com/solutions/trustvmware/ceip.html)
  and restrict access to all or parts of Tanzu Developer Portal.
  For more information, see [Troubleshooting](tap-gui/troubleshooting.hbs.md#ad-block-interference).

#### <a id='1-6-0-intellij-plugin-ki'></a> Tanzu Developer Tools for IntelliJ

- The error `com.vdurmont.semver4j.SemverException: Invalid version (no major version)` is shown in
  the error logs when attempting to perform a workload action before installing the Tanzu CLI apps
  plug-in.

- If you restart your computer while running Live Update without terminating the Tilt
  process beforehand, there is a lock that incorrectly shows that Live Update is still running and
  prevents it from starting again.
  For the fix, see [Troubleshooting](intellij-extension/troubleshooting.hbs.md#lock-prevents-live-update).

- Workload actions and Live Update do not work when in a project with spaces in its name, such as
  `my app`, or in its path, such as `C:\Users\My User\my-app`.
  For more information, see [Troubleshooting](intellij-extension/troubleshooting.hbs.md#projects-with-spaces).

- An **EDT Thread Exception** error is logged or reported as a notification with a message similar to
  `"com.intellij.diagnostic.PluginException: 2007 ms to call on EDT TanzuApplyAction#update@ProjectViewPopup"`.
  For more information, see
  [Troubleshooting](intellij-extension/troubleshooting.hbs.md#ui-liveness-check-error).

#### <a id='1-6-0-amr-observer-cloudevent-handler'></a> Artifact Metadata Repository Observer and CloudEvent Handler
- Periodic reconciliation or restarting of the AMR Observer causes reattempted posting of ImageVulnerabilityScan results. There is an error on duplicate submission of identical ImageVulnerabilityScans which can be ignored so long as the previous submission was successful.
- ReplicaSet status in Artifact Metadata Repository only has two states, `created` and `deleted`. There is a known issue where the `available` and `unavailable` state is not showing. The workaround is that this information can be interpolated from the `instances` metadata in the AMR for the ReplicaSet.
- For more information, see the [Artifact Metadata Repository Overview - Known Issues](./scst-store/amr/overview.hbs.md#known-issues)

#### <a id='1-6-0-cnrs-ki'></a> Cloud Native Runtimes
- Knative Serving: Certain app name, namespace, and domain combinations produce Knative Services with status `CertificateNotReady`. See [Troubleshooting](https://docs.vmware.com/en/Cloud-Native-Runtimes-for-VMware-Tanzu/2.3/tanzu-cloud-native-runtimes/troubleshooting.html#certificate-not-ready-kcert).

---

### <a id="1-6-components"></a> Component versions

The following table lists the supported component versions for this Tanzu Application Platform release.

| Component Name                                  | Version |
| ----------------------------------------------- | ------- |
| API Auto Registration                           |         |
| API portal                                      |         |
| API Scoring and Validation                      |         |
| Application Accelerator                         |         |
| Application Configuration Service               |         |
| Application Live View                           |         |
| Application Single Sign-On                      |         |
| Authentication and authorization                |         |
| Bitnami Services                                | 0.2.0   |
| Cartographer Conventions                        |         |
| cert-manager                                    |         |
| Cloud Native Runtimes                           |         |
| Contour                                         |         |
| Crossplane                                      | 0.2.1   |
| Developer Conventions                           |         |
| Eventing                                        | 2.2.3   |
| FluxCD Source Controller                        |         |
| Learning Center                                 |         |
| Local Source Proxy                              | 0.1.0   |
| Namespace Provisioner                           | 0.4.0   |
| Service Bindings                                | 0.9.1   |
| Services Toolkit                                | 0.11.0  |
| Source Controller                               |         |
| Spring Boot conventions                         |         |
| Spring Cloud Gateway                            |         |
| Supply Chain Choreographer                      |         |
| Supply Chain Security Tools - Policy Controller |         |
| Supply Chain Security Tools - Scan              |         |
| Supply Chain Security Tools - Sign (Deprecated) |         |
| Supply Chain Security Tools - Store             |         |
| Tanzu Developer Portal (formerly named Tanzu Application Platform GUI)                  |         |
| Tanzu Application Platform Telemetry            |         |
| Tanzu Build Service                             |         |
| Tanzu CLI plug-in                               |         |
| Tanzu Developer Tools for IntelliJ              |         |
| Tanzu Developer Tools for Visual Studio         |         |
| Tanzu Developer Tools for VS Code               |         |
| Tanzu Service CLI plug-in                       | 0.7.0   |
| Tekton Pipelines                                |         |

---

## <a id="1-6-deprecations"></a> Deprecations

The following features, listed by component, are deprecated.
Deprecated features will remain on this list until they are retired from Tanzu Application Platform.

### <a id="1-6-alv-deprecations"></a> Application Live View

- `appliveview_connnector.backend.sslDisabled` is deprecated and marked for removal in
  Tanzu Application Platform v1.7.0.
  For more information about the migration, see [Deprecate the sslDisabled key](app-live-view/install.hbs.md#deprecate-the-ssldisabled-key).

#### <a id='1-6-0-apps-cli-plugin-deprecations'></a> Apps plug-in for Tanzu CLI

- The default value for the `--update-strategy` flag will change from merge to replace in
  Tanzu Application Platform v1.7.0

### <a id='1-6-app-sso-deprecations'></a> Application Single Sign-On (AppSSO)

- `ClientRegistration` resource `clientAuthenticationMethod` field values
  `post` and `basic` are deprecated and marked for removal in Tanzu Application
  Platform v1.7.0. Use `client_secret_post` and `client_secret_basic` instead.

### <a id="1-6-flux-sc-deprecations"></a> FluxCD Source Controller

- Deprecations for the `GitRepository` API:

    - `spec.gitImplementation` is deprecated.
    `GitImplementation` defines the Git client library implementation.
    `go-git` is the default and only supported implementation. `libgit2`
    is no longer supported.
    - `spec.accessFrom` is deprecated. `AccessFrom`, which defines an Access
    Control List for enabling cross-namespace references to this object, was never
    implemented.
    - `status.contentConfigChecksum` is deprecated in favor of the explicit fields
    defined in the observed artifact content config within the status.
    - `status.artifact.checksum` is deprecated in favor of `status.artifact.digest`.
    - `status.url` is deprecated in favor of `status.artifact.url`.

- Deprecations for the `OCIRepository` API:

    - `status.contentConfigChecksum` is deprecated in favor of the explicit fields
    defined in the observed artifact content config within the status.

### <a id="1-6-stk-deprecations"></a> Services Toolkit

- The `tanzu services claims` CLI plug-in command is now deprecated. It is
  hidden from help text output, but continues to work until officially removed
  after the deprecation period. The new `tanzu services resource-claims` command
  provides the same function.

### <a id='1-6-0-scc-deprecations'></a> Supply Chain Choreographer

- Supply Chain Choreographer no longer uses the `git_implementation` field. The `go-git` implementation now assumes that `libgit2` is not supported.
  - FluxCD no longer supports the `spec.gitImplementation field` [as of version 0.33.0](https://github.com/fluxcd/source-controller/blob/main/CHANGELOG.md#0330)
  - Existing references to `git_implementation` field are ignored and references to `libgit2` do not cause failures. This is assured up to Tanzu Application Platform v1.9.0
  - Azure DevOps works without specifying `git_implementation` in Tanzu Application Platform v1.6.0

### <a id="1-6-scst-scan-deprecations"></a> Supply Chain Security Tools (SCST) - Scan

- The `docker` field and related sub-fields used in SCST -
  Scan are deprecated and marked for removal in Tanzu Application Platform
  v1.7.0.

   The deprecation impacts the following components: Scan Controller, Grype Scanner, and Snyk Scanner.
   Carbon Black Scanner is not impacted.
   For information about the migration path, see
   [Troubleshooting](scst-scan/observing.hbs.md#unable-to-pull-scanner-controller-images).

- The profile based installation of Grype to a developer namespace and related
  fields in the values file, such as `grype.namespace` and
  `grype.targetImagePullSecret`, are deprecated and marked for removal in Tanzu
  Application Platform v1.8.0.

   VMware recommends using the namespace provisioner to populate namespaces with
   all the required resources, including the Grype installation.  For
   information about how to use namespace provisioner to populate a namespace
   with SCST - SCST scan, see [Setup for OOTB Supply
   Chains](namespace-provisioner/ootb-supply-chain.hbs.md#test-scan).

### <a id="1-6-tbs-deprecations"></a> Tanzu Build Service

- The Ubuntu Bionic stack is deprecated: Ubuntu Bionic stops receiving support in April 2023.
  VMware recommends you migrate builds to Jammy stacks in advance.
  For how to migrate builds, see [Use Jammy stacks for a workload](tanzu-build-service/dependencies.md#using-jammy).

- The Cloud Native Buildpack Bill of Materials (CNB BOM) format is deprecated.
  VMware plans to deactivate this format by default in Tanzu Application Platform v1.5.0 and remove
  support in Tanzu Application Platform v1.6.0.
  To manually deactivate legacy CNB BOM support, see [Deactivate the CNB BOM format](tanzu-build-service/install-tbs.md#deactivate-cnb-bom).

### <a id="1-6-apps-plugin-deprecations"></a> Tanzu CLI Apps plug-in

- The default value for the
  [--update-strategy](./cli-plugins/apps/command-reference/workload_create_update_apply.hbs.md#update-strategy)
  flag will change from `merge` to `replace` in Tanzu Application Platform v1.7.0.

- The `tanzu apps workload update` command is deprecated and marked for removal
  in Tanzu Application Platform v1.6.0. Use the command `tanzu apps workload apply` instead.


### <a id="1-6-tanzu-sc-deprecations"></a> Tanzu Source Controller

- The Tanzu Source Controller `ImageRepository` API is deprecated and is marked for
  removal in Tanzu Application Platform v1.9. Use the `OCIRepository` API instead.
  The Flux Source Controller installation includes the `OCIRepository` API.
  For more information about the `OCIRepository` API, see the
  [Flux documentation](https://fluxcd.io/flux/components/source/ocirepositories/).
