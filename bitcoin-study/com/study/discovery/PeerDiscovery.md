# peer discovery

## 为什么选用点对点（peer-to-peer）网络架构？

因为比特币去中心化控制是核心设计原则，它只能通过维持一种扁平化、 去中心化的点对点共识网络来实现和维护

## 网络发现两种方式

1. DNS种子

```text
DNS种子就是提供比特币节点IP地址列表的DNS服务器。 其中一些DNS种子提供了稳定的比特币侦听节点的IP地址静态列表。 一些DNS种子是BIND（Berkeley Internet Name Daemon）的自定义实现，它从爬虫程序或长时间运行的比特币节点收集的比特币节点地址列表中返回一个随机子集。 Bitcoin Core客户端包含五种不同DNS种子的名称。 不同DNS种子的所有权的多样性和实现的多样性为初始引导过程提供了高水平的可靠性。 在Bitcoin Core客户端中，DNS种子选项是否启用由选项开关 -dnsseed控制（默认设置为1，使用DNS种子）。
```

2. 赋予至少一个比特币节点的IP地址(-seednode)

```text
命令行参数-seednode可用于连接到一个节点，仅用于将其用作引见种子。 在使用初始种子节点完成引见后，客户端将断开连接并使用新发现的对等节点
```

### 代码实现

主要实现下面方法，传入一个或多个IP地址，或传入一个或多个DNS，返回套接字列表。

```java
public interface PeerDiscovery {
    List<InetSocketAddress> getPeers(long services, long timeoutValue, TimeUnit timeoutUnit) throws PeerDiscoveryException;
}
```

其中DNS多一个下面方法
```java
InetAddress[] response = InetAddress.getAllByName(hostname);
```


## 参考
《精通比特币II》

