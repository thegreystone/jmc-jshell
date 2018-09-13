# jmc-jshell
Easy way to get started experimenting with the JDK Flight Recorder and the JMC core classes.

Note, that for this to work, you will need a relatively recent gradle. There is a gradle wrapper included
to make it easier to get started.

To run, first set the following two environment variables:

```bash
JAVA_HOME=/path/to/your/jdk11
_JAVA_OPTIONS="--add-exports=jdk.jshell/jdk.internal.jshell.tool=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"
```

Then run it with:

```bash
./gradlew --no-daemon --console plain jshell
```
