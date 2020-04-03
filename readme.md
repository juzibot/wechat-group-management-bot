## 微信公共群组管理机器人

###适用场景：
* 电商/微商营销社群
* 公司业务群组

### 背景
1. 创建一个风控数据库，监控微信号因为某种原因被举报离群原因
2. 员工离职后，总有某些业务群没有退出，对双方都做成不便

### 功能
* 营销社群举报踢人
  + 记录全网被举报人的次数及原因
  + 便于群管理员识别群成员是否进入【广告】等风控
* 查询公司相关业务群组并踢人
  + 员工离职快速离开各种业务群

### 实现逻辑
* 每次机器人登录都扫描一次所有群聊，确定好群组管理员关系（避免因为掉线，忽略了掉线期间被拉进的群聊）
  + 第一次写入数据库的时候，确定当前群主是该群的永久性管理员，方便以后机器人退还群主位置
* 监控消息（区分群聊/个人消息）
  + 个人消息做对应的指令
  + 群聊消息区分管理员/非管理员指令
    - 非管理员指令有：
      1. 普通回复指令
      2. 举报指令 （该群24小时内，达到3条举报，将被踢出群聊）
    - 管理员指令
      1. 指定某人离开所有管理员管理的群聊

