# simple-process-stats

A small Rust library to get memory usage and elapsed CPU time.

* Supports Windows and Linux.
* Async interface, uses `tokio::fs` for file operations

```
use simple_process_stats::ProcessStats;

let process_stats = ProcessStats::get().expect("could not get stats for running process");
println!("{:?}", process_stats);
// ProcessStats {
//     cpu_time_user: 421.875ms,
//     cpu_time_kernel: 102.332ms,
//     memory_usage_bytes: 3420160,
// }
```

On Linux, this library reads `/proc/self/stat` and uses the `sysconf` libc function.

On Windows, the library uses `GetCurrentProcess` combined with `GetProcessTimes` and `K32GetProcessMemoryInfo`.
