================================================================================
Viavi TestCenter Restful API Python VS Code 辅助插件 说明文档
版本：1.0.2
发布日期：2026-10-28
================================================================================

1. 概述
-------

1.1 简介
    Viavi TestCenter Restful API Python VS Code Helper 是一款专为 Viavi TestCenter
    Restful API（基于 `stcrestclient` HTTP 协议库）自动化脚本编写而设计的插件。
    通过深度解析 REST 数据模型（data schema），本插件降低了 HTTP 接口弱类型 API
    带来的查阅开销，从而在各主流基于 VS Code 的编辑器中提升脚本交付质量与协议仿
    真开发效率。

1.2 功能速览
    - 内置代码样例与代码块 —— 56 个代码样例 + 7 个代码块，一键插入。
    - 20 个核心 API 方法 —— 输入 `tc.` 即刻生成方法骨架。
    - 上下文推断引擎 —— 自动推断句柄（handle）类型。
    - 智能自动补全 —— 对象类型、命令及属性精准联想。
    - 结构化悬停文档 —— 简洁的 Markdown，含 Type / Default / 枚举值。
    - 序号化代码样例 —— 每个代码样例前缀均带唯一序号（如 `R013`），便于多插件
      共存时通过 `#` 补全区分来源。

1.3 支持的编辑器环境
    以下编辑器均支持本地离线 VSIX 安装：
    - VS Code             (Microsoft)
    - Trae                (ByteDance)
    - Cursor              (SpaceX)
    - Qoder               (Alibaba)
    - Code Buddy          (Tencent)
    - Devin               (Codeium)


2. 安装指南（离线 VSIX 方式）
-----------------------------

2.1 安装步骤
    所有基于 VS Code 架构的编辑器安装步骤一致：
    1. 打开编辑器，进入扩展面板（`Ctrl+Shift+X`）。
    2. 点击右上角的"更多操作"图标（`···`）。
    3. 在下拉菜单中选择 "Install from VSIX..."（从 VSIX 安装）。
    4. 浏览并选择目标 `.vsix` 文件，点击安装，然后重启编辑器。

2.2 更新 / 卸载插件
    如需更新到新版本或进行全新重装：
    1. 打开扩展面板（`Ctrl+Shift+X`），找到 TC Restful API Python Helper。
    2. 点击齿轮图标（⚙）→ Uninstall（卸载），然后重启编辑器。
    3. 按照上文 2.1 的第 1–4 步安装新的 `.vsix` 文件。

    说明：部分编辑器支持直接在现有版本上安装新的 VSIX —— 旧版本会被自动替换，
    无需手动卸载。


3. 功能覆盖与特性
-----------------

