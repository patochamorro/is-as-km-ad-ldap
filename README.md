# is-as-km-ad-ldap
Demo with WSO2 Identity Server and User Store managment


## Prepare the ldpa server with the required configuration
```
docker cp base-users1.ldif openldap1:/tmp/base-users.ldif
docker exec -it openldap1 ldapadd -x -D "cn=admin,dc=demo1,dc=org" -w admin -f /tmp/base-users.ldif

docker cp groups1.ldif openldap1:/tmp/groups.ldif
docker exec -it openldap1 ldapadd -x -D "cn=admin,dc=demo1,dc=org" -w admin -f /tmp/groups.ldif


docker cp base-users2.ldif openldap2:/tmp/base-users.ldif
docker exec -it openldap2 ldapadd -x -D "cn=admin,dc=demo2,dc=org" -w admin -f /tmp/base-users.ldif

docker cp groups2.ldif openldap2:/tmp/groups.ldif
docker exec -it openldap2 ldapadd -x -D "cn=admin,dc=demo2,dc=org" -w admin -f /tmp/groups.ldif
```

## Generate a new jks
```
keytool -genkeypair \
  -alias wso2carbon \
  -keyalg RSA \
  -keysize 2048 \
  -validity 365 \
  -keystore wso2carbon.jks \
  -storepass wso2carbon \
  -keypass wso2carbon \
  -dname "CN=wso2is-km, OU=WSO2, O=example, L=Quito, S=Pichincha, C=EC" \
  -ext SAN=dns:wso2is-km,dns:localhost,ip:127.0.0.1
```
