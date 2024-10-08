# Building a PREEMPT_RT Kernel for Raspberry Pi 3B+

This guide provides step-by-step instructions for building and installing a PREEMPT_RT kernel on a Raspberry Pi 3B+.

## Sources

- **Kernel Source:** [Linux Kernel Repository](https://github.com/raspberrypi/linux)
- **RT Patch Archive:** [PREEMPT_RT Patch Archive](https://mirrors.edge.kernel.org/pub/linux/kernel/projects/rt/6.6/older/)

## Latency Test

The `cyclictest` command is executed with the following parameters:

```bash
cyclictest -l100000000 -m -Sp90 -i200 -h400 -q
```

- `-l100000000`: Sets the total number of iterations to 100 million. This ensures the latency is measured across many cycles for accuracy.
- `-m`: Enables maximum latency reporting, providing detailed statistics, including the highest latency observed.
- `-Sp90`: Sets the process priority to 90. Higher values indicate greater priority, which helps in minimizing latency.
- `-i200`: Defines the measurement interval as 200 µs (microseconds), recording latency every 200 µs.
- `-h400`: Sets the maximum latency to monitor at 400 µs. Latencies exceeding this value will be reported.
- `q`: Runs `cyclictest` in quiet mode to produce a streamlined output focusing on essential data.

The latency plots are generated using `gnuplot` with a script based on `mklatencyplot` from `OSADL`.

### Latency Test Results

![Test-result](Image/plot.png)

|       | Cycle Samples | Min Latencies (µs) | Max Latencies (µs) | Avg Latencies (µs) |
|-------|---------------|--------------------|--------------------|--------------------|
| CPU 0 |   100000000   |          4         |        116         |          6         |
| CPU 1 |   100000000   |          4         |         76         |          6         |
| CPU 2 |   100000000   |          4         |         88         |          6         |
| CPU 3 |   100000000   |          4         |         71         |          6         |

## References

- **Raspberry Pi Documentation:** [Raspberry Pi Linux Kernel Documentation](https://www.raspberrypi.com/documentation/computers/linux_kernel.html)
- **System Lockup Patch for RPi 3:** [Fix System Lockup for RPi 3](https://github.com/kdoren/linux/wiki/Building-PREEMPT_RT-kernel-for-Raspberry-Pi)
- **Latency Test:** [HOWTO: Create a latency plot from cyclictest histogram data](https://www.osadl.org/Create-a-latency-plot-from-cyclictest-hi.bash-script-for-latency-plot.0.html)
