# kotlin-native - A Plugin for Snapcraft
Snaps are very useful for CLI applications, and Kotlin Native is a great platform for Kotlin CLI applications.
However, trying to get Snapcraft to successfully Snap your Kotlin Native application is pain and agony.
The Gradle plugin expects a jar, which Kotlin Native does not provide.
Other plugins require another build system, which isn't fun when you already have Gradle.

So, enter this simple plugin. It simply runs `./gradlew linkReleaseExecutableNative`,
copies the resulting artifact into the part's install directory,
and removes the unnecessary `.kexe` extension from the output.

Here is a sample snapcraft.yaml that uses this plugin:

```yml
name: my-snap
version: '0.1.0'
source-code: https://github.com/Stephen-Hamilton-C/snapcraft-kotlin-native
license: GPL-3.0
summary: Simple Snapcraft plugin for Kotlin Native
description: |
  Makes it easy to Snap your Kotlin Native applications.
base: core18
apps:
  my-snap:
    command: $SNAP/my-snap
parts:
  my-snap:
    plugin: kotlin-native
    source: ../
    build-packages:
      - default-jre-headless
```

Replace `my-snap` with your app name.
