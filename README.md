Lift-LDAP
=========

This module provides a LDAPVendor class to perform search and bind operations against a LDAP Server,
and a base class to authentificate LDAP users (using the LDAPVendor)

#### 1. SimpleLDAPVendor
SimpleLDAPVendor extends LDAPVendor class and provides a simple and functional LDAPVendor,
that only needs to provide a parameters var to define the LDAP Server properties .

```scala
SimpleLDAPVendor.parameters = () => Map("ldap.url"  -> "ldap://localhost",
                                        "ldap.base" -> "dc=company,dc=com",
                                        "ldap.userName" -> "cn=query,dc=company,dc=com",
                                        "ldap.password" -> "password")
```

or

```scala
SimpleLDAPVendor.parameters = () => SimpleLDAPVendor.parametersFromFile("/some/directory/ldap.properties")
```

#### 2. LDAPProtoUser
Base class of LDAP users

We can define:

| Value             | Description                                                                                                  | Default                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------ | ---------------------------------------- |
| loginErrorMessage | Message displayed when user auth failed                                                                      | "Unable to login with : %s"              |
| ldapUserSearch    | LDAP search sentence to search user object using login and password                                          | (uid=%s)                                 |
| rolesSearchFilter | LDAP search filter to get the user roles                                                                     | (&(objectClass=groupOfNames)(member=%s)) |
| rolesNameRegex    | Regular expression to get the role name from his dn (maybe we should get object cn attribute or something ?) |                                          |


_We can override setRoles function if we want to define roles search manually_