================================================================================
Viavi TestCenter Restful API Python VS Code 辅助插件 说明文档
版本：1.0.0
发布日期：2026-08-11
================================================================================

1. 概述
-------

1.1 简介
    Viavi TestCenter Restful API Python VS Code Helper 是一款专为 Viavi
    TestCenter Restful API 自动化脚本编写而设计的插件。基于 stcrestclient
    HTTP 协议库，通过深度解析 REST 数据模型（data schema），本插件降低了
    HTTP 接口弱类型 API 带来的查阅开销，从而在各主流基于 VS Code 的编辑器
    中提升脚本交付质量与协议仿真开发效率。

1.2 功能速览
    - 交互式代码样例管理器 —— 36 个代码样例，一键插入。
    - 20 个核心 API 方法 —— 输入 `tc.` 即刻生成方法骨架。
    - 上下文推断引擎 —— 自动推断句柄（handle）类型。
    - 智能自动补全 —— 对象类型与命令按需精准提示。
    - 结构化悬停文档 —— 简洁的 Markdown，含 Type / Default / 枚举值。

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
    1. 打开扩展面板（`Ctrl+Shift+X`），找到 Viavi TestCenter Restful API Python VS Code Helper。
    2. 点击齿轮图标（⚙）→ Uninstall（卸载），然后重启编辑器。
    3. 按照上文 2.1 的第 1–4 步安装新的 `.vsix` 文件。

    说明：部分编辑器支持直接在现有版本上安装新的 VSIX —— 旧版本会被自动
    替换，无需手动卸载。


3. 功能覆盖与特性
-----------------

