# jmc-jshell
Easy way to get started experimenting with the JDK Flight Recorder and the JMC core classes.

First ensure that you are running with a JDK 9 or later. Then run:

```bash
mvn compile
mvn jshell:run
```

You should now be presented with a jshell command line. 

```

|  Welcome to JShell -- Version 11
|  For an introduction type: /help intro

jshell>
```

At the prompt run the following to set up some imports:

```
/open jmc.jsh
```

Now you are ready to play around with the JMC core APIs.

## Examples

Here is an example of a session calculating the standard deviation for the java monitor enter events in the example recording:

```
jshell> var allEvents = JfrLoaderToolkit.loadEvents(new File("latency.jfr"))
allEvents ==> org.openjdk.jmc.flightrecorder.EventCollection@7f010382

jshell> var monitorEnterEvents = allEvents.apply(ItemFilters.type(JdkTypeIDs.MONITOR_ENTER))
monitorEnterEvents ==> org.openjdk.jmc.flightrecorder.EventCollection@433d61fb

jshell> var stddev = monitorEnterEvents.getAggregate(Aggregators.stddev(JfrAttributes.DURATION))
stddev ==> 2.11292968454666E9ticks[ticks]

jshell> stddev.displayUsing(IDisplayable.AUTO)
$9 ==> "2,113 s"
```

Here is another example, evaluating the available rules against the example recording:

```
jshell> JfrRulesReport.printReport("text", Severity.INFO, true, false, "latency.jfr")
Flight Recording report

File: latency.jfr

Rule: Java Blocking
Severity: Warning
Score: 100
Message: Threads in the application were blocked on locks for a total time of 16 min 34 s.
Detailed message: Threads in the application were blocked on locks for a total time of 16 min 34 s. The most common monitor class was 'Logger', which was blocked on 277 times. The following regular expression was used to exclude threads from this rule: '(.*weblogic\.socket\.Muxer.*)'

Rule: Free Physical Memory
Severity: Information
Score: 71.2
Message: The maximum amount of used memory was 93,7 % of the physical memory available.
Detailed message: The maximum amount of used memory was 15 GiB. This is 93,7 % of the 16 GiB of physical memory available. Having little free memory may lead to swapping, which is very expensive. To avoid this, either decrease the memory usage or increase the amount of available memory.

Rule: Competing Processes
Severity: Information
Score: 41
Message: 294 processes were running while this Flight Recording was made.
Detailed message: At 2018-08-24, 06:47:37, a total of 294 other processes were running on the host machine that this Flight Recording was made on. If this is a server environment, it may be good to only run other critical processes on that machine.
```
