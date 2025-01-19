# Gradle Boilerplate with publishing to central

Package and build java library using this template with `maven-publish` and `jreleaser` plugins.

## Generate artifacts in local repository

To publish to local maven repo

    gradle publishMyPubPublicationToMavenLocalRepository

To publish to your custom maven repo

    gradle publishMyPubPublicationToLocalMavenWithChecksumsRepository

To publish to custom maven repo with signing by gpg keys

    gradle clean build publishMyPubPublicationToLocalMavenWithChecksumsRepository -Psigning.password=YOUR-GPG-PASSWORD -Psigning.keyId=YOUR-GPG-KEY-ID

To generate artifacts to be published by jreleaser

    gradle clean build publishMyPubPublicationToPreDeployRepository

## Generate and publish atrifact with jreleaser

Transform gpg keys to required format

```shell
gpg --export-secret-keys --armor YOUR-GPG-KEY-ID > private.key
gpg --export --armor YOUR-GPG-KEY-ID > public.key
```

Create a local JReleaser configuration file, create a file `~/.jreleaser/config.properties` with the following content:

```properties
JRELEASER_GPG_PASSPHRASE=YOUR-GPG
JRELEASER_MAVENCENTRAL_SONATYPE_USERNAME=YOUR-SONATYPE-API-USERNAME
JRELEASER_MAVENCENTRAL_SONATYPE_PASSWORD=YOUR-SONATYPE-API-PASSWORD
```

Publish with JReleaser over Maven Publisher API

```shell
#DANGER: After this, you cannot delete your artifacts from Maven Central
gradle jreleaserDeploy
```
