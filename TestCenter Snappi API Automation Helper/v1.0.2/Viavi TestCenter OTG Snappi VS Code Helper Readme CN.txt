================================================================================
Viavi TestCenter OTG Snappi Python API VS Code 辅助插件 说明文档
版本：1.0.2
发布日期：2026-10-29
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
    - 交互式模板/示例管理器 —— 49 个可直接使用的代码片段，通过 `#` 前缀触发，
      一键插入。
    - 点号触发智能自动补全 —— 基于 25,218 节点静态字典，精准显示子属性候选。
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

3.1 高频内置代码模板/示例
    在任意 `.py` 文件中输入 `#` 加模板/示例前缀，即可触发匹配的代码片段列表。
    选中后，`#<前缀>` 触发文本会被替换为一段完整、可立即运行的 Python 测试脚本。
    每个模板/示例均自包含 —— 包含所有 import、API 初始化、配置、流量控制与结果
    验证，只需替换脚本顶部的机箱 IP 和端口位置常量，即可直接运行。

    完整的分步插入操作说明见 5.1 节。

    3.1.1 可用模板/示例触发词（共 49 个，编号 S001–S049）

        (1) 设备与协议仿真模板/示例（14 个，S001–S014）：
            - #S001_create_device_ipv4
              在两个端口上创建两台基础 IPv4 仿真设备（Ethernet 接口 + 带网关的
              IPv4 接口），是设备创建层的基础模板。
            - #S002_create_device_ipv6
              与 IPv4 版本结构对称的 IPv6 仿真设备创建（IPv6 地址/网关/前缀）。
            - #S003_create_device_l2
              纯二层以太网设备：只配置 Ethernet 接口（MAC/MTU），不挂接三层地址，
              用于二层交换/转发类场景。
            - #S004_create_device_vlan
              带 VLAN 子接口的仿真设备（在 Ethernet 接口下声明 vlans：name/id/
              priority/tpid），验证 VLAN 封装与转发。
            - #S005_create_device_vlan_bound_stream
              在两台 VLAN 设备之间配置引用 IPv4 接口名的双向绑定流，VLAN 标签随
              接口配置自动封装。
            - #S006_create_devices_one_port
              在同一端口批量创建三台 IPv4 设备、另一端口配置一台网关设备，验证
              多设备共享端口与 ARP/转发行为。
            - #S007_create_device_bgp_ipv4_routes
              双侧 eBGP（不同 AS 号）基础配置，各向对端通告一段路由前缀；仅配置，
              会话状态验证见 `#S042_get_bgp_state_ipv4`。
            - #S008_create_device_bgp_ipv4_bound_stream
              eBGP 会话之上追加两条绑定到 BGP 通告路由对象（tx_rx.device 引用
              route 名称）的双向流；仅配置，完整闭环见 `#S044_get_bgp_stream_results`。
            - #S009_create_device_bgp_ipv6_routes
              eBGP over IPv6（BGP+）基础配置，与 IPv4 版本结构对称，通告 IPv6
              前缀；验证见 `#S043_get_bgp_state_ipv6`。
            - #S010_create_device_ospfv2_lsa
              两台仿真设备各自启用 OSPFv2 路由器并在接口加入 area，通告 intra-area
              路由（生成 1 类 LSA），验证邻居建立与 LSA 洪泛。
            - #S011_create_device_isis_lsp
              两台 IS-IS 路由器配置为点对点邻接并生成 LSP；含协议配置与邻接建立。
            - #S012_config_device_ping_response
              配置两台 IPv4 设备后，用协议启停开关（START/STOP）表达被 ping 侧
              是否响应的使能语义；主动发起 ping 见 `#S047_run_ping`。
            - #S013_create_device_dhcpv4_bound_stream
              一台设备运行 DHCPv4 服务器（定义地址池 start_address/count/lease），
              另一台设备作为 DHCPv4 客户端挂在以太网接口下；启动协议栈后由客户端
              发起 DHCP 交互，再查询客户端学到的租约验证地址分配（TestCenter
              v1.55.0 起支持）。
            - #S014_create_device_rocev2_qp
              两端口各建一台 RoCEv2 设备，为 IPv4 接口配置对端 peer 与一个可靠连接
              （RC）QP（source_qp_number/initial_psn/udp_source_port），再配一条以该 QP
              为端点的 RoCEv2 有状态流（config.stateful_flows.rocev2）：起协议栈后由这条
              流量把 QP 落地并发起 CM 握手，轮询 per-peer 计数判 qp_up（QP 只由有状态流
              落地；protocol.rocev2.peers.state=up 不需要，在 QP 存在之前下发它反而会让
              QP 停在 down）。TestCenter v1.55.0 起支持设备层 rocev2；需使用支持 RoCEv2
              仿真的接口板卡端口，OTG 侧无法设置或查询端口的 Performance Mode。

        (2) Raw 报文流模板/示例（13 个，S015–S027）：
            - #S015_config_raw_stream_ipv4
              最基础的单向端口级 Raw 流（Ethernet + IPv4），手工指定源/目的 MAC
              与 IP；仅配置，是本目录的基础 Raw 流模板。
            - #S016_config_raw_stream_ipv6
              单向 Raw 流，网络层换为 IPv6 头并手工指定源/目的 IPv6 地址。
            - #S017_config_raw_stream_udp
              在基础单向流之上追加 UDP 头，构成 Eth/IPv4/UDP 三层报文头栈。
            - #S018_config_raw_stream_tcp
              单向流追加 TCP 传输层头，显式配置源/目的端口。
            - #S019_config_raw_stream_vlan
              在 Ethernet 与 IPv4 之间插入 VLAN 头并设置 vid，验证带标签的二层封装。
            - #S020_config_raw_stream_bidirectional
              两端口间两条反向独立流（f1: p1→p2，f2: p2→p1），各自独立启用流指标。
            - #S021_config_raw_stream_auto_frame
              不显式设置 size，整包长度由协议头栈与 payload 自动决定（auto 帧型）。
            - #S022_config_raw_stream_incr_frame
              帧长在 [start, end] 区间按 step 逐包递增（size.increment），遍历整段
              帧长做转发验证。
            - #S023_config_raw_stream_fixed_frame_ttl
              固定帧长（size.fixed）单向流，并在 IPv4 头显式设置 time_to_live。
            - #S024_config_raw_stream_random_frame_constant_fill
              随机帧长（size.random）+ custom 自定义头以常数字节填充载荷区。
            - #S025_config_raw_stream_dscp_phb_numeric
              IPv4 DSCP 以原始数值 PHB（phb.value，0~63）设置优先级标记。
            - #S026_config_raw_stream_dscp_ecn
              在符号 PHB 基础上叠加 ECN（DS 字段低 2 位）标记配置。
            - #S027_config_raw_stream_pfc_pause
              PFC 优先级流控反压：反向流发 PFC pause 帧（class 3，最大 quanta）
              压制发送端口，正向流带 AF11 DSCP 标记并开启 loss 统计；配置 → 启动
              → 运行 12 秒 → 停止 → 查询正向流的 Tx/Rx/丢包计数。

        (3) 设备绑定流模板/示例（7 个，S028–S034）：
            - #S028_config_bound_stream_ipv6
              两台 IPv6 仿真设备间的双向绑定流；tx_rx.device 引用 IPv6 接口名，
              报文头由仿真接口自动填充。
            - #S029_config_bound_stream_fixed_frame
              基于 IPv4 设备接口的双向绑定流（固定帧长），源/目的 MAC、IP 由仿真
              接口自动填充，无需手工指定头字段。
            - #S030_config_bound_stream_auto_frame
              设备绑定双向流，帧长由协议头栈自动决定（auto 帧型）。
            - #S031_config_bound_stream_pair_incr_frame
              设备绑定双向流，帧长按递增（increment）模式在区间内遍历。
            - #S032_config_bound_stream_bidirectional_random_frame
              设备绑定双向流，帧长按随机（random）分布。
            - #S033_config_bound_stream_bidirectional_arp
              设备绑定双向流 + 启动协议栈，触发 ARP 解析对端网关 MAC，为二层可达
              做准备；ARP 结果验证见 `#S046_get_device_arp_table`。
            - #S034_config_bound_stream_port_based_rate
              演示 Flow.Rate 使用 rate.percentage（占端口最大线速百分比）设定
              发送速率的单向流配置。

        (4) 流量控制模板/示例（3 个，S035–S037）：
            - #S035_start_traffic
              配置单向 Raw 流后，通过 `control_state.traffic.flow_transmit` 显式
              启动流量，演示 Config 与控制两阶段的分离设计。
            - #S036_stop_traffic
              双向流配置 → 启动 → 运行等待 → 停止的完整生命周期管理，适用于需要
              主动控制发流时长或做中间态断言的场景。
            - #S037_config_link_flap
              持续发流过程中对 Tx 端口执行 link-down → link-up 闪断（使用顶层枚举
              `snappi.StatePortLink`），验证链路恢复后全部帧完整收发。

        (5) 指标查询与控制动作模板/示例（12 个，S038–S049）：
            - #S038_get_stream_results
              单向流配置 → 启动 → 轮询流级 Flow Metrics（frames_tx/frames_rx），
              30 秒窗口内 Tx==Rx==预期包数即判 PASS 的完整闭环。
            - #S039_get_port_results
              轮询端口级 Port Metrics（列裁剪只取 FRAMES_TX/FRAMES_RX），对两个
              端口求和判定，适用于只关心端口收发总量的场景。
            - #S040_get_stream_loss_results
              UDP 流启用丢包统计（metrics.loss），以固定等待后单次查询方式输出
              Tx/Rx/丢包计数快照。
            - #S041_get_stream_latency_results
              启用存储转发时延统计（latency.mode=store_forward），输出平均与最大
              时延（纳秒）。
            - #S042_get_bgp_state_ipv4
              eBGP IPv4 邻居：启动协议后轮询 `bgpv4_metrics.session_state` 是否为
              UP，是 BGP 会话建立的最小闭环模板。
            - #S043_get_bgp_state_ipv6
              eBGP+ IPv6 邻居：启动协议后轮询 `bgpv6_metrics` 会话状态，两端均为
              UP 判 PASS。
            - #S044_get_bgp_stream_results
              eBGP 完整闭环：等待会话 UP → 启动绑定到 BGP 通告路由的双向流 →
              轮询流指标验证目标网段可达。
            - #S045_get_isis_session_results
              IS-IS 点对点邻接：轮询 `isis_metrics.l2_sessions_up` 验证会话建立，
              使用扩展的 300 秒请求超时以适配较慢收敛。
            - #S046_get_device_arp_table
              启动协议后通过 `get_states()`（ipv4_neighbors）查询 IPv4 邻居表，
              验证两端网关 MAC 均已解析。
            - #S047_run_ping
              两台 IPv4 设备间通过 `set_control_action()` 发起 ICMP Ping，并验证
              所有响应 result 均为 succeeded。
            - #S048_send_bgp_notification
              eBGP 会话 UP 后，通过 control_action 主动发送 BGP NOTIFICATION
              （Cease / Administrative Shutdown，subcode=
              `admin_shutdown_code6_subcode2`），并验证会话转为 DOWN。
            - #S049_run_raw_stream_capture_save
              在接收端口开启 capture（pcap 格式），发一段 IPv4 UDP 原始流后停止，
              通过 get_capture 取回抓包字节并写入本地 pcap 文件供离线分析
              （TestCenter v1.55.0 起支持 config.captures）。