3.1 内置代码样例与代码块管理器
    本版本内置 56 个代码样例与 7 个代码块，并在 Python 文件中提供三种快速部署
    工作流。

    3.1.1 三种插入方式
        - [工作流 A] 行内触发：在任意 `.py` 文件中于行首输入 `#`，编辑器会立即
          弹出完整的样例/代码块列表。继续输入前缀关键字（如 `#raw_stream` 或
          `#create_bgp`）即可实时过滤，随后按 `Enter` 或 `Tab` 插入；`#` 字符会
          被自动替换为生成的代码。
        - [工作流 B] 完整前缀 + Tab：输入完整的前缀名称（如
          `R027_config_raw_stream_fixed_frame_ttl`），然后按 `Tab` 展开。
        - [工作流 C] 交互式代码样例菜单（推荐）：按 `Ctrl+Shift+I` 打开两级
          Quick Pick 界面 —— 先选择一个分类，再选择一个代码样例或代码块，代码即会
          插入到光标处：

                分类                                     数量
                Raw StreamBlock 代码样例                 20
                Bound StreamBlock 代码样例                 8
                Emulated Device 代码样例                 27
                Benchmark Test 代码样例                    1
                代码块                                     7

        完整的分步操作说明见 5.1 节。

    3.1.2 可用的代码样例前缀
        输入 `#` 后接前缀名称即可触发。下方所示的前缀名称即为补全弹窗中显示的
        名称（不显示 `#`）。除代码块外，每个代码样例前缀均以唯一序号（`R001`～
        `R056`）开头，便于在同时安装多个 Viavi TestCenter API 插件（如 Native API
        与 ReST API 版本）时，通过 `#` 补全快速区分代码样例的来源与条目，不会因
        前缀相同而混淆。序号为全局连续编号，代码块不参与编号。

        (1) Raw 流量代码样例（20 个）：
            - R025_config_raw_stream_auto_frame_signature
              自动帧长 + 插入签名字段（EthernetII+IPv4，TTL）。
            - R026_config_raw_stream_prbs_fcs_error
              PRBS 填充 + FCS 错误插入。
            - R027_config_raw_stream_fixed_frame_ttl
              固定帧长 + TTL 调整（EthernetII+IPv4）。
            - R028_config_raw_stream_incr_frame
              递增帧长（EthernetII+IPv4，无签名）。
            - R029_config_raw_stream_random_frame_constant_fill
              随机帧长 + 恒定填充（EthernetII+IPv4）。
            - R030_config_raw_stream_tcp
              带 EthernetII + IPv4 + TCP 头的 Raw 流。
            - R031_config_raw_stream_udp
              带 EthernetII + IPv4 + UDP 头的 Raw 流。
            - R032_config_raw_stream_ipv6
              带 EthernetII + IPv6 头的 Raw 流 + 端口统计订阅与采集。
            - R033_config_raw_stream_vlan
              带 EthernetII + VLAN + IPv4 头的 Raw 流 + 端口统计订阅与采集。
            - R034_run_raw_stream_capture_save
              Raw 流量发送 + 端口抓包并保存为 PCAP 文件。
            - R036_config_raw_stream_ipv4
              基础 Raw StreamBlock 配置与结果采集。
            - R037_config_raw_stream_bidirectional
              双向固定帧 Raw 流 + Tx/Rx 结果采集、端口释放与清理。
            - R038_get_port_results
              获取 Generator/Analyzer 端口级结果（Tx/Rx 端口统计）。
            - R039_get_raw_stream_results
              获取 RxStreamSummaryResults/TxStreamResults（逐流统计）。
            - R040_get_raw_stream_loss_results
              获取 Raw 流丢包结果（直接读取 DroppedFrameCount）。
            - R041_get_raw_stream_latency_results
              获取 Raw 流时延结果（AvgLatency/MinLatency/MaxLatency）。
            - R043_config_raw_stream_dscp_phb_numeric
              通过 tosDiffserv+diffServ 配置 DSCP PHB 数值。
            - R044_config_raw_stream_dscp_ecn
              通过 tosDiffserv+diffServ 配置 DSCP PHB + ECN。
            - R055_start_traffic
              启动与停止 StreamBlock 流量。
            - R056_stop_traffic
              配置、启动并停止 StreamBlock 流量（自包含示例）。

        (2) Bound 流量代码样例 —— 绑定到仿真设备的 StreamBlock（8 个）：
            - R019_config_bound_stream_fixed_frame
              两台仿真设备之间的固定帧长绑定流。
            - R020_config_bound_stream_pair_incr_frame
              设备对之间递增帧长的绑定流。
            - R021_config_bound_stream_auto_frame
              自动帧长绑定流。
            - R022_config_bound_stream_port_based_rate
              基于端口负载的绑定流分配。
            - R023_config_bound_stream_bidirectional_random_frame
              随机帧长双向绑定流。
            - R024_config_bound_stream_ipv6
              两台 IPv6 设备（全局 + 链路本地地址）之间的绑定流。
            - R042_config_bound_stream_bidirectional_arp
              双向绑定流配置 + ArpNdStartCommand 解析网关 MAC。
            - R054_get_bgp_bound_stream_results
              获取 BGP 绑定流结果（ProtocolStart + RxStreamSummaryResults）。

        (3) 仿真设备代码样例 —— 协议栈（27 个）：
            - R002_create_device_ipv4
              基础 IPv4 仿真设备配置。
            - R003_create_device_bgp_ipv4_routes
              IPv4 BGP 双设备 + 路由块配置。
            - R004_create_device_dhcpv4_bound_stream
              DHCPv4 Server + Client 完整仿真（含流量）。
            - R005_create_device_ospfv2_lsa
              OSPFv2 两台设备 + LSA 拓扑生成器。
            - R006_create_device_isis_lsp
              IS-IS Level-2 IPv4 两台设备 + LSP 拓扑。
            - R007_create_device_group_ip_mac_step
              带 IP / MAC / 网关步进配置的多设备组。
            - R008_create_devices_one_port
              绑定到同一端口的三台仿真设备。
            - R009_create_device_l2
              纯二层以太网仿真设备（无 IPv4），双端口。
            - R010_create_device_ipv6
              两台仿真设备，含全局 IPv6 + 链路本地 IPv6 接口。
            - R011_create_device_vlan
              两台仿真设备，含 VLAN 接口（VlanIf 叠加在 EthIIIf 之上）。
            - R012_create_device_vlan_bound_stream
              两台 VLAN 设备 + Ipv4If over VlanIf over EthIIIf 绑定流。
            - R013_create_device_igmp_bound_stream
              IGMP 主机双设备订阅同一多播组 + 绑定流。
            - R014_create_device_gptp
              gPTP（IEEE 802.1AS-2020）时钟双设备 + 结果订阅。
            - R015_create_device_dot1x_eap_md5
              802.1X Dot1x Supplicant + EAP-MD5 认证配置。
            - R016_create_device_pppoe
              PPPoE 客户端 + 服务端双设备，含完整接口栈。
            - R017_create_device_stp
              两台设备 + BridgePortConfig（STP 桥端口优先级仿真）。
            - R018_create_device_rocev2_qp
              RoCEv2 Queue Pair 双端口（含 PFC / ECN / CNP / VLAN 配置与流量绑定）。
            - R035_config_device_ping_response
              配置设备 Ping 响应（RouterId、PrefixLength 参数化）— 双设备。
            - R045_get_device_arp_table
              通过 ArpNdUpdateArpCacheCommand 获取端口 ARP 表。
            - R046_run_ping
              通过 PingStartCommand 执行 ICMP Ping 并读取 PingReport。
            - R047_send_bgp_notification
              通过 L2TestBreakLinkCommand 发送 BGP CEASE 通知。
            - R048_config_link_flap
              通过 L2TestBreakLinkCommand + L2TestRestoreLinkCommand 实现链路抖动。
            - R049_get_bgp_state_ipv4
              获取 BGP IPv4 会话状态。
            - R050_get_bgp_state_ipv6
              获取 BGP IPv6 会话状态。
            - R051_get_isis_session_results
              获取 ISIS 会话结果（IsisRouterResults）。
            - R052_create_device_bgp_ipv6_routes
              两台 IPv6 eBGP 设备 + BgpIpv6RouteConfig 配置。
            - R053_create_device_bgp_ipv4_bound_stream
              eBGP IPv4 设备 + 绑定流配置（含 UsesIf）。

        (4) Benchmark Test 代码样例（1 个）：
            - R001_create_rfc2544_throughput
              RFC 2544 吞吐量测试（双设备 + 二分法自动搜索）。

        (5) 代码块（7 个）：
            输入 `#tc_block_` 触发，或从 `Ctrl+Shift+I` 菜单选择"代码块"分类。
            代码块不参与 R0xx 序号编号。
            - tc_block_init
              StcHttp 导入 + Lab Server 连接 + 会话创建。
            - tc_block_project_ports
              Project + 两个端口 + AttachPorts + apply 基础框架代码块。
            - tc_block_device_ipv4
              EmulatedDevice + EthIIIf + Ipv4If 设备创建代码块。
            - tc_block_device_bind_ipv4
              IPv4 设备接口关联关系绑定代码块。
            - tc_block_raw_stream_ipv4
              Raw StreamBlock + EthernetII + IPv4 头流量代码块。
            - tc_block_run_devices
              启动全部设备 + 等待 + 停止全部设备代码块。
            - tc_block_subscribe_port_results
              订阅分析仪与生成器端口级结果代码块。

