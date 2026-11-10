================================================================================
Viavi TestCenter OTG Snappi Python API VS Code 辅助插件 说明文档
版本：1.0.1
发布日期：2026-08-17
================================================================================

1. 概述
-------

1.1 简介
    Viavi TestCenter OTG Snappi Python API VS Code Helper 是一款专为使用
    snappi Python 库进行自动化脚本编写而设计的插件。snappi 是 Open Traffic
    Generator（OTG）API 的客户端实现。通过深度解析 OTG OpenAPI 规范并与
    TestCenter 实现进行交叉比对，本插件降低了在深度嵌套的 OTG 对象层级中查阅
    导航的开销，从而提升脚本交付质量与基于 OTG 的协议仿真开发效率。

1.2 功能速览
    - 交互式代码样例管理器 —— 30 个可直接使用的代码片段，通过 `#` 前缀触发，
      一键插入。
    - 点号触发智能自动补全 —— 基于 21,323 节点静态字典，精准显示子属性候选。
    - 上下文变量类型推断引擎 —— 全文档变量扫描，支持简单赋值与解构赋值推断。
    - 结构化悬停文档 —— 每个属性显示完整 OTG 路径、支持状态、类型、默认值、
      最小/最大值及枚举值。

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
    1. 打开扩展面板（`Ctrl+Shift+X`），找到 OTG Snappi Helper。
    2. 点击齿轮图标（⚙）→ Uninstall（卸载），然后重启编辑器。
    3. 按照上文 2.1 的第 1–4 步安装新的 `.vsix` 文件。

    说明：部分编辑器支持直接在现有版本上安装新的 VSIX —— 旧版本会被自动替换，
    无需手动卸载。


3. 功能覆盖与特性
-----------------

3.1 高频内置代码样例
    在任意 `.py` 文件中输入 `#` 加样例前缀，即可触发匹配的代码片段列表。
    选中后，`#<前缀>` 触发文本会被替换为一段完整、可立即运行的 Python 测试脚本。
    每个样例均自包含 —— 包含所有 import、API 初始化、配置、流量控制与结果
    验证，只需替换脚本顶部的机箱 IP 和端口位置常量，即可直接运行。

    完整的分步插入操作说明见 5.1 节。

    3.1.1 可用样例前缀（共 30 个）

        (1) Raw 端口流量样例（5 个）：
            - #config_flow
              单向 Raw 流基础配置（Ethernet + IPv4）。
            - #config_udp_flow
              单向 Raw 流配置（Ethernet + IPv4 + UDP）。
            - #config_bidirflow
              两条反向端口级 Raw 流（双向流量）配置。
            - #config_flow_rate_percentage
              使用 `rate.percentage` 控制发送速率的单向 Raw 流。
            - #config_link_flap
              端口链路 down/up 闪断（Link Flap）测试。

        (2) 流量控制与指标采集样例（9 个）：
            - #start_flow_by_control
              配置单向 Raw 流并通过 Control State 启动流量。
            - #start_bidirflow_by_snappi
              双向流配置 + 启动（snappi 枚举方式调用 Control State）。
            - #stop_bidirflow
              双向流完整生命周期（配置 → 启动 → 等待 → 停止）。
            - #get_flow_metrics
              单向流配置 → 启动 → 轮询 Flow Metrics → PASS/FAIL。
            - #get_port_metrics
              单向流量 → 轮询 Port Metrics（端口级计数）→ PASS/FAIL。
            - #get_bidirflow_flow_metrics
              双向流 → 启动 → 轮询双向流的 Flow Metrics 汇总。
            - #get_bidirflow_port_metrics
              双向流 → 启动 → 轮询端口级 Metrics 汇总。
            - #get_flow_loss_metrics
              查询流丢包指标（`flow_metrics.loss`）。
            - #get_flow_latency_metrics
              查询流时延指标（`flow_metrics.latency`）。

        (3) 绑定设备流量样例（4 个）：
            - #config_bound_bidirflow
              基于仿真设备接口（Device/IPv4）绑定的双向流配置。
            - #config_bound_bidirflow_arp
              Device 绑定双向流 + 启动协议栈（触发 ARP 解析网关 MAC）。
            - #get_bound_bidirflow_arp_table
              查询 IPv4 邻居表（ARP Cache）验证网关 MAC 是否学习成功。
            - #get_bound_bidirflow_flow_metrics
              Device 绑定双向流完整闭环（配置 → ARP → 发流 → 验证）。

        (4) QoS 样例（3 个）：
            - #config_dscp_ecn
              在 DSCP 基础上叠加 ECN（显式拥塞通知）标记。
            - #config_dscp_phb_numeric
              使用数值型 PHB 配置 DSCP 优先级。
            - #config_dscp_phb_symbolic
              使用符号型 PHB 值列表配置 DSCP 优先级（逐包循环）。

        (5) BGP / 仿真设备样例（8 个）：
            - #config_ebgp
              双侧 eBGP（外部 BGP）会话基础配置。
            - #config_ebgp_flow
              eBGP 会话 + 绑定到 BGP 通告路由的双向流。
            - #config_bgpv6
              双侧 eBGP over IPv6（BGP+）基础配置。
            - #get_ebgp_state
              eBGP 会话建立 + 轮询 BGP 会话状态（session_state == UP）。
            - #get_bgpv6_state
              eBGP over IPv6 会话建立 + 轮询会话状态验证。
            - #get_ebgp_flow_metrics
              eBGP 完整闭环（会话建立 → 路由绑定流量 → 转发验证）。
            - #run_ping
              基于仿真 IPv4 接口发起 ICMP Ping 并验证结果。
            - #send_bgp_notification
              主动发送 BGP NOTIFICATION 报文触发会话终止。

        (6) ISIS 样例（1 个）：
            - #config_isis_session
              ISIS 邻接会话建立 + 轮询验证（PASS/FAIL）。

