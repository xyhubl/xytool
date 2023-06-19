# YIM 聊天推送系统

该项目可以业务于 推送、聊天等系统，鉴于goim 不怎么维护，所以复刻了此项目。欢迎感兴趣的伙伴一起维护。

Comet:

有状态服务，目前只支持ws通信(支持多节点部署)

Job:

消息分发层

Logic:

logic路由层，目前实现单聊



流程:

客户端连接ws -> auth- > 建立连接

logic发送消息 -> job分发 -> comet发送消息到客户端



需要环境:

zookeeper kafka redis golang环境（建议>=1.17）



消息协议：

```
| parameter             | is required  | type     | comment|
| :-----                | :---         | :---     | :---       |
| package length        | true  | int32 bigendian | package length |
| header Length         | true  | int16 bigendian | header length |
| ver                   | true  | int16 bigendian | Protocol version |
| operation             | true |  int32 bigendian | Operation |
| seq                   | true |  int32 bigendian | jsonp callback |
| body                  | false | binary          | $(package lenth) - $(header length) |


| operation     | comment | 
| :-----     | :---  |
| 2 | Client send heartbeat|
| 3 | Server reply heartbeat|
| 7 | authentication request |
| 8 | authentication response |
```


目前完成:
1. 单聊、群聊

后续规划:
1. 广播、事件订阅
2. 离线消息存储漫游
3. ack机制
4. 服务发现注册
5. 等等..