3.2 核心 API 方法
    本插件封装了 Viavi TestCenter REST API 的 20 个核心方法。在 Python 上下文中
    输入 `tc.`，即可立即生成带占位符的标准方法结构：
    - apply              将当前测试配置提交并应用到机箱。
    - config             设置或修改一个/多个对象属性或关联关系。
    - connect            连接 Viavi TestCenter 机箱。
    - create             在指定父对象下创建自动化对象（如 StreamBlock）。
    - delete             删除指定对象句柄。
    - disconnect         断开与 Viavi TestCenter 机箱的连接。
    - download           从 Lab Server 下载并保存指定文件。
    - download_all       下载 Lab Server 上的所有文件。
    - end_session        结束测试会话（可选择是否同时终止服务器端会话）。
    - files              获取 Lab Server 上的可用文件列表。
    - get                获取属性值、只读数据或句柄。
    - help               查询数据模型与 API 命令的帮助信息。
    - join               加入一个已存在于 Lab Server 上的测试会话。
    - log                写入带严重级别的诊断信息到日志。
    - new_session        在 Lab Server 上创建并加入新的测试会话。
    - perform            执行 Viavi TestCenter 命令（含端口预留/释放、结果订阅等）。
    - set_timeout        设置等待服务器响应的超时时间（秒，0 表示不超时）。
    - system_info        获取 Lab Server 的系统信息。
    - upload             向 Lab Server 上传配置文件或其他文件。
    - wait_until_complete 阻塞执行，直至 Sequencer 异步命令完成。

