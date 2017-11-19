---
layout: post
title: LDAP 
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- LDAP
star: true
category: blog
author: Jack
description: LDAP 
---

```shell
./export-ldif --includeBranch dc=medtronic,dc=com --backendID userRoot --ldifFile ../backups/20170412/2017_04_13.ldif
```
```shell
sudo ./ldapdelete --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --deleteSubtree "dc=medtronic,dc=com"
```
```shell
sudo ./import-ldif --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --includeBranch dc=medtronic,dc=com --clearBackend --backendID userRoot --ldifFile ~/migration/target/ldap/Ablation.ldif
```
```shell
sudo ./import-ldif --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --includeBranch dc=medtronic,dc=com --backendID userRoot --ldifFile ~/migration/target/ldap/gdmpnew_1109.ldif
```
```shell
sudo ./import-ldif --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --includeBranch dc=medtronic,dc=com --backendID userRoot --ldifFile ~/migration/target/ldap/gateway_5190.ldif
```
```shell
sudo ./import-ldif --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --includeBranch dc=medtronic,dc=com --backendID userRoot --ldifFile ~/migration/target/ldap/GDMPNEW1117_CHANGE_VTSCLIENT_TO_ESSCLIENT.ldif
```
```shell
sudo ./import-ldif --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --includeBranch dc=medtronic,dc=com --backendID userRoot --ldifFile ~/migration/target/ldap/GDMPNEW1109_CHANGE_EMPRINTXXXAPPLICATION_TO_EMPRINTABLATIONXXXAPPLICATION.ldif
```
```shell
sudo ./import-ldif --bindDN "cn=Directory Manager" --bindPassword BLDpass001 --includeBranch dc=medtronic,dc=com --backendID userRoot --ldifFile ~/migration/target/ldap/gdmpnew1117.ldif
```
```shell
sudo ./dsconfig -h localhost -p 4444 -D "cn=directory manager" -w BLDpass001 -X set-connection-handler-prop --handler-name "LDAP Connection Handler" --set enabled:true
```
