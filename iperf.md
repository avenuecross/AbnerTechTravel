Iperf是一个网络性能测试工具。Iperf可以测试TCP和UDP带宽质量。
Iperf还有一个图形界面程序叫做Jperf，使用JPerf程序能简化了复杂命令行参数的构造，而且 它还保存测试结果,同时实时图形化显示结果。
在适当的地方，选项中可以使用K（kilo-）和M（mega-）。例如131072字节可以用128K代替。

example:
iperf -s -p 5001 -i 1 -M

Client/Server:
  -f, --format    [kmKM]   format to report: Kbits, Mbits, KBytes, MBytes
  -i, --interval  #        seconds between periodic bandwidth reports
  -p, --port      #        server port to listen on/connect to
  -M, --mss       #        set TCP maximum segment size (MTU - 40 bytes)

Server specific:
  -s, --server             run in server mode