3.3 静态模型与上下文推断引擎
    针对 REST API 弱类型的特性，本插件采用静态 AST（抽象语法树）类型推断引擎，
    以消除不同对象之间的属性名冲突：
    - 创建推断（Creation Inference）：当你输入 `tc.config(hPortTx, )` 时，本插件
      会向上追溯，找到 `hPortTx = tc.create("Port", hProject, ...)`，从而将
      `hPortTx` 锁定为 `Port` 实体，并将补全提示限定在其专属的可写属性（如
      useDefaultHost=）。
    - 获取推断（Retrieval Inference）：支持对子对象关联关系的推断。若某句柄通过
      关联关系获取，如 `hGenerator = tc.get(hPort, "children-Generator")`，本插件
      会在后续调用中将其正确识别为 `Generator` 实体，并显示对应的计数器与属性。

3.4 智能自动补全
    本插件自动扫描文档，识别当前文件中所有 StcHttp 实例的变量名，并在检测到对应
    变量的方法调用时，自动筛选并提供精准的候选建议：
    - 对象类型提示：在 `tc.create("` 内，触发对所有 Viavi TestCenter 对象类的自动
      补全，如 StreamBlock、BgpRouterConfig 等。
    - 命令提示：在 `tc.perform("` 内，填充可用的系统命令，并附带官方 Markdown 说明
      （如 AttachPortsCommand）。

    注意：`tc.create(object_type, parent, **kwargs)` 中父对象为位置参数，无需使用
    `under=` 关键字。