3.1 高频内置代码样例与交互式样例管理器
    本版本内置 36 个可直接使用的代码样例，并在 Python 文件中提供三种快速
    部署工作流。

    3.1.1 三种插入方式
        - [工作流 A] 行内触发：在任意 `.py` 文件中于行首输入 `#`，编辑器
          会立即弹出完整的样例列表。继续输入前缀关键字（如 `#raw_stream`
          或 `#create_bgp`）即可实时过滤，随后按 `Enter` 或 `Tab` 插入；
          `#` 字符会被自动替换为生成的代码。
        - [工作流 B] 完整前缀 + Tab：输入完整的前缀名称（如
          `raw_stream_fixed_frame_ipv4_ttl`），然后按 `Tab` 展开。
        - [工作流 C] 交互式样例菜单（推荐）：按 `Ctrl+Shift+I` 打开两级
          Quick Pick 界面 —— 先选择一个分类，再选择一个样例，代码片段即
          会插入到光标处：

                分类                                     数量
                Raw StreamBlock 样例                      12
                Bound StreamBlock 样例                     6
                Emulated Device 样例                      18

        完整的分步操作说明见 5.1 节。

    3.1.2 可用的样例前缀
        输入 `#` 后接前缀名称即可触发。下方所示的前缀名称即为补全弹窗中
        显示的名称（不显示 `#`）。

        (1) Raw 流量样例（12 个）：
            - raw_stream_ipv4_send_collect_port_results
              端到端 Raw IPv4 流 + 端口级 Tx/Rx 结果订阅。
            - raw_stream_auto_frame_with_sig
              自动帧长 + 插入签名字段。
            - raw_stream_prbs_fill_with_fcs_error
              PRBS 填充 + 插入 FCS 错误。
            - raw_stream_fixed_frame_ipv4_ttl
              固定帧长 + TTL 调整。
            - raw_stream_incr_frame_no_sig
              递增帧长 + 无签名模式。
            - raw_stream_random_frame_constant_fill
              随机帧长 + 恒定填充。
            - raw_stream_bidir_collect_txrx_results
              双向流 + 双端 Tx/Rx 统计。
            - raw_stream_ipv4_tcp_header
              带 EthernetII + IPv4 + TCP 头的 Raw TCP 流。
            - raw_stream_ipv4_udp_header
              带 EthernetII + IPv4 + UDP 头的 Raw UDP 流。
            - raw_stream_ipv6_basic
              带 EthernetII + IPv6 头的 Raw IPv6 流 + 端口统计订阅与采集。
            - raw_stream_ipv4_with_vlan
              带 EthernetII + VLAN + IPv4 头的 Raw 流 + 端口统计订阅与采集。
            - raw_stream_capture_save
              Raw 流量发送 + 端口抓包并保存为 PCAP 文件。

        (2) Bound 流量样例 —— 绑定到仿真设备的 StreamBlock（6 个）：
            - bound_stream_fixed_frame_two_devices
              两台设备之间的固定帧长绑定流。
            - bound_stream_pair_incr_frame
              设备对之间递增帧长的绑定流。
            - bound_stream_auto_frame
              自动帧长绑定流。
            - bound_stream_port_based_load
              基于端口负载的绑定流分配。
            - bound_stream_random_frame_bidir
              随机帧长双向绑定流。
            - bound_stream_ipv6_two_devices
              两台 IPv6 设备（全局 + 链路本地地址）之间的绑定流。

        (3) 仿真设备样例 —— 协议栈（18 个）：
            - create_ipv4_device
              基础静态 IPv4 仿真设备配置。
            - create_l2_ethernet_device_no_ipv4
              纯二层 MAC 仿真设备（无 IPv4）。
            - create_bgp_ipv4_two_devices_with_routes
              IPv4 BGP 双设备 + 路由块配置。
            - create_dhcpv4_server_client_with_traffic
              DHCPv4 Server + Client 完整仿真（含流量）。
            - create_ospfv2_two_devices_lsa
              OSPFv2 两台设备 + LSA 拓扑生成器。
            - create_isis_ipv4_two_devices_lsp
              IS-IS Level-2 IPv4 两台设备 + LSP 拓扑。
            - create_device_group_with_ip_mac_step
              带 IP / MAC / 网关步进配置的多设备组。
            - create_three_devices_one_port
              绑定到同一端口的三台命名设备。
            - create_device_ping_with_routerid
              设备启用 EnablePingResponse=TRUE 并设置 RouterId。
            - create_device_no_ping_with_prefix_length
              设备设置 EnablePingResponse=FALSE 并设置 PrefixLength。
            - create_ipv6_device_basic
              两台设备，含全局 IPv6 + 链路本地 IPv6 完整接口栈配置。
            - create_device_with_vlan
              两台设备，含 VLAN 接口（VlanIf 叠加在 EthIIIf 之上）。
            - create_device_with_vlan_with_stream
              两台 VLAN 设备 + IPv4 over VlanIf 绑定流。
            - create_igmp_host_two_devices_with_stream
              IGMP 主机双设备订阅同一多播组 + 多播绑定流。
            - create_gptp_clock_two_devices
              gPTP（IEEE 802.1AS-2020）时钟双设备 + 结果订阅。
            - create_dot1x_eap_md5
              802.1X Dot1x Supplicant + EAP-MD5 认证配置。
            - create_pppoe_client_server_two_devices
              PPPoE 客户端 + 服务端双设备，含完整 PPPoE/PPP 接口栈。
            - create_bridge_port_config_two_devices
              两台设备 + BridgePortConfig（STP 桥端口优先级仿真）。

3.2 核心 API 方法
    本插件封装了 Viavi TestCenter REST API 的 20 个核心方法。在 Python 上
    下文中输入实例变量名后接 `.`（如 `tc.`），即可立即生成带占位符的标准
    方法结构：
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
    - perform            执行 Viavi TestCenter 命令（含端口预留/释放、
                         结果订阅等）。
    - set_timeout        设置等待服务器响应的超时时间（秒，0 表示不超时）。
    - system_info        获取 Lab Server 的系统信息。
    - upload             向 Lab Server 上传配置文件或其他文件。
    - wait_until_complete 阻塞执行，直至 Sequencer 异步命令完成。

    说明：在 REST API 中，端口预留/释放通过 tc.perform("reservePort"/
    "releasePort") 执行，结果订阅通过 tc.perform("ResultsSubscribe") 执行。

