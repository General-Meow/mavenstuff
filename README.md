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

- artificatory allows you to generate a settings.xml by selecting the "Set Me Up" link and generate link. This will need to be copied into your maven home directory (typically .m2) and the profile referenced in the pom.xml of your project

```settings.xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd" xmlns="http://maven.apache.org/SETTINGS/1.1.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<pluginGroups>
		<pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
	</pluginGroups>
	<servers>
		<!-- HOME Artifactory server-->
		<server>
			<username>admin</username>
			<password>{3VSDIbOOKdAHfz9HqISkCQpSSSg/cbqSj3OprYXVg7c=}</password>
			<id>central</id>
		</server>
		<server>
			<username>admin</username>
			<password>{3VSDIbOOKdAHfz9HqISkCQpSSSg/cbqSj3OprYXVg7c=}</password>
			<id>snapshots</id>
		</server>
		<!-- HOME Artifactory server end-->

	</servers>
	<profiles>
		<!-- HOME Artifactory repos-->
		<profile>
			<repositories>
				<repository>
					<snapshots>
						<enabled>false</enabled>
					</snapshots>
					<id>central</id>
					<name>libs-release</name>
					<url>http://pine.paulhoang.com:8081/artifactory/libs-release</url>
				</repository>
				<repository>
					<snapshots />
					<id>snapshots</id>
					<name>libs-snapshot</name>
					<url>http://pine.paulhoang.com:8081/artifactory/libs-snapshot</url>
				</repository>
			</repositories>
			<pluginRepositories>
				<pluginRepository>
					<snapshots>
						<enabled>false</enabled>
					</snapshots>
					<id>central</id>
					<name>libs-release</name>
					<url>http://pine.paulhoang.com:8081/artifactory/libs-release</url>
				</pluginRepository>
				<pluginRepository>
					<snapshots />
					<id>snapshots</id>
					<name>libs-release</name>
					<url>http://pine.paulhoang.com:8081/artifactory/libs-release</url>
				</pluginRepository>
			</pluginRepositories>
			<id>artifactory</id>
		</profile>
	</profiles>
	<activeProfiles>
		<activeProfile>artifactory</activeProfile>
	</activeProfiles>
</settings>


```

- for this to be used, you need to generate the deploy settings for the pom.xml. again this can be generated in the set me up area of artifactory
- e.g of the deploy settings

``` pom.xml
<distributionManagement>
    <repository>
        <id>central</id> <!-- this is will correspond to the profile ids in the settings.xml -->
        <name>af083f7e8bdb-releases</name>
        <url>http://pine.paulhoang.com:8081/artifactory/libs-release-local</url>
    </repository>
</distributionManagement>
```

- Important note: the pom version in your pom.xml could indicate which repo the artifact gets uploaded to. having a SNAPSHOT er will make the mvn plugin push to a snapshot repo, so make sure you have it enabled and in the distributionManagement part of the pom