3.2 点号触发智能自动补全
    在任意 Python 文件中，对任何 OTG 对象输入 `.` 后，编辑器会立即显示来自内部
    字典的精准子属性候选：
    - 属性条目：以属性图标显示。每个条目在详情窗格中展示官方 OpenAPI 描述，并带
      有支持状态徽章："Supported (v1.55.0)" 表示该属性已在 TestCenter 中实现；
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
    - 支持状态："Supported (v1.55.0)" 或 "Not supported"。
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
- TestCenter v1.55.0 已支持：   13,249 个属性
- 仅 OTG 规范（TC 尚未支持）：11,969 个属性


5. 模板/示例用法与代码示例
--------------------------

5.1 插入模板/示例
    在任意 `.py` 文件中输入 `#` 加模板/示例的触发词，编辑器会立即以补全列表形式
    展示匹配的模板/示例；继续输入可缩小列表，然后按 `Enter` 或 `Tab` 插入。
    触发词就是 3.1.1 清单里列出的名字，形如 `S001_create_device_ipv4` —— 前缀
    `S001`–`S049` 即场景编号，与《Summary of Plugin Examples》表格的 ID 列、
    Roadmap 以及缺陷单里引用的编号一一对应。`#<触发词>` 会被自动替换为完整的
    可运行代码片段。

    5.1.1 占位常量
        每个模板/示例在脚本顶部暴露三个常量，运行前需替换为实际值：
        1. API  —— OTG 服务器端点地址（如 "0.0.0.0:50051"）
        2. PTX  —— Tx 端口机箱位置（如 "//10.126.32.98/4/5"）
        3. PRX  —— Rx 端口机箱位置（如 "//10.126.32.98/4/6"）

    5.1.2 如何选择合适的模板/示例
        - 基础单向 Raw 流量：使用 `#S015_config_raw_stream_ipv4`（仅配置下发）或
          `#S038_get_stream_results`（含流级指标 PASS/FAIL 闭环）。
        - 只需统计端口收发总量而非按流细分：使用 `#S039_get_port_results`。
        - 流量需绑定到仿真设备接口而非 Raw 端口：先用 `#S001_create_device_ipv4`
          建设备，再用 `#S029_config_bound_stream_fixed_frame` 配置双向绑定流。
        - 测试需要在发流前完成 BGP 会话建立：使用 `#S044_get_bgp_stream_results` ——
          模板/示例已内置 BGP 会话 UP 轮询循环。
        - 需要存储转发时延测量：使用 `#S041_get_stream_latency_results` —— 模板/示例
          启用 `metrics.latency` 并在帧计数旁输出平均/最大时延（纳秒）。
        - 在完整流量测试前验证两台仿真设备的三层可达性：使用 `#S047_run_ping`。

