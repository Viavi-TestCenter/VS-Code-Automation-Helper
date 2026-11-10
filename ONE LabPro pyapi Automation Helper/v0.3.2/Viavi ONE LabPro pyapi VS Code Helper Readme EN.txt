================================================================================
Viavi ONE LabPro API VS Code Helper — User Guide
Version:  0.3.2
Released: 2026-10-30
================================================================================

1. Overview
-----------

1.1 Introduction
    The Viavi ONE LabPro API VS Code Helper is an intelligent code-assistance
    extension purpose-built for test engineers who write automation scripts with
    the Viavi ONE LabPro Python object-tree API (onelabpro_pyapi, SDK 5.0.0).
    The extension covers 3,788 API nodes and provides full path-aware completion,
    hover documentation, and signature help — so engineers can write accurate
    ONE LabPro pyapi test scripts without consulting the API reference manually.

1.2 Feature Summary
    - Path-aware completion — typing `.` after an object chain pops up the child
      node list for that exact level. Variable aliases are tracked end-to-end
      (`sc = ctrl.Scenarios[id]`, `pf = getattr(port, PROFILE)`, etc.) so
      completions are based on the real API path, not fuzzy name matching.
    - Child-node completion — collection nodes (Scenarios / Ports …) are
      automatically pierced through item_child, so typing `.` after them shows
      the usable children directly (add / list / close / L0 / L1 / L2 …).
    - Helper completion — typing `olp_helpers.` pops all 11 helper functions.
    - Hover docs — hovering over any node name shows a structured card:
      description, API path, child-node list, and parameter details.
    - Signature help — typing `(` shows the live parameter signature with the
      current argument highlighted.
    - Snippets — 49 complete test scripts + 92 function-call fragments.
      Type `#` in any .py file to bring up the complete script list, or `##`
      to bring up the function-snippet list. Select and press Enter to expand,
      then Tab through placeholders.
    - Import alias detection — the extension scans the current file and
      recognises both `import onelabpro_pyapi as <alias>` and
      `import onelabpro_pyapi.helpers as <alias>`.

1.3 Supported Editor Environments
    Any VS Code-architecture editor supports local offline VSIX installation:
    - VS Code              (Microsoft — requires version 1.93.0 or later)
    - Trae                 (ByteDance)
    - Cursor               (Anysphere)
    - Qoder                (Alibaba)
    - Code Buddy           (Tencent)


2. Installation (Offline VSIX)
------------------------------

2.1 Installation Steps
    The procedure is identical across all VS Code-based editors:
    1. Open the editor and go to the Extensions panel (Ctrl+Shift+X).
    2. Click the "More Actions" icon (···) in the top-right corner.
    3. Choose "Install from VSIX..." from the dropdown.
    4. Browse to the target .vsix file, click Install, then restart the editor.

    Command-line installation (VS Code):
        code --install-extension onelabpro-pyapi-helper-en-0.3.2.vsix

    Chinese-UI build:
        code --install-extension onelabpro-pyapi-helper-0.3.2.vsix

2.2 Updating / Uninstalling
    To upgrade to a newer release or perform a clean reinstall:
    1. Open the Extensions panel (Ctrl+Shift+X), find Viavi ONE LabPro
       API VS Code Helper.
    2. Click the gear icon (⚙) → Uninstall, then restart the editor.
    3. Follow steps 1–4 in section 2.1 to install the new .vsix file.

    Note: some editors support installing a new VSIX directly on top of an
    existing version — the old release is replaced automatically with no manual
    uninstall required.


3. Features and Capabilities
-----------------------------

3.1 Path-Aware Completion
    Typing `.` after an object chain immediately shows the child nodes available
    at that exact level, each with its node type and a short description.

    Completion examples:
        ctrl.Scenarios.        → add / list / close / save / closeIdle / Saved
        ctrl.Assets.Modules.   → list
        sc.Ports.              → add / list / clone / remove / Profiles / Filters
        port.L1.Pcs.Fec.       → Alarms / Errors / set / states
        olp_helpers.           → checkLinkUp / checkTransceiverReady + 9 more

    Full alias tracking chain:
        ctrl = pyapi.Controller(host, ...)        # ctrl → API root
        sc   = ctrl.Scenarios[sc_data['id']]      # sc  → Scenarios
        port = sc.Ports[port_data['id']]          # port → Ports[id]
        pf   = getattr(port, PROFILE)             # pf  → profile node
        for port in (port_w, port_e):             # loop variables tracked
            pf = getattr(port, PROFILE)
            pf.L0.Unframed.Pattern.set(...)       # resolves to L0.Unframed.Pattern.set

