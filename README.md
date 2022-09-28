# ENSP

一、华为设备命令视图
1.用户视图：<Huawei>
2.系统视图：<Huawei>system-view/sys 进入特权模式
[Huawei]
3、接口视图：
< Huawei>system-view/sys
[Huawei]interface/int Ethernet0/0/1
[Huawei- Ethernet0/0/1]
路由协议视图：
[Huawei]isis
[Huawei- isis-1]
二、设置设备名称
sysname/sy命令设置设备的名称
< Huawei> system-view
[Huawei] sysname Switch 更改设备名称
[Switch]
三、常用基本命令
1、quit 命令 返回上一级视图
2、return 命令 直接返回< Huawei>用户视图
3、save 命令 在< Huawei>用户视图使用，保存配置
4、reboot 命令 重启设备
5、shutdown 命令 关闭端口
undo shutdown 命令 激活端口
6、undo 命令，有以下：
（1）用于恢复缺省情况（例如设置设备的名称）
< Huawei> system-view
[Huawei] sysname Switch
[Switch] undo sysname 恢复缺省情况
[Huawei]
（2）用于禁用某个功能（例如ftp）
< Huawei> system-view
[Huawei] ftp server enable
[Huawei] undo ftp server 禁用设备的ftp功能
（3）用于删除某项设置
undo后跟某项命令的设置信息即可删除相关的某项配置
四、关闭泛洪信息
< Huawei>undo ter mon 关闭终端显示信息中心发送信息
五、设置设备接口的ip地址和子网掩码
[Huawei] interface 接口 进入接口视图
[Huawei- Ethernet0/0/1]ip address ip地址 子网掩码 配置ip地址和子网掩码
[Huawei- Ethernet0/0/1]undo shutdown 启动接口
[Huawei- Ethernet0/0/1]display interface 接口 查看接口状态
六、交换机的登陆
(一)设置Console接口密码
[Huawei]user-interface console 0 进入控制台接口
[Huawei-ui-console0]authentication-mode password 设置认证方式为密码认证
[Huawei-ui-console0]set authentication password cipher/simple 密码
配置密文/明文密码
[Huawei-ui-console0]user privilege level 级别 配置用户级别，级别可为0-15

(二)设置Telnet接口密码
[Huawei]user-interface vty 0 4 进入VTY接口，最多允许5个用户同时登陆
[Huawei-ui-vty0-4]authentication-mode aaa 认证方式为aaa模式
[Huawei]aaa 进入aaa配置
[Huawei-aaa]local-user 用户名 password cipher/simple 密码
设置用户的密码
[Huawei-aaa]local-user 用户名 service-type telnet
设置用户的服务类型协议为telnet，也可以为其它协议，比如http即使用Web界面
[Huawei-aaa]local-user 用户名 privilege level 级别 配置用户级别
七、VLAN配置
(一)单独和批次创建VLAN
< Huawei>system-view
[Huawei]vlan 10 创建或进入VLAN10
[Huawei]vlan batch 10 to 20 创建VLAN10到VLAN20，共创建11个VLAN
batch to表示创建连续的VLAN，若省略to则创建或进入指定号码的VLAN
(二)进入VLAN视图
[Huawei]vlan 10 若已创建vlan，则进入该VLAN视图；若没有则创建VLAN10
[Huawei-vlan10]name huawei 配置vlan10的名称为huawei
[Huawei]vlan vlan-name huawei 通过更改的VLAN名称进入VLAN视图
(三)将端口指定到VLAN
1、单一端口指定VLAN
[Huawei]interface GigabitEthernet 0/0/1
[Huawei-GigabitEthernet 0/0/1]port link-type access
配置接口类型为access
[Huawei-GigabitEthernet 0/0/1]port default vlan ID号
配置端口的缺省的VLAN并将接口加入到指定vlan
2、多个端口指定VLAN
[Huawei]vlan 10 进入相关VLAN的视图，这里表示进入vlan10
[Huawei-vlan10]port GigabitEthernet 0/0/1 to 0/0/10 将多个端口一并设置为相关VLAN，这里是将1~10号接口全部设置为VLAN10
(四)查看配置情况
[Huawei]dislay vlan ID号
[Huawei]display current-configuration 显示当前配置
