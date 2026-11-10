================================================================================
Viavi ONE LabPro API VS Code 辅助插件 说明文档
版本：0.3.2
发布日期：2026-10-30
================================================================================

1. 概述
-------

1.1 简介
    Viavi ONE LabPro API VS Code Helper 是一款专为使用 Viavi ONE LabPro
    Python 对象树 API（onelabpro_pyapi，SDK 5.0.0）编写自动化测试脚本而设计的
    智能辅助插件。插件覆盖 3,788 个 API 节点，在路径感知补全、悬浮文档与签名
    帮助等方面提供完整支持，帮助测试工程师在无需翻阅接口文档的情况下，快速、
    准确地完成 ONE LabPro pyapi 测试脚本的编写。

1.2 功能概览
    - 路径感知补全 —— 在对象链后输入 `.` 即弹出当前层级的子节点列表；插件追踪
      变量别名（`sc = ctrl.Scenarios[id]`、`pf = getattr(port, PROFILE)` 等），
      确保补全基于真实 API 路径而非仅靠名称模糊匹配。
    - 子节点补全 —— 对集合类节点（Scenarios / Ports 等）自动穿透 item_child
      层级，输入 `.` 后直接显示子节点（add / list / close / L0 / L1 / L2 等）。
    - Helper 函数补全 —— 在 `olp_helpers.` 后自动弹出全部 11 个 helper 函数列表。
    - 悬浮文档 —— 鼠标悬停在任意节点名称上，显示结构化文档卡片（节点描述、
      API 路径、子节点列表、参数说明）。
    - 签名帮助 —— 输入 `(` 后实时显示参数签名，当前参数高亮显示。
    - 代码片段（Snippets）—— 内置 49 个完整测试脚本 + 92 个函数调用片段。
      在 .py 文件中输入 `#` 触发完整测试脚本列表，输入 `##` 触发函数片段列表；
      选中后按 Enter 展开，用 Tab 在占位符之间跳转。
    - 导入别名自动识别 —— 自动扫描当前文件，识别 `import onelabpro_pyapi as <alias>`
      与 `import onelabpro_pyapi.helpers as <alias>` 两种导入写法。

1.3 支持的编辑器环境
    以下编辑器均支持本地离线 VSIX 安装：
    - VS Code              (Microsoft，需 1.93.0 及以上版本)
    - Trae                 (ByteDance)
    - Cursor               (Anysphere)
    - Qoder                (Alibaba)
    - Code Buddy           (Tencent)


2. 安装指南（离线 VSIX 方式）
-----------------------------

2.1 安装步骤
    所有基于 VS Code 架构的编辑器安装步骤一致：
    1. 打开编辑器，进入扩展面板（Ctrl+Shift+X）。
    2. 点击右上角的"更多操作"图标（···）。
    3. 在下拉菜单中选择 "Install from VSIX..."（从 VSIX 安装）。
    4. 浏览并选择目标 .vsix 文件，点击安装，然后重启编辑器。

    命令行安装（VS Code）：
        code --install-extension onelabpro-pyapi-helper-0.3.2.vsix

    英文界面版：
        code --install-extension onelabpro-pyapi-helper-en-0.3.2.vsix

2.2 更新 / 卸载插件
    如需更新到新版本或进行全新重装：
    1. 打开扩展面板（Ctrl+Shift+X），找到 Viavi ONE LabPro API VS Code Helper。
    2. 点击齿轮图标（⚙）→ Uninstall（卸载），然后重启编辑器。
    3. 按照上方 2.1 的第 1—4 步安装新的 .vsix 文件。

    说明：部分编辑器支持直接在现有版本上安装新版 VSIX —— 旧版本会被自动替换，
    无需手动卸载。


3. 功能覆盖与特性
-----------------

