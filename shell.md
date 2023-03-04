### ls

### less && more

### head && tail

### top

### ps

### df

### du

### netstat
  - 常用参数
      - **a**:所有连接中的socket
      - **t/u**:tcp/udp协议
      - **n**:显示ip地址而不是域名
      - **l**:显示监听状态的socket
      - **p**:显示程序名
  - 输出项
      - **proto**:协议名
      - **recv-Q/send-Q**:接收和发送缓冲区
          - 若接收缓冲区不为空，表明还没有被进程消费，若长时间不为空，可能遭到了dos攻击
          - 若发送缓冲区不为空，说明接收方接受能力有限，或者发送数据过快
          - 两个队列通常为空，不为空可能出现了问题

### tcpdump
  - 常用命令
  ```
  tcpdump -i eth0  #监听eth0接口的数据包
  tcpdump -i eth0 tcp port 23
  tcpdump -i eth0 udp port 123 and dst host 192.168.0.3
  ```

### grep

### sed

### awk

### wc

### xargs

### find && whereis && location