3.2 Hover Documentation
    Hovering over any pyapi node or helper function shows a structured card:

        Hover target                     Content shown
        --------------------------       ------------------------------------------
        ctrl.Scenarios                   Description, API path, methods, child list
        sc.Ports.add                     Method signature, parameter names and types
        port.L1.Pcs.Fec                  Path, children (Alarms/Errors/set/states)
        olp_helpers.checkLinkUp          Signature, parameter descriptions

    Path-awareness example:
        sc = ctrl.Scenarios[id] → hovering `add` on `sc.Ports.add(…)`
        shows Ports.add docs, not Scenarios.add.

3.3 Signature Help
    When you type `(` after a method name, a live parameter signature appears
    with the current cursor argument highlighted:

        ctrl.Scenarios.add(focus=..., name=..., ...)
                           ^^^^^
                           # active parameter shifts as the cursor moves

        sc.Ports.add(profile=..., count=..., name=..., orientation=..., ...)
        olp_helpers.checkLinkUp(*ports, count=..., interval=..., timeout=...)

3.4 Snippets
    49 complete test scripts and 92 function-call fragments are included,
    activated automatically in .py files.

    Trigger:
        #   → shows the complete script list (49 items) with param blocks,
              try/finally cleanup, and assertions
        ##  → shows the function-snippet list (92 items), single API calls
              insertable directly into existing scripts

    After typing # or ##, continue typing keywords to filter the list.
    Press Enter to expand, then Tab / Shift+Tab to navigate placeholders.
    The full snippet list is in section 5.


4. API Coverage (SDK 5.0.0)
----------------------------
The extension's embedded metadata provides complete coverage of:

    Category                          Detail
    --------------------------------  ------------------------------------------
    Total pyapi metadata nodes        3,788 nodes (extracted from nodes.py)
    Top-level namespace nodes         8 (Scenarios / Assets / Licensing …)
    Max tree depth under Scenarios    6 levels (ctrl → Scenarios → [id] →
                                      Ports → [id] → L1 → Pcs → Fec)
    Helper functions                  11
    Complete test scripts             49
    Function-call snippets            92


5. Snippet Usage and Code Examples
------------------------------------

5.1 Using Snippets
    In any .py file, type `#` (complete scripts) or `##` (function snippets).
    The editor automatically shows a matching list. Continue typing to filter;
    press Enter to expand the selection, then Tab through each placeholder.