3.1 路径感知补全
    在对象链后输入 `.`，自动弹出当前路径层级的子节点列表，每项均带有节点类型
    与简短说明。

    补全示例：
        ctrl.Scenarios.        → add / list / close / save / closeIdle / Saved
        ctrl.Assets.Modules.   → list
        sc.Ports.              → add / list / clone / remove / Profiles / Filters
        port.L1.Pcs.Fec.       → Alarms / Errors / set / states
        olp_helpers.           → checkLinkUp / checkTransceiverReady 等 11 个

    变量别名追踪（全链路）：
        ctrl = pyapi.Controller(host, ...)        # ctrl → API 根
        sc   = ctrl.Scenarios[sc_data['id']]      # sc → Scenarios
        port = sc.Ports[port_data['id']]          # port → Ports[id]
        pf   = getattr(port, PROFILE)             # pf → profile 节点
        for port in (port_w, port_e):             # 循环变量同样被追踪
            pf = getattr(port, PROFILE)
            pf.L0.Unframed.Pattern.set(...)       # 正确解析到 L0.Unframed.Pattern.set

3.2 悬浮文档（Hover Provider）
    鼠标悬停在任意 pyapi 节点或 helper 函数上，弹出结构化文档卡片：

        悬停对象                         显示内容
        ------------------------------   ------------------------------------------
        ctrl.Scenarios                   节点描述、API 路径、可调方法、子节点列表
        sc.Ports.add                     方法签名、参数名与类型、示例返回值
        port.L1.Pcs.Fec                  路径、子节点（Alarms/Errors/set/states）
        olp_helpers.checkLinkUp          函数签名、参数描述

    路径感知举例：
        sc = ctrl.Scenarios[id] → sc.Ports.add(…)
        悬停 add 显示 Ports.add 文档，而非 Scenarios.add。

3.3 签名帮助（Signature Help）
    调用方法时，输入 `(` 后实时显示参数签名，当前光标所在参数高亮显示：

        ctrl.Scenarios.add(focus=..., name=..., ...)
                           ^^^^^
                           # 当前高亮参数随光标位置自动切换

        sc.Ports.add(profile=..., count=..., name=..., orientation=..., ...)
        olp_helpers.checkLinkUp(*ports, count=..., interval=..., timeout=...)

3.4 代码片段（Snippets）
    内置 49 个完整测试脚本与 92 个函数调用片段，均在 .py 文件中自动激活。

    触发方式：
        #   → 弹出完整测试脚本列表（49 个），含参数块、try/finally、断言
        ##  → 弹出函数调用片段列表（92 个），单个 API 调用，可插入已有脚本

    输入 # 或 ## 后继续输入关键词可缩小范围；按 Enter 展开，用 Tab/Shift+Tab
    在占位符之间跳转。完整的片段列表见第 5 节。


4. API 覆盖范围（SDK 5.0.0）
-----------------------------
插件内嵌元数据完整覆盖以下内容：

    类别                       说明
    -------------------------  --------------------------------------------------
    pyapi 元数据节点总数        3,788 个节点（从 nodes.py 动态提取）
    顶层命名空间节点            8 个（Scenarios / Assets / Licensing 等）
    Scenarios 子树最大深度      6 层（ctrl → Scenarios → [id] → Ports →
                               [id] → L1 → Pcs → Fec）
    Helper 函数                 11 个
    完整测试脚本                49 个
    函数调用片段                92 个


5. 代码片段用法与代码示例
--------------------------

5.1 使用代码片段
    在任意 .py 文件中输入 `#`（完整脚本）或 `##`（函数片段），编辑器自动弹出
    匹配列表，继续输入关键词可缩小范围；按 Enter 展开，然后依次按 Tab 跳转
    并填写各占位符。