3.3 静态模型与上下文推断引擎
    针对 REST API 弱类型的特性，本插件采用静态 AST（抽象语法树）类型推断
    引擎，以消除不同对象之间的属性名冲突：
    - 创建推断（Creation Inference）：当你输入 `tc.config(hPortTx, )` 时，
      本插件会向上追溯，找到 `hPortTx = tc.create("Port", ...)`，从而将
      `hPortTx` 锁定为 `Port` 实体，并将补全提示限定在其专属的可写属性
      （如 useDefaultHost=）。
    - 获取推断（Retrieval Inference）：支持对子对象关联关系的推断。若某
      句柄通过关联关系获取，如
      `hGenerator = tc.get(hPort, "children-Generator")`，本插件会在后续
      调用中将其正确识别为 `Generator` 实体，并显示对应的计数器与属性。

    说明：本插件自动识别文档中所有 stchttp.StcHttp 实例的变量名（如 tc、
    stc 等），并据此触发上述补全与推断逻辑。

3.4 智能自动补全
    本插件自动扫描文档，识别当前文件中所有 StcHttp 实例的变量名，并在检
    测到对应变量的方法调用时，自动筛选并提供精准的候选建议：
    - 对象类型提示：在 `tc.create("` 内，触发对所有 Viavi TestCenter 对象
      类的自动补全，如 StreamBlock、BgpRouterConfig 等。
    - 命令提示：在 `tc.perform("` 内，填充可用的系统命令，并附带官方
      Markdown 说明（如 AttachPortsCommand）。
    - 属性提示：在 `tc.config(handle, ` 或 `tc.create("Type", parent, `
      内，根据上下文推断引擎锁定的对象类型，精准呈现该对象的可写属性
      及其 Type / Default 信息。

3.5 结构化悬停文档（Hover Provider）
    将鼠标悬停在 Viavi TestCenter 的方法、对象类、属性或命令上，会弹出一
    个精致的 Markdown 窗口。每份文档都经过精确的字段提取：
    - 层级与规则：采用简洁、统一的卡片式视觉布局。
    - 元数据行：显式提取 Type（如 bool、handle）与 Default（默认值）字段，
      并列出有效枚举值及 Deprecated（弃用）标记。
    - 说明描述：从原始数据中剔除残留标点，提供干净的官方描述。


4. 协议支持范围
---------------
本插件的底层数据完整覆盖以下协议：
- 路由协议：BGP、OSPFv2/v3、IS-IS。
- 接入与认证协议：DHCPv4/v6、802.1X Dot1x、PPPoE。
- 组播与时间同步：IGMP、PTP / gPTP。
- 二层协议：STP、VLAN。
- 流量模型：Raw StreamBlock、Bound StreamBlock。
- 结果对象：端口级、流级与协议会话级。


5. 样例用法与代码示例
---------------------

5.1 使用代码样例
    共有三种方式将样例插入到你的 Python 脚本中：

    5.1.1 方式一 —— 输入 `#` 触发行内补全（推荐）
        1. 在任意 `.py` 文件中，于行首输入 `#`。
        2. 编辑器会立即以补全列表形式展示所有可用的样例。
        3. 继续输入关键字进行过滤（如 `#raw_stream` 过滤 Raw 流样例，
           `#create_bgp` 过滤 BGP 设备样例）。
        4. 选中目标样例，按 `Enter` 或 `Tab` 插入 —— `#` 字符会被自动替换
           为完整的代码片段。
        5. 使用 `Tab` / `Shift+Tab` 在占位符之间跳转。

    5.1.2 方式二 —— 输入完整前缀并按 Tab
        1. 在任意 `.py` 文件中，输入完整的样例前缀名称
           （如 `raw_stream_ipv4_send_collect_port_results`）。
        2. 按 `Tab` —— 前缀会展开为一段完整、可运行的代码片段。
        3. 光标跳转到第一个占位符。输入所需值（如 Lab Server IP）。
        4. 按 `Tab` 前进到下一个占位符；按 `Shift+Tab` 返回上一个。
        5. 依次填完所有占位符后，即可运行完整脚本。

    5.1.3 方式三 —— 层级选择器（Ctrl+Shift+I）
        1. 将光标置于 `.py` 文件中的目标插入位置。
        2. 按 `Ctrl+Shift+I`（或打开命令面板运行 `TC: Insert Code Template`）。
        3. 从第一个列表中选择一个分类（右侧显示样例数量）。
        4. 从第二个列表中选择具体的样例（显示前缀与说明）。
        5. 完整片段随即插入 —— 使用 `Tab` / `Shift+Tab` 在占位符之间跳转。

    5.1.4 占位符导航按键
        - Tab          跳转到下一个占位符
        - Shift+Tab    跳转到上一个占位符
        - Escape       退出占位符模式（保留当前已填值）

    5.1.5 示例 —— `raw_stream_ipv4_send_collect_port_results` 的占位符顺序
        1. server_ip  —— Lab Server IP 地址（REST API 服务器，如 192.168.0.200）
        2. user       —— 会话用户名标识（如 JoeUser）
        3. session    —— 会话名称（如 ExampleTest）
        4. chassis_ip —— TestCenter 机箱 IP 地址
        5. tx_slot    —— Tx 端口槽位号
        6. tx_port    —— Tx 端口号
        7. rx_slot    —— Rx 端口槽位号
        8. rx_port    —— Rx 端口号
        9. src_mac    —— 源 MAC 地址（端口 A），默认值：22:22:22:22:22:25
        10. dst_mac   —— 目的 MAC 地址（端口 B），默认值：22:22:22:22:22:22
        11. src_ip    —— 源 IP 地址，默认值：20.0.0.2
        12. dst_ip    —— 目的 IP 地址，默认值：30.0.0.2

