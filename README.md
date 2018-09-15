# jmc-jshell
Easy way to get started experimenting with the JDK Flight Recorder and the JMC core classes.

First ensure that you are running with a JDK 9 or later. Then run:

```bash
mvn compile
mvn jshell:run
```

You should now be presented with a jshell command line. 

```bash

|  Welcome to JShell -- Version 11
|  For an introduction type: /help intro

jshell>
```

At the prompt run the following to set up some imports:

```bash
/open jmc.jsh
```

Now you are ready to play around with the JMC core APIs.

## Example

Here is an example of a session calculating the standard deviation for the java monitor enter events in the example recording:

```bash
jshell> var allEvents = JfrLoaderToolkit.loadEvents(new File("latency.jfr"))
allEvents ==> org.openjdk.jmc.flightrecorder.EventCollection@7f010382

jshell> var monitorEnterEvents = allEvents.apply(ItemFilters.type(JdkTypeIDs.MONITOR_ENTER))
monitorEnterEvents ==> org.openjdk.jmc.flightrecorder.EventCollection@433d61fb

jshell> var stddev = monitorEnterEvents.getAggregate(Aggregators.stddev(JfrAttributes.DURATION))
stddev ==> 2.11292968454666E9ticks[ticks]

jshell> stddev.displayUsing(IDisplayable.AUTO)
$9 ==> "2,113 s"
```