5.2 完整测试脚本（49 个）
    每个脚本均包含：顶部参数块（Tab 跳转填写控制器 IP、端口等）、try/finally
    错误处理、logging.info 输出和结果断言。

    (1) 入门 / 环境验证
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP001_probe_hardware              探测控制器所有模块及空闲硬件端口，输出端口清单
        OLP002_run_getting_started         Hello World：连接→列举模块/Profiles/运行场景→关闭
        OLP003_verify_installation         安装验证：检查 import/olp_helpers/Controller 可用性

    (2) 资产 / 硬件清单
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP004_query_assets                查询模块详情 + License 列表 + 收发器信息
        OLP005_inventory_hardware          全硬件清单：模块/端口/收发器/License/空闲端口汇总
        OLP006_discover_profiles           探测所有可映射 profile（线速率/介质类型/空闲端口数）

    (3) 场景管理
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP007_manage_scenario_basic       场景全生命周期：创建→保存→列举→加载→关闭
        OLP008_run_scenario_full_lifecycle  完整生命周期：创建→添加端口→运行→保存→列举→关闭
        OLP009_manage_saved_scenarios      列举已保存场景→按名加载→重跑流量→可选删除旧场景
        OLP010_cleanup_idle_scenarios      closeIdle + 运行中/已保存场景审计（dry-run）
        OLP011_scenario_load_saved_active  保存+重载完整流程（Saved.list + Saved.load(...)），支持按名加载

    (4) 端口映射
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP012_run_container_pattern       Container 封装模式（自动 remove），适合脚本框架
        OLP013_map_free_ports_auto         自动发现某 profile 下空闲硬件端口并映射
        OLP014_discover_and_map_ports      自动发现空闲 HW 端口→映射→运行 L2L3 流量
        OLP015_switch_port_focus           PHY 场景→关闭→L2L3 复用同端口，验证无需重启

    (5) L2L3 流量
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP016_run_l2l3_traffic            L2L3 双向流量，TfgClusters RAW，RxFlows 聚合统计
        OLP017_verify_l2l3_flow_loss       L2L3 + 逐流 TX/RX 等值断言（零丢包）
        OLP018_run_l2l3_multi_framesize    顺序多帧长（64/512/1518 字节），每帧长汇总
        OLP019_get_l2l3_port_stats_detail  L2L3 + L2 FrameLayer + L0 主机频率 + PCS 统计
        OLP020_poll_l2l3_continuous        长时运行：持续流量 + 周期端口健康轮询
        OLP021_run_l2l3_port_orientation   L2L3 + 显式东/西向 orientation，验证 port.get()
        OLP022_run_l2l3_repeated_measurements  N 轮重复测量（start→stop→readstats）
        OLP023_inject_l2l3_fec_error       L2L3 基线 + FEC 注入对比（比较丢包差值）
        OLP024_raw_traffic_vlan_udp        L2L3 RAW VLAN/Ipv4/Udp（A→B），Layers.add 模式，零丢包
        OLP025_send_custom_payload         RAW 流量 + ViaviTfl CUSTOM_REPEAT 自定义载荷模式
        OLP026_traffic_vlan_tcp            L2L3 DevClusters Ipv4 + TCP 层双向流量

    (6) PHY / PRBS 测试
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP027_run_phy_prbs                PHY 非成帧 PRBS BER，支持 PRBS31Q/SSPRQ/PRBS9/PRBS13Q
        OLP028_run_phy_prbs_multi_pattern  PHY 顺序多码型，每码型读取 PCS + FEC
        OLP029_switch_phy_fec_mode         FEC 模式循环切换（NONE→RS→FC），验证协调状态
        OLP030_check_phy_alignment_skew    对齐偏移 + 通道映射 + 逐通道 PCS 状态读取
        OLP031_monitor_phy_host_freq       L0 主机接口 Tx/Rx 频率轮询（N 次，双端口）
        OLP032_get_phy_xcvr_details        收发器详情 + RxMapped + 主机频率 + L2 FrameLayer
        OLP033_check_phy_per_lane          PHY 逐通道 PCS 状态（100G/400G 多通道）
        OLP034_run_phy_prbs_ssprq          SSPRQ 基线 PHY，验证 PCS 协调 + FEC 告警消除
        OLP035_enable_an_lt                PHY AN（AutoNegotiation）+ LT（LinkTraining）配置
        OLP036_i2c_readwrite               ONE-1600 PHY I2C Dump/Peek/Poke 操作

    (7) FEC / 告警 / 端口健康
        前缀                       描述
        -------------------------  ----------------------------------------
        OLP037_inject_fec_error            FEC 错误注入（start→读告警/误码→stop）
        OLP038_monitor_port_summary        端口健康周期监控，L0/L1/L2 汇总 + 告警事件日志
        OLP039_poll_fec_alarm              FEC 告警/PCS 协调周期轮询
        OLP040_monitor_xcvr_power          收发器状态 + RxMapped 周期轮询
        OLP041_inject_fec_error_rounds     N 轮 FEC 注入 + 告警/误码读取，每轮汇总
        OLP042_detect_pcs_fault            FEC 注入→东侧告警出现→停注入→告警消除 验证
        OLP043_detect_link_flap            N 轮链路闪断（Flap）检测，输出每次闪断事件日志
        OLP044_health_check_debug          控制器健康统计 + Debug Dump 下载 URL
        OLP045_stats_frame_pcs_fec         PHY 端口 Frame/PCS/FEC/B64B66 统计 + FEC 模式设置
        OLP046_rx_service_disruption       PHY Rx 服务中断传感器 + FEC_UNCORR 注入
        OLP047_alarms_errors_insertion     完整告警+错误套件：AlarmFec/AlarmReconciliation/ErrorFec/ErrorFrame
        OLP048_fec_validation              RAW A→B + 四类 FEC 验证（ErrorFec/AlarmFec/AlarmReconciliation/ErrorTranscoding）
        OLP049_transceiver_health_config   HSE800 PHY 收发器健康迭代：MsaInfo/Health/OpticalPower/Control

