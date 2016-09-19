# Prepare for JDK9

## Incompatibility

* Uses of JDK-internal APIs
  * Non critical APIs
  Used only for convenience
  * Critical
  Functionality that would be hard to expose outside of JDK

## Tools

### JDeps
* Included in JDK8 improved in JDK9

```
$ jdeps -jdkinternals yourjarfile.jar
```

* Maven JDeps Plugin

https://maven.apache.org/plugins/maven-jdeps-plugin/

### Command Line Flags

```
--add-exports java.base/sun.security.provider=ALL-UNNAMED
                  ^             ^                  ^
                  |             |                  |
                module       package             flag
```

## Changes in the binary structure

One level of directories:

```
       |
  -----------
  |    |    |
/bin /conf /lib
```

## Removed extension mechanism:
- Endorsed standards override mechanism
- Extension mechanism

```
java -cp jsr305.jar

javax.annotation.Notnull
javax.annotation.Nullable
```

## Modules shared with JavaEE not resolved by default:

- use command line option to resolve modules:

```
--add-module java.corba
```
 - Deploy on the upgrade module path:

```
 --upgrademodulepath corba.jar --ad-module java.corba
 ```

 - Deploy on the classpath

```
 --class-path java.corba.jar
```

## Removed:

-Xbootclasspath -Xbootclasspath/p

## New version-string scheme

```
1.9.0 -> 9
1.9.0-b100 -> 9+100
```

The is a version object available in the runtime

## Multi-Release JAR files

```
com/acme/stats/cli/Main.class
com/acme/stats/internal/Helper.class
META-INF
META-INF/MANIFEST.MF ------------------> Multi-Release: true
META-INF/versions/9/com/acme/stats/internal/Helper.class
```

## We dont need multiple JDK in our build environment

```
javac --release 7
```
