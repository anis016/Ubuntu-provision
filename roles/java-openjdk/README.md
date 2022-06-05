# java-openjdk

This role installs and setup the Java 8 or 11 depending on the `java_openjdk__enable_jdk8` variable.

## Role Variables

Available variables are listed below.

Java version (8 or 11) is set using the below variable. When `java_openjdk__enable_jdk8` is set to `true` then OpenJDK-8
is installed and when `java_openjdk__enable_jdk8` is set to `false` then OpenJDK-11 is installed.

```yaml
java_openjdk__enable_jdk8: true
```

`JAVA_HOME` is set using the below variable.

```yaml
java_openjdk__java_version
```

## Example Playbook

```yaml
- hosts: "all"
  roles:
    - name: "java-openjdk"
      tags: "java"
```