5.3 函数调用片段（92 个）
    单个操作的最小片段，可直接插入已有脚本。

    (1) 连接（connect.json，3 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        connect                    账号密码方式连接控制器
        connect_token              JWT Token 方式连接
        connect_context            with 上下文管理器连接（自动清理）

    (2) 场景管理（scenarios.json，6 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        scenario_create            创建场景（L2L3 / PHY focus 可选）
        scenario_list              列举所有运行中场景（id/name/focus）
        scenario_save              保存当前场景到命名存档
        scenario_load              按名加载已保存场景
        scenario_close             关闭运行中场景
        scenario_container         Container 封装模式（自动 remove）

    (3) 端口操作（ports.json，12 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        port_add                   添加端口（profile 枚举选择）
        port_list_profiles         列举所有可映射 profile
        port_map_single            映射单端口到硬件（module/hw_port）
        port_map_multi             批量映射多端口（mapPortsById）
        port_check_link            阻塞等待链路 UP（checkLinkUp）
        port_check_transceiver     等待收发器达到 ModuleReady
        port_get_link_state        非阻塞读取链路状态
        port_summary               读取 L0/L1/L2 汇总状态（getPortSummary）
        port_summary_ok            检查所有层是否全部 OK（无告警）
        port_set                   设置端口名称/描述
        port_states                读取端口 L1/L2 状态标志
        port_free_mappings         查询 profile 下空闲硬件端口

    (4) L1/L0/L2（l1_l2.json，17 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        l1_pcs_states              读取 PCS 协调状态 + FEC 告警 + FEC 误码
        l1_pcs_fec_set             设置 FEC 模式（NONE / RS / FC）
        l1_alignment_skew          读取 PCS 对齐偏移和通道映射
        l1_pcs_lanes               读取逐通道 PCS 状态
        l1_unframed_prbs           配置非成帧 PRBS Tx/Rx 码型
        l0_transceiver_stats       读取 L0 收发器状态和检测类型
        l0_host_interface          读取 L0 主机接口 Tx/Rx 频率
        l2_frame_layer             读取 L2 FrameLayer 帧计数和错误
        error_fec_inject           FEC 错误注入 start/stop
        payload_custom_fixed       CUSTOM_FIXED Payload（固定 hex）
        payload_increment          INCREMENT_BYTE Payload（步进 hex）
        rxflows_verify             逐流 TX/RX 等值断言（零丢包）
        measurement_run            start / sleep / stop + 读 RxFlows
        l1_fec_hser_inject         FEC HSER 连续注入 + 读告警/误码
        l1_xcvr_power_read         L0 收发器状态 + RxMapped 读取
        l1_pcs_summary             PCS 协调 + FEC 告警 + FEC 误码一次性汇总
        l1_port_summary_detail     getPortSummary 分层告警提取

    (5) Helper 工具函数（helpers.json，9 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        helpers_checkLinkUp        阻塞等待链路 UP
        helpers_checkTransceiverReady 等待收发器就绪
        helpers_getLinkState       非阻塞读取链路状态
        helpers_mapPortToHardware  映射单端口到硬件
        helpers_mapPortsById       批量映射多端口
        helpers_getPortSummary     获取 L0/L1/L2 端口汇总
        helpers_checkPortSummaryAllOk 断言所有端口无告警
        helpers_payload_fixed      CUSTOM_FIXED Payload 字典
        helpers_payload_increment  INCREMENT_BYTE Payload 字典

    (6) 高级功能（advanced_pyapi.json，45 个）

        流量 / TFG（8 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        scenario_close_idle        关闭空闲超时场景（dry-run 安全）
        helpers_payload_repeat     CUSTOM_REPEAT Payload 字典
        helpers_payload_decrement  DECREMENT_BYTE Payload 字典
        allflows_list              列举 AllFlows，逐流 TX/RX 统计
        alltfgs_list               列举场景内所有 TFG（id/name/state）
        tfgcontrol_start           TfgControl.start() 启动所有 TFG
        tfgcontrol_stop            TfgControl.stop() 停止所有 TFG
        rxflow_rate_calc           两次快照差值计算实时 Rx 帧率

        高级端口操作（9 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        port_states_l1l2           port.states(L1Summary, L2Summary)
        port_get_details           获取端口完整配置（name/orientation/profile）
        port_clone                 克隆端口
        port_remove                移除端口
        port_set_orientation       设置端口东/西向
        port_count_add             一次 add 多个端口（count 参数）
        port_filters_list          列举场景内端口过滤器
        port_profiles_list         列举所有可映射 profile（线速率/空闲数）
        port_map_single_auto       映射端口 + 等待收发器就绪

        高级场景管理（7 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        scenario_saved_list        列举已保存场景（name/savedAt）
        scenario_saved_remove      按名删除已保存场景
        scenario_close_by_name     在运行中场景列表中按名关闭
        scenario_list_running      列举所有运行中场景
        scenario_create_phy        创建 PHY 场景
        hw_ports_list              列举场景内已分配硬件端口
        mappings_list              列举场景内端口-硬件映射关系

        高级 L1 PHY 操作（9 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        l1_pcs_alignment_read      读取 PCS 对齐偏移值 + 通道映射
        l1_fec_mode_rs             设置 FEC 为 RS（Reed-Solomon）
        l1_fec_mode_none           禁用 FEC（NONE）
        l1_fec_mode_fc             设置 FEC 为 FC（FireCode）
        l1_host_freq_both          L0 主机接口 Tx + Rx 频率一次读取
        l1_unframed_ssprq          配置 SSPRQ 非成帧码型（IEEE 100G/400G）
        l1_unframed_prbs31q        配置 PRBS31Q 非成帧码型
        pcs_reconciliation_check   双端口 PCS 协调状态读取并记录
        fec_errors_check           双端口 FEC 告警 + 误码计数读取

        高级 L0 / L2 / 工具（3 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        l0_xcvr_full_details       完整收发器详情（状态/检测/厂商/PN/RxMapped）
        l2_framelayer_full         L2 FrameLayer 帧计数和错误读取
        error_fec_stop             停止 FEC 错误注入

        硬件 / 资产查询（2 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        assets_modules_list        模块列表（端口数/固件版本/空闲端口）
        licensing_list             License 列表（类型/状态/到期时间）

        高级 Helper / 连接（7 个）
        前缀                       描述
        -------------------------  ----------------------------------------
        helpers_get_link_state     getLinkState 逐端口状态 dict
        helpers_map_ports_by_id    mapPortsById 批量映射
        helpers_check_port_ok      checkPortSummaryAllOk + 断言告警
        connect_no_verify          关闭 TLS 验证连接（自签名证书）
        helpers_retry_connect      连接失败自动重试（N 次，含延迟）
        modules_free_ports         遍历所有模块汇总空闲端口列表
        port_summary_all           读取场景内所有端口告警状态汇总