3.5 结构化悬停文档（Hover Provider）
    将鼠标悬停在 Viavi TestCenter 的方法、对象类、属性或命令上，会弹出一个精致的
    Markdown 窗口。每份文档都经过精确的字段提取：
    - 层级与规则：采用简洁、统一的卡片式视觉布局。
    - 元数据行：显式提取 Type（如 bool、handle）与 Default（默认值）字段，并列出
      有效枚举值及 Deprecated（弃用）标记。
    - 说明描述：从原始数据中剔除残留标点，提供干净的官方描述。


4. 协议与结果对象支持范围
-------------------------
- 路由协议：BGP、OSPFv2/v3、IS-IS。
- 接入与认证协议：DHCPv4/v6、802.1X Dot1x、PPPoE。
- 组播与时间同步：IGMP、MLD、IEEE 802.1AS / gPTP。
- 二层协议：STP / RSTP / MSTP、VLAN。
- RoCEv2。
- RFC 2544：吞吐量（Throughput）、时延（Latency）、帧丢失率（Frame Loss）、
  背靠背（Back-to-Back）四项完整测试。
- 流量模型：Raw StreamBlock（IPv4/IPv6/VLAN/TCP/UDP/DSCP + 抓包保存）、
  Bound StreamBlock（IPv4/IPv6 绑定流、双向流、端口负载配置）。
- 结果对象：端口级、流级与协议会话级。


5. 代码样例/代码块用法与代码示例
----------------------------------

5.1 使用代码样例与代码块
    共有三种方式将代码样例或代码块插入到你的 Python 脚本中：

    5.1.1 方式一 —— 输入 `#` 触发行内补全（推荐）
        1. 在任意 `.py` 文件中，于行首输入 `#`。
        2. 编辑器会立即以补全列表形式展示所有可用的代码样例与代码块。
        3. 继续输入关键字进行过滤（如 `#raw_stream` 过滤 Raw 流代码样例，
           `#create_bgp` 过滤 BGP 设备代码样例，`#tc_block_` 过滤代码块）。
        4. 选中目标条目，按 `Enter` 或 `Tab` 插入 —— `#` 字符会被自动替换
           为完整的代码片段。
        5. 使用 `Tab` / `Shift+Tab` 在占位符之间跳转。

    5.1.2 方式二 —— 输入完整前缀并按 Tab
        1. 在任意 `.py` 文件中，输入完整的代码样例前缀名称
           （如 `R027_config_raw_stream_fixed_frame_ttl`）。
        2. 按 `Tab` —— 前缀会展开为一段完整、可运行的代码片段。
        3. 光标跳转到第一个占位符。输入所需值（如 Lab Server IP）。
        4. 按 `Tab` 前进到下一个占位符；按 `Shift+Tab` 返回上一个。
        5. 依次填完所有占位符后，即可运行完整脚本。

    5.1.3 方式三 —— 层级选择器（Ctrl+Shift+I）
        1. 将光标置于 `.py` 文件中的目标插入位置。
        2. 按 `Ctrl+Shift+I`（或打开命令面板运行 `TC: Insert Code Template`）。
        3. 从第一个列表中选择一个分类（右侧显示代码样例数量）。
        4. 从第二个列表中选择具体的代码样例或代码块（显示前缀与说明）。
        5. 完整片段随即插入 —— 使用 `Tab` / `Shift+Tab` 在占位符之间跳转。

    5.1.4 占位符导航按键
        - Tab          跳转到下一个占位符
        - Shift+Tab    跳转到上一个占位符
        - Escape       退出占位符模式（保留当前已填值）

    5.1.5 示例 —— `R036_config_raw_stream_ipv4` 的占位符顺序
        1. szServerIp      —— Lab Server IP 地址（REST API 服务器），默认值：192.168.0.200
        2. szUser          —— 会话用户名标识，默认值：JoeUser
        3. szSessionName   —— 会话名称，默认值：ExampleTest
        4. szChassisIp     —— TestCenter 机箱 IP 地址，默认值：192.168.0.100
        5. iTxSlot         —— Tx 端口槽位号，默认值：1
        6. iTxPort         —— Tx 端口号，默认值：1
        7. iRxSlot         —— Rx 端口槽位号，默认值：1
        8. iRxPort         —— Rx 端口号，默认值：2
        9. szMacAddrPortA  —— 源 MAC 地址（端口 A），默认值：22:22:22:22:22:25
        10. szMacAddrPortB —— 目的 MAC 地址（端口 B），默认值：22:22:22:22:22:22
        11. txIpAddr       —— 源 IP 地址，默认值：20.0.0.2
        12. rxIpAddr       —— 目的 IP 地址，默认值：30.0.0.2

