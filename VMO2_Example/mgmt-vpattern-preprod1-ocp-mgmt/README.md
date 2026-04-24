# Validated Patterns for Telco Hub OpenShift Clusters

This repository is in charge of applying day 1 and day 2 configurations to Telco OpenShift clusters using the Validated Patterns framework approach.This framework follow Telco Network Cloud (TNC) v5.0 with specifications for OpenShift 4.18.

Validated Patterns are an evolution of how you deploy applications in a hybrid cloud. With a pattern, you can automatically deploy a full application stack through a GitOps-based framework. With this framework, you can create business-centric solutions while maintaining a level of Continuous Integration (CI) over your application.

The following table provide information about what are the expected variables inside values-hub.yaml alongside a example.

## Expected variables inside values-hub.yaml

| Variable                              | Description                                                                                                    | Example                                                         |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| `clusterGroup.nodes[n]` | List of nodes that allows you to add labels.          | `m-m00.mgmt2.dc.domain.es` |
| `mgmt.cluster.name`                   | The name of the management cluster.                                                                           | `mgmt2`                                                         |
| `mgmt.cluster.location`               | Physical or logical location of the management cluster.                                                        | `dc`                                                            |
| `mgmt.cluster.domain`                 | Domain used for the management cluster.                                                                       | `domain.es`                                                     |
| `mgmt.cluster.enableUnsealVault`      | Enables or disables the automatic unseal functionality for Vault. If there's no Vault in place set it to false.                                             | `false`                                                         |
| `mgmt.cluster.mgmt_location`          | Specific management location, such as main data center.                                          | `mgmt1`                                                       |
| `mgmt.authentication.htpasswd.admin`  | Admin password hash for HTPasswd authentication.                                                               | `""`                                                            |
| `mgmt.authentication.ldap.bind_password` | Password for the LDAP bind user.                                                                            | `your_bind_password`                                            |
| `mgmt.authentication.ldap.url`        | URL of the LDAP server for authentication.                                                                     | `idm-serv.mgmt2.dc.domain.es`                                   |
| `mgmt.authentication.ldap.bind_dn`    | Distinguished Name (DN) for binding to the LDAP server.                                                        | `uid=ocp-bind-user,cn=users,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es` |
| `mgmt.authentication.ldap.groups_base_dn` | Base DN for LDAP groups.                                                                                   | `cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es`          |
| `mgmt.authentication.ldap.users_base_dn` | Base DN for LDAP users.                                                                                    | `cn=users,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es`           |
| `mgmt.authentication.ldap.group_membership` | Specific LDAP group that allows access to the management cluster.                                         | `cn=ocpusers,cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es` |
| `mgmt.authentication.ldap.groups_whitelist` | List of LDAP groups with access to the cluster.                                                          | `[ "cn=ocpusers,cn=groups,...", "cn=ocpadmins,...", "cn=ocpreaders,..." ]` |
| `mgmt.authentication.ldap.sync_schedule` | Cron schedule for syncing LDAP groups and users.                                                          | `"*/15 * * * *"`                                                |
| `mgmt.authentication.ldap.crt`        | Certificate file for LDAP server connection.                                                                  | `/etc/pki/tls/certs/ldap.crt`                                   |
| `mgmt.apps.provisioner_ip`                    | IP address of the provisioner for the applications namespace.                                             | `IP_ADDRESS_13`                            |
| `mgmt.apps.ns`                                | Namespace where the application resources will be deployed.                                               | `mano-apps`                                |
| `mgmt.apps.nad_name`                          | Name of the NetworkAttachmentDefinition (NAD) used by the applications.                                   | `apps-nad`                                 |
| `mgmt.apps.subnet`                            | IP subnet allocated for applications.                                                                     | `IP_ADDRESS_14`                            |
| `mgmt.apps.subnet_len`                        | Length of the subnet mask for the application IP range.                                                   | `26`                                       |
| `mgmt.apps.subnet_gw`                         | Gateway IP for the applications subnet.                                                                   | `IP_ADDRESS_15`                            |
| `mgmt.apps.domain`                            | Domain for the applications within the management cluster.                                                | `mgmt2.dc.domain.es`            |
| `mgmt.apps.dns_server_ip`                     | DNS server IP address for applications.                                                                   | `IP_ADDRESS_16`                            |
| `mgmt.apps.imageSourceRegistry`                     | Source QCOW image                                                                   | `docker://quay.example.com/org/rhel-vm:9.6`                            |
| `mgmt.apps.imageSourceSecret`                     | Secret name containing access credential to QCOW source                                                                    | `qcow-robot-account`                            |
| `mgmt.apps.imageSourceAccessKeyID`                     | User to access the QCOW                                                                   | `org+qcow`                            |
| `mgmt.apps.imageSourceSecretKey`                     | Password to access the QCOW                                                                    | `HFJSHKJDSKFLLF...`                            |
| `mgmt.capsule.qcow`                      | Path to the QCOW2 image for the Capsule server.                                        | `iso/rhel-9.6-x86_64-kvm.qcow2`        |
| `mgmt.capsule.uuid`                      | Unique identifier for the Capsule server. You can use $ uuidgen to get a random UUID.                                              | `BF308E89-331E-428B-979F-161B6E9ABD84`          |
| `mgmt.capsule.app_name`                  | Application name of the Capsule server.                                                | `sat-server`                                    |
| `mgmt.capsule.domain`                    | Domain of the Capsule server.                                                          | `mgmt2.dc.domain.es`                            |
| `mgmt.capsule.user`                      | Username for accessing the Capsule server.                                             | `admin`                                         |
| `mgmt.capsule.password`                  | Password for accessing the Capsule server.                                             | `admin`                                      |
| `mgmt.capsule.ip`                        | IP address of the Capsule server.                                                      | `IP_ADDRESS_17`                                 |
| `mgmt.capsule.hostname`                  | Fully qualified domain name (FQDN) for the Capsule server.                             | `capsule.mgmt2.dc.domain.es`                  |
| `mgmt.capsule.ssh_authorized_key`        | SSH authorized key for accessing the Capsule server.                                   | `"~/.ssh/id_rsa.pub"`                                            |
| `mgmt.kafka.topics[n]`                        | List of Kafka topics for log management and metrics.                                          | `["rsyslog-test", "stf-metrics", "mano1-ocp-metrics"]` |  
| `mgmt.gitops.ztp_plugin_image`                  | Image for the ZTP (Zero-Touch Provisioning) plugin.                                                          | `registry.redhat.io/openshift4/ztp-site-generate-rhel8:v4.14.4` |
| `mgmt.gitops.ztp_instance_ns`                   | Namespace for the ZTP instance.                                                                              | `ztp`                                                        |
| `mgmt.gitops.openshift_gitops_api_version`      | API version of OpenShift GitOps.                                                                             | `argoproj.io/v1alpha1`                                       |
| `mgmt.gitops.multicluster_operators_subscription` | Image for the multicluster operators subscription.                                                            | `registry.redhat.io/rhacm2/multicluster-operators-subscription-rhel8:v2.7` |
| `mgmt.gitops.repoURL`                           | URL of the GitOps repository.                                                                                | `https://gitlab.cicd.mgmt2.dc.domain.es/gitops/core-ztp.git` |
| `mgmt.gitops.core_ztp_repoToken`                | Authentication token for the core ZTP GitOps repository.                                                     | `glpat-example-kla`                                          |
| `mgmt.gitops.targetRevision`                | Branch containiz ztp definitions.                                                     | `your_branch`                                          |
| `mgmt.ztp.jobTerminationGracePeriod`            | Grace period for job termination in seconds.                                                                 | `300`                                                        |
| `mgmt.ztp.serviceAccountName`                   | Name of the service account used for ZTP jobs.                                                               | `mce-prereq-sa`                                              |
| `mgmt.ztp.rbac.roles[n].name`                   | Name of the role for ZTP RBAC configuration.                                                                 | `mce-prereq`                                                 |
| `mgmt.ztp.rbac.roles[n].createRole`             | Whether to create the role for ZTP RBAC configuration.                                                       | `true`                                                       |
| `mgmt.ztp.rbac.roles[n].apiGroups[j]`              | List of API groups for the RBAC role.                                                                        | `['""', 'metal3.io']`                                        |
| `mgmt.ztp.rbac.roles[n].scope.cluster`          | Indicates whether the role applies at the cluster level.                                                     | `true`                                                       |
| `mgmt.ztp.rbac.roles[n].resources[j]`              | List of resources for the RBAC role permissions.                                                             | `["namespace", "configmaps", "provisionings", "secrets"]`    |
| `mgmt.ztp.rbac.roles[n].verbs[j]`                  | List of actions allowed by the role (e.g., get, list, patch).                                                | `["get", "list", "patch", "update", "create", "edit"]`       |
| `mgmt.ztp.rbac.roleBindings[n].name`            | Name of the role binding for ZTP RBAC configuration.                                                         | `mce-prereq-rolebinding`                                     |
| `mgmt.ztp.rbac.roleBindings[n].createBinding`   | Whether to create the role binding for ZTP RBAC configuration.                                               | `true`                                                       |
| `mgmt.ztp.rbac.roleBindings[n].scope.cluster`   | Indicates whether the role binding applies at the cluster level.                                             | `true`                                                       |
| `mgmt.ztp.rbac.roleBindings[n].namespace`       | Namespace in which the role binding applies, if not at the cluster level.                                    | `""`                                                         |
| `mgmt.ztp.rbac.roleBindings[n].subjects.kind`   | Kind of subject for the role binding (e.g., ServiceAccount).                                                 | `ServiceAccount`                                             |
| `mgmt.ztp.rbac.roleBindings[n].subjects.name`   | Name of the subject for the role binding.                                                                    | `mce-prereq-sa`                                              |
| `mgmt.ztp.rbac.roleBindings[n].subjects.namespace` | Namespace of the subject for the role binding.                                                                | `multicluster-engine`                                        |
| `mgmt.ztp.rbac.roleBindings[n].roleRef.kind`    | Kind of the referenced role (e.g., ClusterRole).                                                             | `ClusterRole`                                                |
| `mgmt.ztp.rbac.roleBindings[n].roleRef.name`    | Name of the referenced role.                                                                                 | `mce-prereq`                                                 |
| `mgmt.portworx.mgmtendpint`               | Portworx Management Endpoint            | `IP_ADDRESS_18`                              |
| `mgmt.portworx.apitoken`                | API Token for authentication            | `JKDKJFSLD...`                |
| `mgmt.portworx.realm`                   | Authentication realm                    | `my-auth-realm`                           |
| `mgmt.portworx.thanos_route`                     | Thanos Querier route endpoint           | `thanos-querier.apps.mycluster.com`       |
| `mgmt.portworx.dataInterface`                    | Data network interface name             | `bond0.100`                               |
| `mgmt.portworx.mgmtInterface`                    | Management network interface name       | `bond0.101`                                   |
| `mgmt.portworx.customImageRegistry`              | Custom image registry URL               | `registry.example.com/my-mirror`          |
| `mgmt.portworx.iscsiImage`                       | iSCSI support tools image               | `registry.example.com/org/tools:latest` |
| `mgmt.portworx.base_iscsiIQN`                    | Base iSCSI IQN prefix                   | `iqn.2024-01.com.example:my-cluster`      |
| `mgmt.portworx.pod`                    | Pod management configuration value      | `config-value-here`                       |
| `mgmt.portworx.registry_dockerconfigjson`        | Base64 encoded docker config            | `(Base64_encoded_json_string)`            |
| `mgmt.portworx.default_storageclass`             | Default StorageClass name               | `my-storage-class`                        |
| `mgmt.oadp.access_key`           | OADP S3 Access Key                      | `YOUR_S3_ACCESS_KEY`                      |
| `mgmt.oadp.secret_key`           | OADP S3 Secret Key                      | `YOUR_S3_SECRET_KEY`                      |
| `mgmt.oadp.region`               | OADP S3 Bucket Region                   | `us-west-2`                               |
| `mgmt.oadp.s3_uri`               | OADP S3 Bucket URL (endpoint)           | `s3.my-provider.com`                      |
| `mgmt.oadp.bucket`               | OADP S3 Bucket Name                     | `my-backup-bucket`                        |
| `mgmt.oadp.prefix`               | OADP S3 Path Prefix                     | `my-prefix`                               |
| `mgmt.nmstate.appsNetworks.nic1`        | Apps Network NIC 1                      | `ens3f0`                                  |
| `mgmt.nmstate.appsNetworks.nic2`        | Apps Network NIC 2                      | `ens3f1`                                  |
| `mgmt.nmstate.appsNetworks.mtu`         | Apps Network MTU Size                   | `8950`                                    |
| `mgmt.nmstate.storageNetworks[0].nodeName` | Node Hostname (example)                 | `worker-0.example.com`                    |
| `mgmt.nmstate.storageNetworks[0].vlan_id_FB` | Node FlashBlade VLAN ID                 | `100`                                     |
| `mgmt.nmstate.storageNetworks[0].ip_FB`   | Node FlashBlade Data IP                 | `IP_ADDRESS_19`                             |
| `mgmt.nmstate.storageNetworks[0].vlan_id_FA` | Node FlashArray VLAN ID                 | `200`                                     |
| `mgmt.nmstate.storageNetworks[0].ip_FA`   | Node FlashArray Data IP                 | `IP_ADDRESS_20`                             |
| `mgmt.quay.fqdn`                                | Fully qualified domain name for the Quay registry service.                                                                | `quay.apps.mgmt2.dc.domain.es`                                 |
| `mgmt.quay.components[n]`                          | List of Quay components with configuration options.                                                                      | `clair`, `postgres`, `objectstorage`, etc.                     |
| `mgmt.quay.components[].kind`                   | Type of Quay component being configured.                                                                                 | `clair`, `postgres`, `objectstorage`, `redis`, etc.            |
| `mgmt.quay.components[].managed`                | Indicates if the component is managed by the Quay Operator.                                                              | `true`, `false`                                                |
| `mgmt.quay.components[].overrides.volumeSize`   | Specifies the storage size for the component, if applicable.                                                             | `100Gi`, `500Gi`                                               |
| `mgmt.quay.param.FEATURE_USER_INITIALIZE`       | Enables initial user setup on first Quay startup.                                                                        | `true`                                                         |
| `mgmt.quay.param.BROWSER_API_CALLS_XHR_ONLY`    | Restricts API calls to XMLHttpRequest (XHR) only for browser requests.                                                   | `false`                                                        |
| `mgmt.quay.param.ALLOW_PULLS_WITHOUT_STRICT_LOGGING` | Allows image pulls without strict logging enabled.                                                                   | `false`                                                        |
| `mgmt.quay.param.DEFAULT_TAG_EXPIRATION`        | Default expiration time for image tags.                                                                                  | `2w`                                                           |
| `mgmt.quay.param.ENTERPRISE_LOGO_URL`           | URL for custom enterprise logo in Quay UI.                                                                              | `/static/img/RH_Logo_Quay_Black_UX-horizontal.svg`             |
| `mgmt.quay.param.FEATURE_BUILD_SUPPORT`         | Enables build support within Quay.                                                                                       | `false`                                                        |
| `mgmt.quay.param.FEATURE_DIRECT_LOGIN`          | Enables direct login to Quay without SSO.                                                                               | `true`                                                         |
| `mgmt.quay.param.FEATURE_MAILING`               | Enables mailing features in Quay.                                                                                        | `false`                                                        |
| `mgmt.quay.param.REGISTRY_TITLE`                | Full title displayed in Quay's UI.                                                                                       | `Red Hat Quay`                                                 |
| `mgmt.quay.param.REGISTRY_TITLE_SHORT`          | Shortened registry title displayed in UI.                                                                               | `Red Hat Quay`                                                 |
| `mgmt.quay.param.TAG_EXPIRATION_OPTIONS[n]`        | List of available tag expiration options.                                                                               | `2w`                                                           |
| `mgmt.quay.param.TEAM_RESYNC_STALE_TIME`        | Time interval for resyncing team memberships.                                                                           | `60m`                                                          |
| `mgmt.quay.param.SERVER_HOSTNAME`               | Hostname for Quay server, used in configurations and UI.                                                                 | `quay.apps.mgmt2.dc.domain.es`                                 |
| `mgmt.quay.param.TESTING`                       | Enables testing mode for Quay.                                                                                           | `false`                                                        |
| `mgmt.quay.param.DISTRIBUTED_STORAGE_CONFIG`                     | S3 object storage config to be used. Refer to the product documentation to get this information based on your needs.                                                                   | `radosGWStorage`                            |
| `mgmt.quay.param.AUTHENTICATION_TYPE`           | Type of authentication used for Quay.                                                                                    | `LDAP`                                                         |
| `mgmt.quay.param.LDAP_ADMIN_DN`                 | Distinguished Name (DN) for the LDAP admin user.                                                                         | `uid=quay-bind-user,cn=users,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es` |
| `mgmt.quay.param.LDAP_ADMIN_PASSWD`             | Password for LDAP admin user.                                                                                            | `vriESYGoV02AIsXoCZjhdw==`                                     |
| `mgmt.quay.param.LDAP_ALLOW_INSECURE_FALLBACK`  | Allows fallback to insecure LDAP connections if secure connections fail.                                                 | `true`                                                         |
| `mgmt.quay.param.LDAP_BASE_DN[n]`                  | Base DN used for LDAP searches.                                                                                          | `dc=mgmt2, dc=dc, dc=domain, dc=es`              |
| `mgmt.quay.param.LDAP_EMAIL_ATTR`               | LDAP attribute that stores user email addresses.                                                                         | `mail`                                                         |
| `mgmt.quay.param.LDAP_UID_ATTR`                 | LDAP attribute for the user ID.                                                                                          | `uid`                                                          |
| `mgmt.quay.param.LDAP_URI`                      | URI for connecting to the LDAP server.                                                                                   | `ldaps://idm-serv.mgmt2.dc.domain.es`                          |
| `mgmt.quay.param.LDAP_USER_RDN[n]`                 | Relative DN(s) used to locate users in LDAP.                                                                             | `cn=users`, `cn=accounts`                                      |
| `mgmt.quay.param.FEATURE_TEAM_SYNCING`          | Enables synchronization of team data with LDAP groups.                                                                   | `true`                                                         |
| `mgmt.quay.param.LDAP_USER_FILTER`              | LDAP filter to match users authorized to access Quay.                                                                    | `(memberOf=cn=quayusers,cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es)` |
| `mgmt.quay.param.LDAP_SUPERUSER_FILTER`         | LDAP filter to match users with superuser access in Quay.                                                                | `(memberOf=cn=quayadmins,cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es)` |
| `mgmt.quay.param.FEATURE_SUPERUSERS_FULL_ACCESS`| Grants superusers full access in Quay.                                                                                   | `true`                                                         |
| `mgmt.apiserver.tls.crt` | TLS certificate for the API server    | `LS0tLS1C...MEVBd0l3` |
| `mgmt.apiserver.tls.key` | TLS private key for the API server    | `LS0tLS1C...hQWxVSg` |
| `mgmt.ingress.tls.crt` | TLS certificate for Ingress             | `LS0tLS1C...MEVBd0l3` |
| `mgmt.ingress.tls.key` | TLS private key for Ingress             | `LS0tLS1C...hQWxVSg` |

## Authors
Paulo Pacifico <ppacific@redhat.com>
Juan Carlos Tovar <jtovarro@redhat.com>