5.4 典型脚本骨架
    import onelabpro_pyapi as pyapi
    import onelabpro_pyapi.helpers as olp_helpers
    import logging, time

    logging.basicConfig(level=logging.INFO)

    CTRL_HOST = '10.86.88.19'
    PROFILE   = 'ONE800_OSFP_100GAUI2_L2L3_ETHERNET_BREAKOUT'
    MODULE_W  = '2'
    HW_PORT_W = '5'
    MODULE_E  = '2'
    HW_PORT_E = '6'
    DURATION  = 10

    # 1. 连接
    ctrl = pyapi.Controller(CTRL_HOST, auth_credentials=('admin', 'Admin123'))
    ctrl._session.trust_env = False

    # 2. 创建场景
    sc_data = ctrl.Scenarios.add(focus='L2L3', name='my-test')
    sc = ctrl.Scenarios[sc_data['id']]

    try:
        # 3. 添加端口并映射到硬件
        pw_data = sc.Ports.add(profile=PROFILE)
        pe_data = sc.Ports.add(profile=PROFILE)
        port_w  = sc.Ports[pw_data['id']]
        port_e  = sc.Ports[pe_data['id']]
        olp_helpers.mapPortsById({port_w: f'{MODULE_W}/{HW_PORT_W}',
                                   port_e: f'{MODULE_E}/{HW_PORT_E}'})

        # 4. 等待链路 UP
        olp_helpers.checkLinkUp(port_w, port_e, timeout=60)
        logging.info('Links up')

        # 5. 运行流量
        sc.Measurement.start()
        time.sleep(DURATION)
        sc.Measurement.stop()

        # 6. 读取统计
        flows    = sc.RxFlows.list()
        total_tx = sum(f.get('txFrameCount', 0) for f in flows)
        total_rx = sum(f.get('rxFrameCount', 0) for f in flows)
        logging.info(f'tx={total_tx:,}  rx={total_rx:,}  lost={total_tx-total_rx}')
        assert total_tx == total_rx, 'Frame loss detected'

        # 7. 读取 L1 状态
        rec = port_w.L1.Pcs.Reconciliation.states()
        fec = port_w.L1.Pcs.Fec.Alarms.states()
        logging.info(f'PCS={rec}  FEC alarms={fec}')

    finally:
        # 8. 关闭场景
        ctrl.Scenarios.close(id=sc_data['id'])
        logging.info('Done.')

    编写过程中：
    - 输入 `ctrl.` 触发顶层节点补全（Scenarios / Assets / Licensing 等）。
    - 输入 `sc.Ports.` 触发端口子节点补全（add / list / clone / remove 等）。
    - 输入 `port.L1.Pcs.Fec.` 触发 Fec 子节点补全（Alarms/Errors/set/states）。
    - 输入方法括号后（如 `sc.Ports.add(`）触发签名帮助。
    - 鼠标悬停在任意节点名称上，弹出路径感知文档卡片。