5.2 Complete Test Scripts (49)
    Each script includes: a top parameter block (Tab through to fill
    Controller IP, ports, etc.), try/finally error handling,
    logging.info output, and result assertions.

    (1) Getting Started / Environment Verification
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP001_probe_hardware                   Probe controller: list modules and free hardware ports
        OLP002_run_getting_started              Hello World: connect → list modules/profiles/scenarios → close
        OLP003_verify_installation              Verify onelabpro_pyapi install: import, olp_helpers, Controller class

    (2) Assets / Hardware Inventory
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP004_query_assets                     Query modules, ports, licenses
        OLP005_inventory_hardware               Full hardware inventory: modules/ports/transceivers/licenses/free ports
        OLP006_discover_profiles                Discover all available profiles with line rate, medium, free port count

    (3) Scenario Management
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP007_manage_scenario_basic            Scenario lifecycle: create → save → list → load → close
        OLP008_run_scenario_full_lifecycle      Full lifecycle: create → add ports → run → save → list → close
        OLP009_manage_saved_scenarios           List saved scenarios, load by name, re-run, optionally delete old
        OLP010_cleanup_idle_scenarios           Audit running + saved scenarios, close idle — dry-run safe
        OLP011_scenario_load_saved_active       Save + reload flow (Saved.list + Saved.load(...)); load active by name

    (4) Port Mapping
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP012_run_container_pattern            Container wrapper pattern with auto-cleanup
        OLP013_map_free_ports_auto              Auto-discover free hardware ports for a profile, add and map
        OLP014_discover_and_map_ports           Auto-discover free HW ports, map to scenario ports, run L2L3 traffic
        OLP015_switch_port_focus                PHY then L2L3 on same HW port: validates focus switching without reboot

    (5) L2/L3 Traffic
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP016_run_l2l3_traffic                 Basic bidirectional L2L3 RAW traffic with TfgClusters (2 ports)
        OLP017_verify_l2l3_flow_loss            L2L3 RAW bidirectional + assert every flow has zero packet loss
        OLP018_run_l2l3_multi_framesize         Sequential multi-frame-size L2L3: 64/512/1518 bytes, each run separate
        OLP019_get_l2l3_port_stats_detail       L2L3 RAW + per-port stats: L0 frequency, L1 PCS, L2 FrameLayer
        OLP020_poll_l2l3_continuous             Long-running L2L3 RAW traffic with periodic RxFlows polling
        OLP021_run_l2l3_port_orientation        L2L3 RAW bidirectional with orientation=west/east — verifies port.get()
        OLP022_run_l2l3_repeated_measurements   Repeated start/stop measurement rounds — validates run consistency
        OLP023_inject_l2l3_fec_error            L2L3 RAW traffic + FEC error injection: baseline vs. error comparison
        OLP024_raw_traffic_vlan_udp             L2L3 RAW VLAN/Ipv4/Udp A→B (Layers.add pattern) — zero-loss assertion
        OLP025_send_custom_payload              RAW traffic + ViaviTfl CUSTOM_REPEAT custom payload pattern
        OLP026_traffic_vlan_tcp                 L2L3 DevClusters Ipv4 + TCP layer bidirectional (Layers.add Tcp)

    (6) PHY / PRBS Tests
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP027_run_phy_prbs                     PHY PRBS BER test: PRBS31Q/SSPRQ/PRBS9/PRBS13Q, PCS + FEC stats
        OLP028_run_phy_prbs_multi_pattern       PHY sequential multi-pattern: each pattern reads PCS + FEC stats
        OLP029_switch_phy_fec_mode              FEC mode cycle: NONE/RS/FC — verify reconciliation after each switch
        OLP030_check_phy_alignment_skew         PHY alignment skew + lane mapping + per-lane PCS status readout
        OLP031_monitor_phy_host_freq            L0 host-interface Tx/Rx frequency polling (N iterations, dual port)
        OLP032_get_phy_xcvr_details             Transceiver state + RxMapped + host frequency + FrameLayer (both ports)
        OLP033_check_phy_per_lane               PHY per-lane PCS status + lane mapping (100G/400G multi-lane)
        OLP034_run_phy_prbs_ssprq               SSPRQ basic PHY test: PCS reconciliation + FEC alarm/error readout
        OLP035_enable_an_lt                     PHY AN (AutoNegotiation) + LT (LinkTraining) configuration
        OLP036_i2c_readwrite                    ONE-1600 PHY I2C Dump/Peek/Poke via HwPorts[id].L0.Transceiver.I2C

    (7) FEC / Alarm / Port Health
        Prefix                                   Description
        -------------------------                ----------------------------------------
        OLP037_inject_fec_error                 FEC error injection: inject, read FEC alarms/errors, stop
        OLP038_monitor_port_summary             Continuous port health monitoring with alarm event log
        OLP039_poll_fec_alarm                   Periodic FEC alarm + PCS reconciliation polling loop
        OLP040_monitor_xcvr_power               Transceiver (L0) state and Rx-mapped stats periodic polling
        OLP041_inject_fec_error_rounds          N-round FEC injection with alarm/error count per round
        OLP042_detect_pcs_fault                 Inject FEC errors west, verify alarms east, stop and verify clear
        OLP043_detect_link_flap                 Monitor link state to detect flaps — logs each flap event
        OLP044_health_check_debug               Controller health stats + Debug Dump download URL
        OLP045_stats_frame_pcs_fec              PHY port Frame/PCS/FEC/Reconciliation/B64B66 stats + FEC mode set
        OLP046_rx_service_disruption            PHY Rx service disruption sensor + FEC_UNCORR injection
        OLP047_alarms_errors_insertion          Full alarm+error suite: AlarmFec/AlarmReconciliation/ErrorFec/ErrorFrame/ErrorTranscoding
        OLP048_fec_validation                   RAW A→B + 4-type FEC validation: ErrorFec/AlarmFec/AlarmReconciliation/ErrorTranscoding
        OLP049_transceiver_health_config        HSE800 PHY transceiver health: MsaInfo/Health/OpticalPower/Control per port

