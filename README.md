# 3scale-demo
Example Project on Red Hat 3Scale API Gateway

## Steps
* Install Red Hat Integration - 3scale operator
* In operator > API manager > create instance
  * Set wildcard domain to <base url of your cluster> (e.g., ocp4-bm.redhat.arrowlabs.be)
  * Set file system that allows ReadWriteMany => use persistent volume maarten-persistent-volume (see test.yaml)
  * Check resourceRequirementsEnabled
  * The dashboard shows the new portal URL of the tenant. As an example, if the <wildCardDomain> is 3scale-project.example.com, the Admin Portal URL is: https://3scale-admin.3scale-project.example.com.
* Install Red Hat SSO operator
* In operator > Keycloak > create instance

## Keycloak
* Get admin password
    ```shell
    oc get secret system-seed -n 3scale --template={{.data.ADMIN_PASSWORD}} | base64 -d; echo
    ```
* Login in keycloak 
    ```shell
    oc get route | grep keycloak
    ```
* Add realm '3scale'
* Add user roles SERVICE_A_V1_READ, SERVICE_A_2_READ, SERVICE_B_READ, SERVICE_C_READ
* Create user maarten - r3dhat and add user roles from above

## 3Scale - infra config
* Get master url
    ```shell
    oc get route | grep 3scale | grep master
    ```
* Get admin url
    ```shell
    oc get route | grep 3scale | grep admin
    ```
* Get admin password
    ```shell
    oc get secret system-seed --template={{.data.ADMIN_PASSWORD}} | base64 -d; echo
    ```
* Get master password
    ```shell
    oc get secret system-seed --template={{.data.MASTER_PASSWORD}} | base64 -d; echo
    ```


## 3scale
* Go to master
* Create new account 
  * demo-user
  * user@3cale-demo.be
  * 3scale
  * demo-organization
* Impersonate







https://a-client:wIswiVY60tTTxeQKKffCuysA8cBJ2zPv@keycloak-maarten-3scale.apps.cluster-rtplj.rtplj.sandbox2154.opentlc.com/auth/realms/3scale
https://zync-client:hYrtNUMC1hk3IvMjO34Eoch57z54UbZe@keycloak-maarten-3scale.apps.ocp4-bm.redhat.arrowlabs.be/auth/realms/3scale


echo -n | openssl s_client -connect keycloak-maarten-3scale.apps.ocp4-bm.redhat.arrowlabs.be:443 \
        -servername keycloak-maarten-3scale.apps.ocp4-bm.redhat.arrowlabs.be -showcerts | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > keycloak.pem

oc rsh zync-que-1-cjsht /bin/bash -c "cat /etc/pki/tls/cert.pem" > zync.pem 2>&1
cat keycloak.pem >> zync.pem




