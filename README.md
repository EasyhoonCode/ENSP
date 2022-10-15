# ENSP

  # 一、华为设备命令视图
    1.用户视图：<Huawei>
    2.系统视图：<Huawei>system-view或者sys 进入特权模式
    [Huawei]
    3、接口视图：
    <Huawei>system-view/sys
    [Huawei]interface eth0/0/1或者int Ethernet0/0/1
    [Huawei-Ethernet0/0/1]
    路由协议视图：
    [Huawei]isis
    [Huawei-isis-1]
  
  # 二、设置设备名称
    sysname/sy命令设置设备的名称
    <Huawei> system-view
    [Huawei] sysname Switch 更改设备名称
    [Switch]
  
  # 三、常用基本命令
    1、quit 命令 返回上一级视图
    2、return 命令 直接返回< Huawei>用户视图
    3、save 命令 在< Huawei>用户视图使用，保存配置
    4、reboot 命令 重启设备
    5、shutdown 命令 关闭端口
    undo shutdown 命令 激活端口
    6、undo 命令，有以下：
    （1）用于恢复缺省情况（例如设置设备的名称）
    <Huawei> system-view
    [Huawei] sysname Switch
    [Switch] undo sysname 恢复缺省情况
    [Huawei]
    （2）用于禁用某个功能（例如ftp）
    <Huawei> system-view
    [Huawei] ftp server enable
    [Huawei] undo ftp server 禁用设备的ftp功能
    （3）用于删除某项设置
    undo后跟某项命令的设置信息即可删除相关的某项配置
  
  # 四、关闭泛洪信息
    <Huawei>undo ter mon 关闭终端显示信息中心发送信息
  
  # 五、设置设备接口的ip地址和子网掩码
    [Huawei] interface 接口 进入接口视图
    [Huawei-Ethernet0/0/1]ip address ip地址 子网掩码 配置ip地址和子网掩码
    [Huawei-Ethernet0/0/1]undo shutdown 启动接口
    [Huawei-Ethernet0/0/1]display interface 接口 查看接口状态
  
  # 六、交换机的登陆
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
  
  # 七、VLAN配置
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
    [Huawei]display port vlan        //查看接口VLAN状态
   
   # 八、交换机端口工作模式
    (一)Access模式(接入模式)
    Access端口只属于单个VLAN，一般用于连接计算机的端口，即只运行设置一个VLAN，丢弃其它VLAN。
    [Huawei]interface GigabitEthernet 0/0/1 进入接口视图
    [Huawei-GigabitEthernet 0/0/1]port link-type access 设
    置端口工作模式为access
    [Huawei-GigabitEthernet 0/0/1]port default vlan ID号 配置端口的缺省的VLAN并将接口加入到指定vlan

    (二)Trunk模式
    Trunk端口允许多个VLAN通过，可以接收和发送多个VLAN报文，一般用于交换机之间端口，只允许默认VLAN报文发送时不打标签，带有标签的数据被转发至另一个交换机Trunk端口。
    [Huawei]interface GigabitEthernet 0/0/1
    [Huawei-GigabitEthernet 0/0/1]port link-type trunk 设置端口工作模式为trunk
    [Huawei-GigabitEthernet 0/0/1]port trunk pvid vlan ID号 指定端口的PVID值
    [Huawei-GigabitEthernet 0/0/1]port trunk allow-pass vlan all/ID号
    允许所有或部分VLAN通过trunk口

    (三)Hybrid模式
    Hybrid端口和Trunk端口一样，不过它既能用于交换机也能用于计算机，允许多个VLAN报文发送时不打标签。
    [Huawei]interface GigabitEthernet 0/0/1
    [Huawei-GigabitEthernet 0/0/1]port link-type hybrid 设置端口工作模式为hybrid
    [Huawei-GigabitEthernet 0/0/1]port hybrid pvid vlan ID号 指定端口的PVID值
    [Huawei-GigabitEthernet 0/0/1]port hybrid tagged vlan ID号
    指定相关VLAN的数据发送时添加Tag
    [Huawei-GigabitEthernet 0/0/1]port hybrid tagged(untagged) vlan all/ID号
    允许hybrid端口对所有或部分VLAN添加(不添加）Tag

   # 九、QinQ技术
    QinQ技术用于解决公网VLAN ID的资源紧缺问题，在IEEE 802.1Q协议标签前再次封装IEEE802.1Q协议标签，其中一层标识用户系统网络，另一层标识网络业务。
    [Huawei]interface GigabitEthernet 0/0/1
    [Huawei-GigabitEthernet0/0/1]port link-type dot1q-tunnel 设置交换机端口类型为QinQ端口

   # 十、VCMP（VLAN集中管理协议）
    VLAN集中管理协议可实现在一台交换机上创建、删除VLAN，提供一种在二层网络中传播VLAN配置信息（域内所有指定的其他交换机自动同步创建、删除相应的VLAN），简单的来说，只需在一台交换机上进行创建、删除VLAN的操作，这些操作会同步至指定的所以交换机，从而大大地减少了工作量，并保证了各修改的一致性。

    1、配置交换机接口的链路类型
    在VCMP管理域中，通过Trunk或Hybrid链路接口连接的同组域名相同的交换机，所以执行命令port link-type { trunk | hybrid }指定接口的链路类型为Trunk或Hybrid，即在进入相应接口后，输入命令port link-type类型，指定配置接口类型。
    2、配置VCMP角色

    配置角色为服务器角色，缺省时，VCMP管理域中的角色是client。
    < Huawei>system-view
    [Huawei]vcmp role server/client/silent/transparent
    3、配置管理域的域名和管理域认证密码

    在同一VCMP管理域内的每台交换机的域名必须是相同的；管理域认证密码这一步是可选的，即也可以不配置认证密码，缺省情况下，没有配置认证密码，VCMP报文直接认证通过。要注意若设置了认证密码，则Server与所有Client上的密码是要保持一致的，执行命令vcmp authentication sha2-256 password 认证密码，配置VCMP管理域的认证密码。
    [Huawei]vcmp 设备ID号 设备名称 配置相应域名
    [Huawei]vcmp authentication 设备名称 password 密码
    [Huawei]interface GigabitEthernet 0/0/1 进入需要使能VCMP功能的以太网接口视图，在二层以太网接口上使能，比如这里就是进入GigabitEthernet 0/0/1接口
    4、使能VCMP功能的接口

    通过interface命令后跟接口名称，进入需要使能VCMP功能的接口视图，使二层以太网处于使能状态，通过执行undo vcmp disable使基于接口使能VCMP功能，缺省情况下，交换机上的所有接口的VCMP功能处于使能状态。
    [Huawei-GigabitEthernet0/0/1]undo vcmp disable 基于该接口使能VCMP功能，缺省情况时则交换机上所有接口的VCMP功能处于使能状态

    十一、GVRP(VLAN注册协议)
    GVRP协议用于注册和注销VLAN属性，手工配置的VLAN称为静态VLAN，而通过GVRP协议创建的VLAN称为动态VLAN。

    < Huawei>system-view
    [Huawei]vcmp role silent 配置GVRP之前必须要将VCMP角色设置为Silent或Transparent
    [Huawei]gvrp 全局使能GVRP功能
    [Huawei]interface GigabitEthernet 0/0/1 进入相关接口
    [Huawei-GigabitEthernet0/0/1]port link-type trunk 配置接口为trunk类型
    [Huawei-GigabitEthernet0/0/1]port trunk allow-pass vlan all 允许所有的VLAN通过该接口
    [Huawei-GigabitEthernet0/0/1]gvrp 在接口下执行命令使能接口GVRP功能
    [Huawei-GigabitEthernet0/0/1]gvrp registration normal 设置GVRP接口注册模式为normal，简化配置

    [Huawei]display gvrp statistics 在交换机上查看接口的GVRP统计信息

   #  十二、STP（生成树协议）
    生成树协议是一种链路管理协议，为网络提供路径冗余，同时防止产生环路。

    < Huawei>system-view
    [Huawei]stp enable 启动生成树协议
    [Huawei]stp root primary 配置本桥为根桥

    [Huawei]display stp brief 在交换机上查看端口状态和端口的保护类型

   # 十三、VRRP(虚拟路由冗余协议)
    虚拟路由冗余协议用于解决局域网中配置静态网关出现单点失效现象的路由协议，可以配置一个交换机群集，通过该协议能实现主设备和备用设备共同分担用户业务的配置。

    < Huawei>system-view
    [Huawei]interface Ethernet0/0/1
    [Huawei- Ethernet0/0/1]ip addres ip地址 子网掩码

    [Huawei]interface Ethernet0/0/2
    [Huawei- Ethernet0/0/2]ip addres ip地址 子网掩码 配置连接主机的接口IP地址
    [Huawei- Ethernet0/0/2]vrrp vrid 1 virtual-ip ip地址 配置备份组1的虚拟网关地址
    [Huawei- Ethernet0/0/2]vrrp vrid 1 priority 优先级 配置路由器在备份组1中的优先级[Huawei- Ethernet0/0/2]vrrp vrid 2 virtual-ip ip地址 配置备份组2的虚拟网关地址

    [Huawei]display vrrp 查看路由器的VRRP状态

   # 十四、BFD（双向转发检测）
    BFD是一种快速检测、监控网络中链路或IP路由的转发连通状况的全网统一的检测机制。

    < Huawei>system-view
    [Huawei]bfd 使能全局BFD功能并进入BFD视图
    *[Huawei]default-ip-address 组播ip地址 配置BFD缺省组播IP地址，缺省情况下，使用组播地址224.0.0.184

    [Huawei]bfd 会话设备名称 bind peer-ip ip地址 interface端口类型 端口号 若有IP地址的三层接口时，创建BFD会话的绑定信息
    /
    [Huawei]bfd 会话设备名称 bind peer-ip default-ip interface 端口类型 端口号 若为二或无IP的三层接口时，创建组播BFD
    [Huawei]discriminator local 标识符值 配置BFD会话的本地标识符
    [Huawei]discriminator remote 标识符值 配置BFD会话的远端标识符
    [Huawei]commit 提交配置

   # 十五、显示路由器的路由
    < Huawei>display ip routing-table 显示路由器的路由
    < Huawei>display ip routing-table verbos 显示路由表的详细信息
    < Huawei>display ip routing-table acl 编号值 显示通过ACL编号为某值过滤的激活路由的概要信息
    < Huawei>display ip routing-table 目标网络的网络地址 子网掩码 网关 根据下一跳显示某目的地址的路由

   # 十六、静态路由、默认路由的配置
    静态路由指定某一网络访问所需要经过的路径，而默认路由是一种特殊的静态路由，当路由表中与包的目的地址之间没有匹配的表项时，路由器做出选择。

    < Huawei>system-view
    [Huawei]ip routing-static 0.0.0.0 0.0.0.0 默认网关地址 配置默认路由，从而简化配置，提高网络性能

    [Huawei]ip routing-static 目标网络的网络地址 子网掩码 网关 配置静态路由，其中网关处的IP地址说明了路由下一站

   # 十七、向当前路由表中添加一条新的路由表条目
    [Huawei]route add 210.43.230.33 mask 255.255.255.224 202.103.123.7 metric 5
    //设定一个到目的网络210.43.230.33的路由，中间经过5个路由器网段，首先经过本地网络上的一个路由器IP为202.103.123.7，子网掩码为255.255.255.224

   # 十八、DHCP（动态主机配置协议）
    动态主机配置协议是基于BOOTP上的改进所来的主机配置协议，通过该协议，DHCP服务器为DHCP客户端进行动态IP地址分配，即不必指明DHCP服务器的IP地址就能获得DHCP服务。

    < Huawei>system-view
    [Huawei]dhcp option template template1 设置分配的分配的启动配置文件
    [Huawei-dhcp-option-template-template1]gateway-list 网关地址 配置网关地址
    [Huawei-dhcp-option-template-template1]bootfile configuration.ini 获取配置文件
    [Huawei-dhcp-option-template-template1]next-server 配置文件地址 配置获取配置文件地址

    (一)接口模式的DHCP命令
    [Huawei]dhcp enable 开启DHCP配置功能
    [Huawei]int g0/0/1 进入相关接口进行接口模式的DHCP配置
    [Huawei-GigabitEthernet0/0/1]ip address ip地址 子网掩码
    [Huawei-GigabitEthernet0/0/1]dhcp select interface 开启接口的DHCP功能
    [Huawei-GigabitEthernet0/0/1]dhcp server excluded-ip-address 单个要排除的ip地址或两个ip地址即范围
    [Huawei-GigabitEthernet0/0/1]dhcp server lease day 天 hour 时 minute 分 设置地址池ip租用有效期
    /*[Huawei- GigabitEthernet0/0/1]lease unlimited 租期无限制
    [Huawei-GigabitEthernet0/0/1]dhcp server dns-list 主要DNS 备用DNS 设置DNS
    [Huawei-GigabitEthernet0/0/1]dhcp select interface 开启接口的DHCP功能使其从接口地址池分配地址

    (二)全局模式的DHCP命令
    [Huawei]dhcp enable
    [Huawei]ip pool HUAWEI 创建全局地址池，pool后跟名称，这里是HUAWEI
    [Huawei-ip-pool-HUAWEI]network ip地址 mask 子网掩码 设置全局地址池的范围
    [Huawei-ip-pool-HUAWEI]getway-list 网关地址 设置分配的网关地址
    [Huawei-ip-pool-HUAWEI]excluded-ip-address ip地址 ip地址 设置不参与动态分配的地址，可以是一个范围
    [Huawei-ip-pool-HUAWEI]dhcp server dns-list 主要DNS 备用DNS 设置DNS
    [Huawei-ip-pool-HUAWEI]lease day 天 hour 时 minute 分 设置地址池ip租用有效期
    /*[Huawei-ip-pool-HUAWEI]lease unlimited 租期无限制
    [Huawei-ip-pool-HUAWEI]static-bind ip-address ip地址 mac-address MAC地址 option- template template1 对某个MAC地址进行绑定，给该MAC地址分配固定的IP地址
    [Huawei]int g0/0/1 进入相关接口
    [Huawei-GigabitEthernet0/0/1]dhcp select global 指定该接口采用全局地址池为客户端分配ip地址
    < Huawei>dis ip pool name 全局地址池名称 all 查看全局地址池的分配信息