3.2 点号触发智能自动补全
    在任意 Python 文件中，对任何 OTG 对象输入 `.` 后，编辑器会立即显示来自内部
    字典的精准子属性候选：
    - 属性条目：以属性图标显示。每个条目在详情窗格中展示官方 OpenAPI 描述，并带
      有支持状态徽章："Supported (v1.19.0)" 表示该属性已在 TestCenter 中实现；
      "Not supported"（标记为已弃用）表示该属性属于更广泛的 OTG 规范，但当前
      TestCenter 版本尚不支持。

3.3 上下文变量类型推断引擎
    针对底层 OTG 对象模型弱类型的特性，本插件应用全文档变量扫描引擎，将短别名
    解析为完整的 OTG 类型路径，无需显式类型注解即可对变量进行补全：
    - 简单赋值推断：若写下 `flw = cfg.flows.flow(name='f1')`，则输入 `flw.` 时
      会正确显示限定在 `config.flows.flow` 节点范围内的补全。
    - 解构赋值推断：若写下 `eth, ip, udp = flw.packet.ethernet().ipv4().udp()`，
      每个变量会被独立映射到对应的头部类型。输入 `ip.` 只显示 IPv4 头字段；
      输入 `udp.` 只显示 UDP 头字段。
    推断引擎在每次编辑后重新扫描全文，确保推断类型随脚本演进始终保持准确。

3.4 结构化悬停文档（Hover Provider）
    将鼠标悬停在编辑器中任意 OTG 属性标记上，会弹出一张直接从内部字典生成的
    Markdown 卡片，卡片内容包含：
    - OTG 路径：完整的点分规范键（如 `config.flows.packet.ipv4.src`）。
    - 支持状态："Supported (v1.19.0)" 或 "Not supported"。
    - 说明：经过清理的官方 OpenAPI 描述。
    - 类型与格式：数据类型（如 `string`、`integer`）及格式约束（如 `mac`、
      `ipv4`，如适用）。
    - 默认值：模型定义的默认值（如存在）。
    - 最小值 / 最大值：整数与数字属性的数值范围。
    - 枚举值：具有固定取值集合的字符串属性的完整枚举列表（如 `choice` 属性）。
    悬停功能在关键字参数上下文中同样有效 —— 例如将鼠标悬停在
    `ipv4(address="10.0.0.1", ...)` 中的 `address` 参数上，无需移动光标即可
    查看该参数的 OpenAPI 描述、类型与格式（ipv4 字符串）。


