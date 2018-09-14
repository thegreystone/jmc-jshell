# jmc-jshell
Easy way to get started experimenting with the JDK Flight Recorder and the JMC core classes.

Note, that for this to work, you will need a relatively recent gradle. There is a gradle wrapper included
to make it easier to get started.

To run, first set the JAVA_HOME environment variable to point to your JDK 11 installation. For example, on Mac OS X, this could look like this:

```bash
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-11.jdk/Contents/Home
```

Then run it with:

```bash
./gradlew --no-daemon --console plain jshell
```

You may have to set the following environment variable as well:

```bash
_JAVA_OPTIONS="--add-exports=jdk.jshell/jdk.internal.jshell.tool=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"
```
