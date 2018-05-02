# mavenstuff

### random stuff that i want to keep aroud

- to have encrypted passwords you need to generate a master password and settings-security.xml file
- you do that by running mvn --encrypt-master-password
- enter password
- it returns the encrypted master password
- paste it into the settings-security.xml under .m2 dir
```
<settingsSecurity>
    <master>ENCRYPTED_PASSWORD_GOES HERE</master>
</settingsSecurity>
```

- then generate an encrypted password with mvn --encrypt-password
- then paste that password into your settings.xml in .m2 where needed

- artificatory allows you to generate a settings.xml by selecting the "Set Me Up" link and generate link
- for this to be used, you need to generate the deploy settings for the pom.xml. again this can be generated in the set me up area of artifactory
- e.g of the deploy settings

```
<distributionManagement>
    <repository>
        <id>central</id> <!-- this is will correspond to the profile ids in the settings.xml -->
        <name>af083f7e8bdb-releases</name>
        <url>http://pine.paulhoang.com:8081/artifactory/libs-release-local</url>
    </repository>
</distributionManagement>
```
