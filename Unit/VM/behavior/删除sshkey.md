# 删除SSH key
* ### 描述

 云主机由Stopped状态变为Running

* ### 初始状态

 [Stopped](/Unit/VM/status.md)

* ### 前提条件

 物理机处于enabled状态，connectted状态

* ### 参数
 
 | 资源 | 状态 |
 | ---
 | 云主机 | state：running | 


* ### 结束状态

 [Running](/Unit/VM/status.md)

* ### 错误

* ### 场景

 场景1：非停止状态的VM应无法点击启动，或者直接报错

 场景2：若对应Host处于disabled或maintain状态，那么VM无法从Stopped状态启动

 场景3：若对应的Host已删除，则VM不可启动

 场景4：若对应的根云盘被停用或删除，VM不可启动