5.2 基础代码工作流
    插入 `#S038_get_stream_results` 模板/示例后的典型脚本编写流程：

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
    - 支持状态：  Supported (v1.55.0)
    - 类型：      boolean
    - 默认值：    false
    - 说明：      为当前流启用流指标采集。


6. 支持、增强与持续更新
-------------------------

6.1 持续更新与演进
    本插件处于持续维护中。后续版本将更新知识库字典，以对齐新的 TestCenter 软件
    版本和 OTG 规范修订，并扩充内置模板/示例库，覆盖更广泛的复杂测试工作流，
    包括更多仿真设备与协议会话场景。

6.2 技术支持与反馈联系
    你的反馈对改进本插件至关重要。如遇到任何缺陷、需要技术协助，或希望提出功能
    建议/增强需求，请联系我们的支持团队：

    - 支持邮箱：HSESupportBJ@viavisolutions.com

    欢迎就以下事项与我们联系：
    - 缺陷报告与故障排查：补全、悬停或推断问题。
    - 功能请求与增强：结构性新增或改进。
    - 新模板/示例与协议需求：希望在后续版本中支持的测试工作流或模板/示例。


7. 重要说明与环境前提
---------------------

7.1 懒加载激活机制
    为保持环境轻量，本插件采用懒加载（lazy-loading）架构。仅当实际打开以 `.py`
    结尾的 Python 文件时，才会激活并加载完整的 25,218 节点字典，确保在其他语言
    的常规编码期间零空闲内存占用。

7.2 前提条件
    - 本插件严格作为前端语法辅助工具运行。如需执行生成的脚本，本地或远程环境
      必须已安装 snappi Python 包（`pip install snappi`），并能连接到正在运行的
      TestCenter OTG 服务器端点。
    - 本插件本身无需联网；完整的 OTG 知识库已作为本地文件打包在 VSIX 包内。
