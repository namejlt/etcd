# etcd对象设计


## 名词解释



Raft：Etcd所采用的保证分布式系统强一致性的算法。

Node：一个Raft状态机实例。

Member： 一个Etcd实例。它管理着一个Node，并且可以为客户端请求提供服务。

Cluster：由多个Member构成可以协同工作的Etcd集群。

Peer：对同一个Etcd集群中另外一个Member的称呼。

Client： 向Etcd集群发送HTTP请求的客户端。

WAL：预写式日志，Etcd用于持久化存储的日志格式。

snapshot：Etcd防止WAL文件过多而设置的快照，存储Etcd数据状态。

Proxy：Etcd的一种模式，为Etcd集群提供反向代理服务。

Leader：Raft算法中通过竞选而产生的处理所有数据提交的节点。

Follower：竞选失败的节点作为Raft中的从属节点，为算法提供强一致性保证。

Candidate：当Follower超过一定时间接收不到Leader的心跳时转变为Candidate开始竞选。

Term：某个节点成为Leader到下一次竞选时间，称为一个Term。

Index：数据项编号。Raft中通过Term和Index来定位数据


## 模块核心


raft用于通信和共识，raft协议实现

storage 写入，mvcc写入

lease 租期，核心优先队列


## 代码查看顺序


客户端代码，这个封装了请求服务端http、grpc的代码，可以知道服务端支持那些服务

client
etcdctl
etcdutl


服务端代码


server
- web server
- raft
- wal （entry、snapshot）
- store







