# LDAP USER SEARCH

[
 "OU=Users,DC=pg,DC=lab",
 "SCOPE_SUBTREE",
 "(uid=%(user)s)"
]

    LDAP search query to find users. Any user that matches the given pattern will be able to login to Tower.
    The user should also be mapped into a Tower organization (as defined in the AUTH_LDAP_ORGANIZATION_MAP setting).
    If multiple search queries need to be supported use of "LDAPUnion" is possible. See Tower documentation for details.



# LDAP GROUP SEARCH

[
 "OU=Users,DC=pg,DC=lab",
 "SCOPE_SUBTREE",
 "(objectClass=posixGrooup)"
]

    Users are mapped to organizations based on their membership in LDAP groups. 
    This setting defines the LDAP search query to find groups. Unlike the user search, group
    search does not support LDAPSearchUnion.



# LDAP USER ATTRIBUTE MAP


    Mapping of LDAP user schema to Tower API user attributes. The default setting is valid for
    ActiveDirectory but users with other LDAP configurations may need to change the values. Refer 
    to the Ansible Tower documentation for additional details.

