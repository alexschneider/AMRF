AMRF
====

Alex's Map Reduce Framework


* Objectives from most important to least:
  1. Write a simple map reduce framework written in a systems language (either Rust or Go, TBD).
    1. Hook into a program written using at least the following methods:
      1. `split`, which takes arguments: 
        * `data` - collection of some sort containing data required for processing
        * `numClients` 

        Returns a `numClients` (or less) length tuple that contains the data required for processing.
      2. `process`
        * `data` - one of the parts of the tuple returned from `split`
        
        Returns an ambigous type of data (generic if we use Rust, `interface{}` if we use Go)
      3. `generateInitialData` - no arguments, returns collection suitable for `data` argument in `split`
      4. `filter` OR `reduce` - takes `data` argument which is a tuple composed of data from `process`.   
         Returns a collection or single generic/`interface{}` if filter or reduce are used, respectively. If both are used, filter will be run first and then reduce will be run on the filtered collection.
      5. `processFinalData` - takes `data` argument which is the output from `filter` or `reduce`. Called when all clients are finished processing. 
    2. Provide some sort of fault tolerance if a system is unable to process data or takes too long. Especially don't call `processFinalData` with incomplete results, unless to signal an error.  
    3. Provide a management frontend for launching or controlling the server and clients
    4. Write communication framework using sockets and message passing. 
  2. If time permits, the following would be nice to have
    1. Simple web frontend for controlling clients/server
    2. Distributed Filesystem using FUSE (like [HDFS](http://hortonworks.com/hadoop/hdfs/)).
    3. A more comprehensive framework that handles multiple processes per client (we can map multiple times to get smaller and smaller data) so we can get the highest performance.
    4. Some sort of priortiy queueing system so multiple programs can be using the framework at the same time
      1. For real fanciness - authentication and user management system to divy up process resources using some sort of cake cutting algorithm (with Dorin's help possibly).
  2. ???
  3. Profit