5.2 基础代码工作流
    在 `.py` 文件中的一个典型脚本编写流程：

    from stcrestclient import stchttp

    tc = stchttp.StcHttp("192.168.0.200")
    tc.new_session("JoeUser", "ExampleTest")

    # 1. 方式 A：按 'Ctrl+Shift+I' 可视化挑选一个框架样例。
    #    方式 B：自动补全触发候选对象类型，选择 "Project"。
    hProject = tc.create("Project")

    # 2. 定义端口句柄（父对象为位置参数，无需 under=）
    hPortTx = tc.create("Port", hProject, location="//192.168.0.100/1/1",
                         useDefaultHost="False")

    # 3. 上下文推断将 'hPortTx' 锁定为 'Port' 对象类型。
    #    可写的端口属性会即时弹出，并自动追加等号。
    tc.config(hPortTx, useDefaultHost="False")

    # 4. 命令自动补全：拉取命令并补全内部参数。
    tc.perform("AttachPortsCommand", autoConnect="TRUE")


6. 支持、增强与持续路线图
-------------------------

6.1 持续更新与演进
    本插件处于持续维护中。后续版本将更新数据模型字典，以对齐新的 Viavi
    TestCenter 软件版本，加入更深入的语义分析，并扩充内置代码样例与代码块库，
    覆盖更广泛的测试工作流。

6.2 技术支持与反馈联系
    你的反馈对改进本插件至关重要。如遇到任何缺陷、需要技术协助，或希望提出功能
    建议/增强需求，请联系我们的支持团队：

    - 支持邮箱：HSESupportBJ@viavisolutions.com

    欢迎就以下事项与我们联系：
    - 缺陷报告与故障排查：自动补全、悬停或语法问题。
    - 功能请求与增强：结构性新增或改进。
    - 新代码样例/协议提交：希望在后续版本中支持的测试工作流或代码样例。


7. 重要说明与环境前提
---------------------

7.1 懒加载激活机制
    为保持环境轻量，本插件采用懒加载（lazy-loading）架构。仅当实际打开以 `.py`
    结尾的 Python 文件时，才会激活并加载模型字典，从而确保常规编码期间零空闲
    内存占用。

7.2 前提条件
    - 需安装 stcrestclient Python 库（pip install stcrestclient），并可访问
      Viavi TestCenter Lab Server。
    - 每个 Python 脚本中须包含 from stcrestclient import stchttp —— 插件通过
      识别该导入语句来定位 StcHttp 实例，进而激活代码补全与悬停文档功能。


8. 本版本（1.0.2）相较 1.0.1 的变更摘要
----------------------------------------

8.1 新增
    - 代码样例新增统一序号前缀（`R001`～`R056`），加在除代码块外全部代码样例的
      prefix 开头，便于在同时安装多个 Viavi TestCenter API 插件（如 Native API
      与 ReST API 版本）时，通过 `#` 补全快速区分代码样例来源，不再因前缀相同
      而混淆。
    - 新增 `Benchmark Test` 独立分类（当前含 1 个代码样例：
      `R001_create_rfc2544_throughput`）。

8.2 变更
    - README/READMECN 文档中的代码样例表格与占位符示例已按 `tc_snippets.json`
      实际当前前缀重新整理。
