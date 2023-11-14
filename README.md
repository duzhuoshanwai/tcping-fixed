# Tcping

[中文](README-zh.md)

The Tcping is a network tool.
which is similar with ping.

We often use the network is based on tcp, So use tcping more accurately.

## Usage

```
pip install tcping
```

```
➜  ~ tcping api.github.com
Connected to api.github.com[:80]: seq=1 time=236.44 ms
Connected to api.github.com[:80]: seq=2 time=237.99 ms
Connected to api.github.com[:80]: seq=3 time=248.88 ms
Connected to api.github.com[:80]: seq=4 time=233.51 ms
Connected to api.github.com[:80]: seq=5 time=249.23 ms
Connected to api.github.com[:80]: seq=6 time=249.77 ms
Connected to api.github.com[:80]: seq=7 time=235.82 ms
Connected to api.github.com[:80]: seq=8 time=242.30 ms
Connected to api.github.com[:80]: seq=9 time=248.26 ms
Connected to api.github.com[:80]: seq=10 time=251.77 ms

--- api.github.com[:80] tcping statistics ---
10 connections, 10 succeeded, 0 failed, 100.00% success rate
minimum = 233.51ms, maximum = 251.77ms, average = 243.40ms
```

GFW Fucking.
 
```
➜  ~ tcping-fixed.py --help
Usage: tcping-fixed.py [OPTIONS] HOST

Options:
  -p, --port INTEGER      Tcp port
  -c, --count INTEGER     Try connections counts
  -t, --timeout FLOAT     Timeout seconds
  --report / --no-report  Show report to replace statistics
  -4, --ipv4              Use IPv4
  -6, --ipv6              Use IPv6
  --help                  Show this message and exit.
```

the result is ascii table by using `--report`.

```
root@cloudcone:~# ./tcping-fixed.py ipw.cn --report -c 5 -t 2 -4
Connected to ipw.cn (42.7.60.104:80): tcp_seq=1 time=367.42 ms
Connected to ipw.cn (42.7.60.104:80): tcp_seq=2 time=405.87 ms
Connected to ipw.cn (42.7.60.104:80): tcp_seq=3 time=229.61 ms
Connected to ipw.cn (42.7.60.104:80): tcp_seq=4 time=539.49 ms
Connected to ipw.cn (42.7.60.104:80): tcp_seq=5 time=400.68 ms

+--------+-------------+------+-----------+--------+--------------+----------+----------+----------+
|  Host  | Resolved IP | Port | Succeeded | Failed | Success Rate | Minimum  | Maximum  | Average  |
+--------+-------------+------+-----------+--------+--------------+----------+----------+----------+
| ipw.cn | 42.7.60.104 |  80  |     5     |   0    |   100.00%    | 229.61ms | 539.49ms | 388.61ms |
+--------+-------------+------+-----------+--------+--------------+----------+----------+----------+
root@cloudcone:~# ./tcping-fixed.py ipw.cn --report -c 5 -t 2 -6
Connected to ipw.cn (2408:8723:800:3:3a::b:80): tcp_seq=1 time=160.55 ms
Connected to ipw.cn (2408:8723:800:3:3a::b:80): tcp_seq=2 time=310.83 ms
Connected to ipw.cn (2408:8723:800:3:3a::b:80): tcp_seq=3 time=475.40 ms
Connected to ipw.cn (2408:8723:800:3:3a::b:80): tcp_seq=4 time=279.85 ms
Connected to ipw.cn (2408:8723:800:3:3a::b:80): tcp_seq=5 time=287.57 ms

+--------+-----------------------+------+-----------+--------+--------------+----------+----------+----------+
|  Host  |      Resolved IP      | Port | Succeeded | Failed | Success Rate | Minimum  | Maximum  | Average  |
+--------+-----------------------+------+-----------+--------+--------------+----------+----------+----------+
| ipw.cn | 2408:8723:800:3:3a::b |  80  |     5     |   0    |   100.00%    | 160.55ms | 475.40ms | 302.84ms |
+--------+-----------------------+------+-----------+--------+--------------+----------+----------+----------+
```

The return code can be catch by some real-time test tools. Following is an example:

```python
import subprocess as sp

# Print the return code (status=0 mean ping success)
status = sp.call(['tcping', '-c', '1', '-t', '1', 'github.com'], stdout=sp.DEVNULL, stderr=sp.DEVNULL)
print(status)

# OR print the full message
status = sp.run(['tcping', '-c', '1', '-t', '1', 'github.com'], stdout=sp.DEVNULL, stderr=sp.DEVNULL)
print(status)
```

## END 

Huh, I just want to check my VPS's network status.