5.3 Function-Call Snippets (92)
    Minimal single-operation fragments for insertion into existing scripts.

    (1) Connection (connect.json — 3)
        Prefix                     Description
        -------------------------  ----------------------------------------
        connect                    Connect to controller with user/password
        connect_token              Connect with JWT token
        connect_context            Connect via `with` context manager
                                   (auto-cleanup)

    (2) Scenario Management (scenarios.json — 6)
        Prefix                     Description
        -------------------------  ----------------------------------------
        scenario_create            Create a scenario (L2L3 / PHY focus)
        scenario_list              List all running scenarios (id/name/focus)
        scenario_save              Save current scenario to a named archive
        scenario_load              Load a saved scenario by name
        scenario_close             Close a running scenario
        scenario_container         Container-encapsulated mode (auto remove)

    (3) Port Operations (ports.json — 12)
        Prefix                     Description
        -------------------------  ----------------------------------------
        port_add                   Add a port (profile enum selection)
        port_list_profiles         List all mappable profiles
        port_map_single            Map a single port to hardware (module/hw)
        port_map_multi             Batch-map multiple ports (mapPortsById)
        port_check_link            Block until link is UP (checkLinkUp)
        port_check_transceiver     Wait for transceiver to reach ModuleReady
        port_get_link_state        Non-blocking read of link state
        port_summary               Read L0/L1/L2 summary state (getPortSummary)
        port_summary_ok            Assert all port layers OK (no alarms)
        port_set                   Set port name / description
        port_states                Read port L1/L2 state flags
        port_free_mappings         Query free hardware ports for a profile

    (4) L1 / L0 / L2 (l1_l2.json — 17)
        Prefix                     Description
        -------------------------  ----------------------------------------
        l1_pcs_states              Read PCS reconciliation state + FEC
                                   alarms + FEC errors
        l1_pcs_fec_set             Set FEC mode (NONE / RS / FC)
        l1_alignment_skew          Read PCS alignment skew and lane mapping
        l1_pcs_lanes               Read per-lane PCS state
        l1_unframed_prbs           Configure unframed PRBS Tx/Rx pattern
        l0_transceiver_stats       Read L0 transceiver state and detect type
        l0_host_interface          Read L0 host Tx/Rx frequency
        l2_frame_layer             Read L2 FrameLayer frame counts and errors
        error_fec_inject           FEC error injection start/stop
        payload_custom_fixed       CUSTOM_FIXED payload (fixed hex)
        payload_increment          INCREMENT_BYTE payload (incrementing hex)
        rxflows_verify             Per-flow TX/RX equality assertion (zero loss)
        measurement_run            start / sleep / stop + read RxFlows
        l1_fec_hser_inject         Continuous FEC HSER inject + read alarms/
                                   errors
        l1_xcvr_power_read         L0 transceiver state + RxMapped read
        l1_pcs_summary             PCS reconciliation + FEC alarms + errors in
                                   one shot
        l1_port_summary_detail     getPortSummary per-layer alarm extraction

    (5) Helper Utilities (helpers.json — 9)
        Prefix                     Description
        -------------------------  ----------------------------------------
        helpers_checkLinkUp        Block until link is UP
        helpers_checkTransceiverReady Wait until transceiver is ready
        helpers_getLinkState       Non-blocking link state (dict)
        helpers_mapPortToHardware  Map a single port to hardware
        helpers_mapPortsById       Batch-map multiple ports
        helpers_getPortSummary     Retrieve L0/L1/L2 port summary
        helpers_checkPortSummaryAllOk Assert all ports have no alarms
        helpers_payload_fixed      CUSTOM_FIXED payload dict
        helpers_payload_increment  INCREMENT_BYTE payload dict

    (6) Advanced (advanced_pyapi.json — 45)

        Traffic / TFG (8)
        Prefix                     Description
        -------------------------  ----------------------------------------
        scenario_close_idle        Close idle/timed-out scenarios (dry-run
                                   safe)
        helpers_payload_repeat     CUSTOM_REPEAT payload dict
        helpers_payload_decrement  DECREMENT_BYTE payload dict
        allflows_list              List AllFlows, per-flow TX/RX stats
        alltfgs_list               List all TFGs in a scenario (id/name/state)
        tfgcontrol_start           TfgControl.start() — start all TFGs
        tfgcontrol_stop            TfgControl.stop() — stop all TFGs
        rxflow_rate_calc           Two-snapshot delta to compute live Rx rate

        Advanced Port Operations (9)
        Prefix                     Description
        -------------------------  ----------------------------------------
        port_states_l1l2           port.states(L1Summary, L2Summary)
        port_get_details           Retrieve full port config (name/orientation/
                                   profile)
        port_clone                 Clone a port
        port_remove                Remove a port
        port_set_orientation       Set port east/west orientation
        port_count_add             Add multiple ports in one add() call (count)
        port_filters_list          List port filters in a scenario
        port_profiles_list         List all mappable profiles (line-rate/free)
        port_map_single_auto       Map port + wait for transceiver ready

        Advanced Scenario Management (7)
        Prefix                     Description
        -------------------------  ----------------------------------------
        scenario_saved_list        List saved scenarios (name/savedAt)
        scenario_saved_remove      Delete a saved scenario by name
        scenario_close_by_name     Close a running scenario by name
        scenario_list_running      List all currently running scenarios
        scenario_create_phy        Create a PHY scenario
        hw_ports_list              List hardware ports allocated in a scenario
        mappings_list              List port-to-hardware mappings in a scenario

        Advanced L1 PHY Operations (9)
        Prefix                     Description
        -------------------------  ----------------------------------------
        l1_pcs_alignment_read      Read PCS alignment skew + lane mapping
        l1_fec_mode_rs             Set FEC to RS (Reed-Solomon)
        l1_fec_mode_none           Disable FEC (NONE)
        l1_fec_mode_fc             Set FEC to FC (FireCode)
        l1_host_freq_both          L0 host Tx + Rx frequency in one read
        l1_unframed_ssprq          Configure SSPRQ unframed pattern
                                   (IEEE 100G/400G)
        l1_unframed_prbs31q        Configure PRBS31Q unframed pattern
        pcs_reconciliation_check   Dual-port PCS reconciliation state read
                                   and log
        fec_errors_check           Dual-port FEC alarms + error count read

        Advanced L0 / L2 / Utilities (3)
        Prefix                     Description
        -------------------------  ----------------------------------------
        l0_xcvr_full_details       Full transceiver details (state/detect/
                                   vendor/PN/RxMapped)
        l2_framelayer_full         L2 FrameLayer frame counts and errors
        error_fec_stop             Stop FEC error injection

        Hardware / Asset Queries (2)
        Prefix                     Description
        -------------------------  ----------------------------------------
        assets_modules_list        Module list (port count/firmware/free ports)
        licensing_list             License list (type/state/expiry)

        Advanced Helpers / Connection (7)
        Prefix                     Description
        -------------------------  ----------------------------------------
        helpers_get_link_state     getLinkState per-port state dict
        helpers_map_ports_by_id    mapPortsById batch mapping
        helpers_check_port_ok      checkPortSummaryAllOk + alarm assertion
        connect_no_verify          Connect with TLS verification disabled
                                   (self-signed certs)
        helpers_retry_connect      Auto-retry on connection failure (N times,
                                   with delay)
        modules_free_ports         Enumerate all modules and collect free
                                   ports
        port_summary_all           Read alarm summary for all ports in a
                                   scenario

