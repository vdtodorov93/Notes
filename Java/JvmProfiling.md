# JVM Profiling

## Common tools

### Jps
`jps` - lists java processes  

### Histograms
`jmap` - live inspection of java processes  
`jmap -histo[:live] <pid>`

`[C` = Char array, `[B` = Byte array, `[L` - array of some class, etc.  

## Heap dumps
Contain a lot more details than a histogram  
`jmap -dump:file=/path/to/log <pid>`  

add a Java option on run:  
`-XX:+HeapDumpOnOutOfMemoryError`  
`-XX:HeapDumpPath=/path/to/dump`  
Downsides of this approach is it might take a lot of time to make the dump on the disk and increase time-to-recovery of the service.  