4. OTG 对象与结果覆盖范围
-------------------------
内部字典完整覆盖以下 OTG 命名空间：

- config:          完整的 OTG Config 对象树（ports、flows、devices、lags、
                   layer1、captures、lldp、options），包含所有报文头栈
                   （Ethernet、IPv4、IPv6、TCP、UDP、VLAN、MPLS、GRE、ICMPv4、
                   ICMPv6、ARP、PFC Pause、Custom）及其完整字段层级（fixed
                   value、increment、decrement、random、value_list、
                   metric_tags）。
- api:             顶层 API 方法节点（set_config、get_config、get_metrics、
                   get_states、get_capture、set_control_state、
                   set_control_action 等）。
- config_update:   ConfigUpdate / 增量更新对象树。
- metrics_request: MetricsRequest 及所有子对象（flow、port、bgpv4、bgpv6、
                   isis、lacp、lldp、rsvp 等），含 choice 枚举。
- states_request:  StatesRequest 及所有子对象（bgpv4_peers、isis_lsps、
                   dhcpv4_clients 等），含 choice 枚举。
- control_state:   ControlState 对象（流量发送、端口链路、协议启停），含完整
                   枚举列表。
- control_action:  ControlAction 对象。
- capture_request: CaptureRequest 对象。
- snappi:          顶层 snappi Python 模块路径节点。

支持状态分解：
- TestCenter v1.19.0 已支持：   9,347 个属性
- 仅 OTG 规范（TC 尚未支持）：11,976 个属性


5. 样例用法与代码示例
---------------------

5.1 插入样例
    在任意 `.py` 文件中输入 `#` 加前缀关键字，编辑器会立即以补全列表形式展示
    所有匹配的样例。继续输入进行过滤（如 `#config` 过滤配置类样例，`#get` 过滤
    含采集验证的样例，`#bgp` 过滤 BGP 样例），然后按 `Enter` 或 `Tab` 插入。
    `#<前缀>` 触发文本会被自动替换为完整的可运行代码片段。

    5.1.1 占位常量
        每个样例在脚本顶部暴露三个常量，运行前需替换为实际值：
        1. API  —— OTG 服务器端点地址（如 "0.0.0.0:50051"）
        2. PTX  —— Tx 端口机箱位置（如 "//10.126.32.98/4/5"）
        3. PRX  —— Rx 端口机箱位置（如 "//10.126.32.98/4/6"）

    5.1.2 如何选择合适的样例
        - 基础单向 Raw 流量（仅配置）：使用 `#config_flow`。
        - 基础单向 Raw 流量（含启动 + 采集验证）：使用 `#get_flow_metrics`
          （流级）或 `#get_port_metrics`（端口级）。
        - 双向 Raw 流量：使用 `#config_bidirflow`（仅配置）或
          `#get_bidirflow_flow_metrics`（含完整验证闭环）。
        - 流量需绑定到仿真 IPv4 设备而非 Raw 端口：使用
          `#get_bound_bidirflow_flow_metrics`。
        - 测试需要在发流前完成 BGP 会话建立：使用 `#get_ebgp_flow_metrics` ——
          样例已内置 BGP 会话 UP 轮询循环。
        - 需要时延测量：使用 `#get_flow_latency_metrics` —— 样例启用
          `metrics.latency` 并输出平均/最大时延（纳秒）。
        - 在完整流量测试前验证两台仿真设备的三层可达性：使用 `#run_ping`。
        - 细粒度流量控制（单独启停）：使用 `#start_flow_by_control` /
          `#stop_bidirflow`。