5.4 Typical Script Skeleton
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

    # 1. Connect
    ctrl = pyapi.Controller(CTRL_HOST, auth_credentials=('admin', 'Admin123'))
    ctrl._session.trust_env = False

    # 2. Create scenario
    sc_data = ctrl.Scenarios.add(focus='L2L3', name='my-test')
    sc = ctrl.Scenarios[sc_data['id']]

    try:
        # 3. Add and map ports to hardware
        pw_data = sc.Ports.add(profile=PROFILE)
        pe_data = sc.Ports.add(profile=PROFILE)
        port_w  = sc.Ports[pw_data['id']]
        port_e  = sc.Ports[pe_data['id']]
        olp_helpers.mapPortsById({port_w: f'{MODULE_W}/{HW_PORT_W}',
                                   port_e: f'{MODULE_E}/{HW_PORT_E}'})

        # 4. Wait for links to come up
        olp_helpers.checkLinkUp(port_w, port_e, timeout=60)
        logging.info('Links up')

        # 5. Run traffic
        sc.Measurement.start()
        time.sleep(DURATION)
        sc.Measurement.stop()

        # 6. Read statistics
        flows    = sc.RxFlows.list()
        total_tx = sum(f.get('txFrameCount', 0) for f in flows)
        total_rx = sum(f.get('rxFrameCount', 0) for f in flows)
        logging.info(f'tx={total_tx:,}  rx={total_rx:,}  lost={total_tx-total_rx}')
        assert total_tx == total_rx, 'Frame loss detected'

        # 7. Read L1 state
        rec = port_w.L1.Pcs.Reconciliation.states()
        fec = port_w.L1.Pcs.Fec.Alarms.states()
        logging.info(f'PCS={rec}  FEC alarms={fec}')

    finally:
        # 8. Close scenario
        ctrl.Scenarios.close(id=sc_data['id'])
        logging.info('Done.')

    While writing:
    - Type `ctrl.` to trigger top-level node completion (Scenarios/Assets/…).
    - Type `sc.Ports.` to trigger port child-node completion (add/list/clone/…).
    - Type `port.L1.Pcs.Fec.` to trigger Fec sub-node completion.
    - Type a method's opening `(` (e.g. `sc.Ports.add(`) to trigger signature help.
    - Hover over any node name to view the path-aware documentation card.