6. Helper 函数参考
------------------

    函数                                      说明
    ----------------------------------------  ----------------------------------
    checkLinkUp(*ports, count, interval,      阻塞等待所有端口链路 UP
        timeout)
    checkTransceiverReady(*ports, timeout)    等待收发器达到 ModuleReady 状态
    getLinkState(*ports)                      非阻塞获取链路状态（dict: id→0/1）
    mapPortToHardware(port, module_id,        映射单个场景端口到硬件
        hw_port_id)
    mapPortsById(mappings)                    批量映射多端口（dict: port→'m/p'）
    getPortSummary(*ports)                    聚合读取 L0/L1/L2 端口汇总状态
    checkPortSummaryAllOk(*ports)             检查所有端口层是否全部 OK（无告警）
    configurePayloadCustomFixedHex(hex)       生成 CUSTOM_FIXED Payload 配置字典
    configurePayloadCustomRepeatHex(hex)      生成 CUSTOM_REPEAT Payload 配置字典
    configurePayloadIncrementByteHex(base)    生成 INCREMENT_BYTE Payload 配置字典
    configurePayloadDecrementByteHex(base)    生成 DECREMENT_BYTE Payload 配置字典


7. 键盘快捷键
-------------

    操作                              快捷键
    --------------------------------  ------------------------------------------
    触发签名帮助（显示参数列表）      输入 (
    触发枚举值 / 子节点列表           输入 . 或 Ctrl+Space
    查看悬浮文档                      悬停鼠标 / Ctrl+I
    手动触发补全                      Ctrl+Space
    展开片段后跳到下一个占位符        Tab
    展开片段后跳到上一个占位符        Shift+Tab
    退出片段模式（最后占位符 $0 处）  Tab 或 Escape


8. 支持、增强与持续更新
------------------------

8.1 持续更新与演进
    本插件处于持续维护中。后续版本将持续完善 API 节点覆盖与参数元数据，
    并新增更多场景化代码片段，覆盖更广泛的 pyapi 测试工作流。

8.2 技术支持与反馈联系
    您的反馈对改进本插件至关重要。如遇任何缺陷、需要技术协助，或希望提出
    功能建议，请联系我们的支持团队：

    - 支持邮箱：HSESupportBJ@viavisolutions.com

    欢迎就以下事项与我们联系：
    - 缺陷报告（补全、悬浮或签名帮助异常）。
    - 功能请求（新增节点/参数覆盖或代码片段模板）。
    - 测试脚本需求（希望在后续版本中支持的测试工作流）。


9. 重要说明与环境依赖
---------------------

9.1 激活机制
    插件采用按语言激活（onLanguage:python）机制，仅当打开 .py 文件时才会
    激活，确保在编写其他语言代码时零额外开销。

9.2 前提条件
    - VS Code / Trae / Cursor / Qoder / Code Buddy 任意一款（VS Code 需 1.93.0
      及以上版本）。
    - 本插件严格作为前端语法辅助工具运行。如需实际执行生成的测试脚本，本地
      或远程运行环境必须已安装 onelabpro_pyapi SDK，并能连接到实际的
      ONE LabPro 控制器（默认 IP：10.86.88.19）或仿真环境。
    - 本插件本身无需网络连接，完整的 API 知识库已作为本地文件打包在 VSIX 内。

9.3 导入别名支持
    插件自动识别以下两种导入写法：

        import onelabpro_pyapi as pyapi               # 推荐写法
        import onelabpro_pyapi.helpers as olp_helpers  # helper 模块

9.4 已知限制
    - 路径解析在当前打开文件范围内进行，不支持跨文件的别名追踪。
    - 不与 Pylance 冲突——本插件作为增强层叠加在 Pylance 之上，不替代其功能。
================================================================================