5.2 基础代码工作流
    在 `.py` 文件中的一个典型脚本编写流程：

    from stcrestclient import stchttp

    # 连接至 Lab Server 并创建会话
    tc = stchttp.StcHttp("192.168.0.200")
    tc.new_session("JoeUser", "ExampleTest")

    # 1. 方式 A：在 Python 文件中按 'Ctrl+Shift+I' 可视化挑选一个样例框架。
    #    方式 B：自动补全触发候选对象类型，选择 "Project"。
    hProject = tc.create("Project")

    # 2. 定义端口句柄（父对象为位置参数，无需使用 under= 关键字）。
    hPortTx = tc.create("Port", hProject,
                         location="//192.168.0.100/1/1",
                         useDefaultHost="False")

    # 3. 上下文推断将 'hPortTx' 锁定为 'Port' 对象类型。
    #    可写的端口属性会即时弹出，并自动追加等号。
    tc.config(hPortTx, useDefaultHost="False")

    # 4. 命令自动补全：拉取命令并补全内部参数。
    tc.perform("AttachPortsCommand", autoConnect="TRUE")

    # 5. 会话结束后断开机箱并终止服务器端会话。
    tc.disconnect("192.168.0.100")
    tc.end_session(end_tcsession=True)


6. 支持、增强与持续路线图
-------------------------

6.1 持续更新与演进
    本插件处于持续维护中。后续版本将更新数据模型字典，以对齐新的 Viavi
    TestCenter 软件版本，加入更深入的语义分析，并扩充内置代码样例库 ——
    增加更多可直接使用的样例，覆盖更广泛的测试工作流。

6.2 技术支持与反馈联系
    你的反馈对改进本插件至关重要。如遇到任何缺陷、需要技术协助，或希望
    提出功能建议/增强需求，请联系我们的支持团队：

    - 支持邮箱：HSESupportBJ@viavisolutions.com

    欢迎就以下事项与我们联系：
    - 缺陷报告与故障排查：自动补全、悬停或语法问题。
    - 功能请求与增强：结构性新增或改进。
    - 新代码样例/协议提交：希望在后续版本中支持的测试工作流或样例。


7. 重要说明与环境前提
---------------------

7.1 懒加载激活机制
    为保持环境轻量，本插件采用懒加载（lazy-loading）架构。仅当实际打开以
    `.py` 结尾的 Python 文件时，才会激活并加载模型字典，从而确保常规编码
    期间零空闲内存占用。

7.2 前提条件
    - 本插件作为前端语法辅助工具运行，无需在本地安装 TestCenter 应用程序。
    - 需安装 stcrestclient Python 库（pip install stcrestclient）并可访问
      Viavi TestCenter Lab Server，方可执行脚本。
    - 每个 Python 脚本中须包含以下导入语句，插件通过识别该语句定位
      StcHttp 实例，进而激活代码补全与悬停文档功能：
          from stcrestclient import stchttp
    - 本插件仅提供编辑时的智能提示与样例插入，运行时的 HTTP 通信由
      stcrestclient 库负责。