5.2 基础代码工作流
    插入 `#get_flow_metrics` 样例后的典型脚本编写流程：

    import time
    import snappi

    API = "0.0.0.0:50051"
    PTX = "//10.126.32.98/4/5"
    PRX = "//10.126.32.98/4/6"

    api = snappi.api(location=API, transport=snappi.Transport.GRPC)
    cfg = api.config()

    ptx = cfg.ports.port(name="ptx", location=PTX)[-1]
    prx = cfg.ports.port(name="prx", location=PRX)[-1]

    flw = cfg.flows.flow(name="flw")[-1]
    flw.tx_rx.port.tx_name  = ptx.name
    flw.tx_rx.port.rx_names = [prx.name]
    flw.size.fixed = 512
    flw.rate.percentage = 50
    flw.duration.fixed_packets.packets = 1000
    flw.metrics.enable = True

    eth, ip, udp = flw.packet.ethernet().ipv4().udp()
    eth.src.value, eth.dst.value = "00:AA:00:00:04:00", "00:AA:00:00:00:AA"
    ip.src.value,  ip.dst.value  = "10.0.0.1", "10.0.0.2"
    udp.src_port.value = 49152
    udp.dst_port.value = 80

    api.set_config(cfg)

    cs = api.control_state()
    cs.traffic.flow_transmit.state = cs.traffic.flow_transmit.START
    api.set_control_state(cs)

    req = api.metrics_request()
    req.flow.flow_names = ["flw"]
    expected = flw.duration.fixed_packets.packets

    passed = False
    start = time.time()
    while time.time() - start <= 30:
        res = api.get_metrics(req)
        print(res)
        if (res.flow_metrics[0].frames_tx == expected and
                res.flow_metrics[0].frames_rx == expected):
            passed = True
            break
        time.sleep(2)

    print("PASS" if passed else "FAIL")

    # 插入后，变量推断引擎会自动识别所有变量绑定：
    # - `flw` 推断为 config.flows.flow —— 输入 `flw.` 显示流属性补全
    #   （size、rate、duration、metrics、packet 等）。
    # - `eth`、`ip`、`udp` 各自由解构赋值推断得出。
    #   输入 `ip.` 只显示 IPv4 头字段；输入 `udp.` 只显示 UDP 头字段。
    #
    # 示例：如需添加 DSCP 标记，输入 `ip.priority.` → 选择 `choice`，
    # 再输入 `ip.priority.dscp.` → 选择 `phb.` 进入 PHB 字段。

5.3 使用悬停文档查看属性详情
    修改不熟悉的属性前，将鼠标悬停其上即可打开文档卡片。例如，悬停
    `flw.metrics.enable` 显示：
    - OTG 路径：  config.flows.flow.metrics.enable
    - 支持状态：  Supported (v1.19.0)
    - 类型：      boolean
    - 默认值：    false
    - 说明：      为当前流启用流指标采集。


6. 支持、增强与持续更新
-------------------------

6.1 持续更新与演进
    本插件处于持续维护中。后续版本将更新知识库字典，以对齐新的 TestCenter 软件
    版本和 OTG 规范修订，并扩充内置样例库，覆盖更广泛的复杂测试工作流，
    包括更多仿真设备与协议会话场景。

6.2 技术支持与反馈联系
    你的反馈对改进本插件至关重要。如遇到任何缺陷、需要技术协助，或希望提出功能
    建议/增强需求，请联系我们的支持团队：

    - 支持邮箱：HSESupportBJ@viavisolutions.com

    欢迎就以下事项与我们联系：
    - 缺陷报告与故障排查：补全、悬停或推断问题。
    - 功能请求与增强：结构性新增或改进。
    - 新样例与协议需求：希望在后续版本中支持的测试工作流或样例。


7. 重要说明与环境前提
---------------------

7.1 懒加载激活机制
    为保持环境轻量，本插件采用懒加载（lazy-loading）架构。仅当实际打开以 `.py`
    结尾的 Python 文件时，才会激活并加载完整的 21,323 节点字典，确保在其他语言
    的常规编码期间零空闲内存占用。

7.2 前提条件
    - 本插件严格作为前端语法辅助工具运行。如需执行生成的脚本，本地或远程环境
      必须已安装 snappi Python 包（`pip install snappi`），并能连接到正在运行的
      TestCenter OTG 服务器端点。
    - 本插件本身无需联网；完整的 OTG 知识库已作为本地文件打包在 VSIX 包内。
