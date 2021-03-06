# 2PC
```md
二阶段提交其实就是实现XA分布式事务的关键。
（两阶段提交主要保证了分布式事务的原子性：即所有结点要么全做要么全不做）
```
## 两个阶段
* 准备阶段
```md
事务协调者(事务管理器)给每个参与者(资源管理器)发送Prepare消息，每个参与者要么直接返回失败(如权限验证失败)，
要么在本地执行事务，写本地的redo和undo日志，但不提交，然后向协调者反馈YES,NO。
```
* 提交阶段
```md
如果协调者收到了参与者的失败消息或者超时，直接给每个参与者发送回滚(Rollback)消息；
否则，发送提交(Commit)消息。

参与者根据协调者的指令执行提交或者回滚操作，释放所有事务处理过程中使用的锁资源。

* 注意
必须在最后阶段释放锁资源。
在2PC中，当等待超时，会进行回滚操作。
```
## 存在的问题
* 同步阻塞问题
```md
执行过程中，所有参与节点都是事务阻塞型的。

各个参与者在等待协调者发出提交或中断请求时，会一直阻塞。
而协调者的发出时间要依赖于所有参与者的响应时间，如果协调者宕机了（单点），
那么他就一直阻塞在这，而且无法达成一致（3PC引入了超时提交解决）。
```
* 单点故障
```md
如果是协调者挂掉，可以重新选举一个协调者，但是无法解决因为协调者宕机导致的参与者处于阻塞状态的问题。
```
* 脑裂 (数据一致性问题)
```md
2PC协议中，如果出现协调者和参与者都挂了的情况，有可能导致数据不一致。
```
* 太过保守
```md
2PC没有设计相应的容错机制，当任意一个参与者节点宕机，
那么协调者超时没收到响应，就会导致整个事务回滚失败。
```