6. Helper Function Reference
-----------------------------

    Function                                  Description
    ----------------------------------------  ----------------------------------
    checkLinkUp(*ports, count, interval,      Block until all ports report
        timeout)                              link UP
    checkTransceiverReady(*ports, timeout)    Wait until transceivers reach
                                              ModuleReady state
    getLinkState(*ports)                      Non-blocking link state read
                                              (dict: id → 0/1)
    mapPortToHardware(port, module_id,        Map a single scenario port to
        hw_port_id)                           a hardware port
    mapPortsById(mappings)                    Batch-map multiple ports
                                              (dict: port → 'module/hw')
    getPortSummary(*ports)                    Aggregate L0/L1/L2 port summary
    checkPortSummaryAllOk(*ports)             Assert all port layers are OK
                                              (no alarms)
    configurePayloadCustomFixedHex(hex)       Build a CUSTOM_FIXED payload dict
    configurePayloadCustomRepeatHex(hex)      Build a CUSTOM_REPEAT payload dict
    configurePayloadIncrementByteHex(base)    Build an INCREMENT_BYTE payload
                                              dict
    configurePayloadDecrementByteHex(base)    Build a DECREMENT_BYTE payload
                                              dict


7. Keyboard Shortcuts
---------------------

    Action                                   Shortcut
    ---------------------------------------  -----------------------------------
    Trigger signature help (show params)     Type (
    Trigger enum values / child-node list    Type . or Ctrl+Space
    View hover documentation                 Hover mouse / Ctrl+I
    Manually trigger completion              Ctrl+Space
    Jump to next placeholder after expand    Tab
    Jump to previous placeholder             Shift+Tab
    Exit snippet mode (at final $0 stop)     Tab or Escape


8. Support, Enhancements, and Updates
--------------------------------------

8.1 Ongoing Development
    This extension is actively maintained. Future releases will continue to
    refine API node coverage and parameter metadata, and will add further
    scenario-focused code snippets to cover a wider range of pyapi test
    workflows.

8.2 Technical Support and Feedback
    Your feedback is essential for improving this extension. If you encounter
    any defects, need technical assistance, or want to suggest new features,
    please contact our support team:

    - Support email: HSESupportBJ@viavisolutions.com

    We welcome contact on any of the following:
    - Bug reports (incorrect completion, hover, or signature-help behavior).
    - Feature requests (additional node/parameter coverage or snippet templates).
    - Test-script requests (workflows you would like supported in a future
      release).


9. Important Notes and Prerequisites
--------------------------------------

9.1 Activation Mechanism
    The extension uses on-language activation (onLanguage:python) — it activates
    only when a .py file is opened, ensuring zero overhead when you are working
    in other languages.

9.2 Prerequisites
    - Any of: VS Code / Trae / Cursor / Qoder / Code Buddy (VS Code requires
      version 1.93.0 or later).
    - The extension runs strictly as a front-end syntax-assistance layer. To
      actually execute the generated test scripts, the local or remote Python
      environment must have the onelabpro_pyapi SDK installed and must be able
      to reach a live ONE LabPro controller (default IP: 10.86.88.19) or a
      simulation environment.
    - The extension itself requires no network connectivity. The full API
      knowledge base is bundled as a local file inside the VSIX package.

9.3 Import Alias Support
    The extension automatically recognises both import forms:

        import onelabpro_pyapi as pyapi               # recommended
        import onelabpro_pyapi.helpers as olp_helpers  # helper module

9.4 Known Limitations
    - Alias resolution is scoped to the currently open file; cross-file
      alias tracking is not supported.
    - The extension does not conflict with Pylance — it layers on top of
      Pylance's own intelligence without replacing it.
================================================================================
