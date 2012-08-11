# Qt Jambi PKGBUILD
This Repo contains an [Archlinux]  [PKGBUILD] of [Qt Jambi].

Its current aim is to provide Qt Jambi compiled against system Qt.

Code examples contain `$QTVERSION` which can be determined like so: `QTVERSION=$(pkg-config --modversion QtCore)`.

## Paths
currently, it installs its libraries into `lib/jni`, and needs system Qt libraries to run.

This means that your IDE/buildscript needs to add the following paths to its `java.library.path`:

* `/usr/lib`
* `/usr/lib/jni`

The `jar` resides in `share/java`, so you have to add the following to your classpath:

* `/usr/share/java/qtjambi-$QTVERSION.jar`

## Examples
### Eclipse
Setup your project like so (it’s german, but you should figure it out)

![Eclipse user libraries](https://raw.github.com/flying-sheep/qtjambi-git-pkgbuild/master/eclipse-user-lib.png)

### Running the demos
```bash
java -Djava.library.path=/usr/lib:/usr/lib/jni \
	-cp /usr/share/java/qtjambi-$QTVERSION.jar:/usr/share/java/qtjambi-examples-$QTVERSION.jar \
	com.trolltech.launcher.Launcher
```

[Archlinux]: https://www.archlinux.org/
[PKGBUILD]:  https://wiki.archlinux.org/index.php/PKGBUILD
[Qt Jambi]:  http://qt-jambi.org/