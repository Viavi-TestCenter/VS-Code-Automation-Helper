================================================================================
Viavi TestCenter OTG Snappi Python API VS Code Helper Readme
Version: 1.0.2
Release Date: 2026-10-29
================================================================================

1. Overview
-----------

1.1 Introduction
    Viavi TestCenter OTG Snappi Python API VS Code Helper is an extension
    designed specifically for automation scripting with the snappi Python
    library — the client-side implementation of the Open Traffic Generator
    (OTG) API. By deeply parsing the OTG OpenAPI specification and
    cross-referencing it against the TestCenter implementation, the helper
	lowers the overhead of navigating the deeply nested OTG object hierarchy,
	thereby enhancing script delivery quality and OTG-based protocol
    simulation development efficiency.

1.2 Key Features at a Glance
    - Interactive Template/Example Manager — 49 production-ready snippets,
      one-click insertion via `#` prefix trigger.
    - Dot-Triggered Intelligent Auto-Completion — precise child property
      candidates from a 25,218-node static dictionary.
    - Contextual Variable Type Inference Engine — document-wide variable
      scanning with support for simple and destructuring assignments.
    - Structured Hover Documentation — full OTG path, support status, type,
      default, min/max, and enum values per property.

1.3 Supported Editor Environments
    All support local offline VSIX installation:
    - VS Code             (Microsoft)
    - Trae                (ByteDance)
    - Cursor              (SpaceX)
    - Qoder               (Alibaba)
    - Code Buddy          (Tencent)
    - Devin               (Codeium)


2. Installation Guide (Offline VSIX Method)
-------------------------------------------

2.1 Installation Steps
    All supported VS Code-architecture editors follow identical installation steps:
    1. Open your editor and navigate to the Extensions Panel (`Ctrl+Shift+X`).
    2. Click the More Actions icon (`···`) located at the top-right corner.
    3. Select "Install from VSIX..." from the drop-down menu.
    4. Browse and select the target `.vsix` file, click install, and restart the editor.

2.2 Updating / Uninstalling the Extension
    To update to a newer version or perform a clean reinstall:
    1. Open the Extensions panel (`Ctrl+Shift+X`) and locate OTG Snappi Helper.
    2. Click the gear icon (⚙) → Uninstall, then restart the editor.
    3. Follow steps 1–4 in 2.1 above to install the new `.vsix` file.

    Note: Some editors support installing a new VSIX directly over the existing
    version — the old version is replaced automatically without a manual
    uninstall step.


3. Feature Coverage & Characteristics
--------------------------------------

3.1 High-Frequency Built-in Code Templates/Examples
    Typing `#` followed by a template/example prefix triggers a list of
    matching production-ready code templates/examples. Selecting one replaces
    the `#<prefix>` trigger text with a complete, immediately executable Python
    test script. Each template/example is self-contained — it includes all
    imports, API setup, configuration, traffic control, and result verification
    in a single file, and can be run directly after substituting the chassis IP
    and port location constants at the top.

    Full step-by-step insertion instructions are in section 5.1.

    3.1.1 Available Template/Example Trigger Words (49 total, S001–S049)

        (1) Device & Protocol Emulation Templates/Examples (14), S001–S014:
            - #S001_create_device_ipv4
              Creates two basic emulated IPv4 devices across two ports (Ethernet
              interface + IPv4 interface with gateway); base device-layer template.
            - #S002_create_device_ipv6
              Emulated IPv6 device creation (IPv6 address/gateway/prefix),
              structurally symmetric to the IPv4 version.
            - #S003_create_device_l2
              Pure Layer-2 Ethernet device: configures only the Ethernet interface
              (MAC/MTU) with no Layer-3 address, for switching/forwarding scenarios.
            - #S004_create_device_vlan
              Emulated device with a VLAN sub-interface (vlans under Ethernet:
              name/id/priority/tpid), verifying VLAN encapsulation and forwarding.
            - #S005_create_device_vlan_bound_stream
              Bidirectional bound flows referencing IPv4 interface names between
              two VLAN devices; the VLAN tag is encapsulated with the interface.
            - #S006_create_devices_one_port
              Batch-creates three IPv4 devices on one port plus a gateway device on
              a second port, verifying multi-device port sharing and ARP/forwarding.
            - #S007_create_device_bgp_ipv4_routes
              Two-side eBGP (separate ASNs) base configuration, each advertising a
              route prefix; configuration only (session check: `#S042_get_bgp_state_ipv4`).
            - #S008_create_device_bgp_ipv4_bound_stream
              eBGP session plus two bound flows targeting the advertised BGP route
              objects (tx_rx.device references the route name); configuration only
              (full loop: `#S044_get_bgp_stream_results`).
            - #S009_create_device_bgp_ipv6_routes
              eBGP over IPv6 (BGP+) base configuration, symmetric to the IPv4
              version, advertising IPv6 prefixes (check: `#S043_get_bgp_state_ipv6`).
            - #S010_create_device_ospfv2_lsa
              Two devices each enable an OSPFv2 router, join an area on the
              interface and advertise intra-area routes (Type-1 LSA), verifying
              neighbor establishment and LSA flooding.
            - #S011_create_device_isis_lsp
              Two IS-IS routers configured as point-to-point neighbors and
              generating LSPs; includes protocol configuration and adjacency setup.
            - #S012_config_device_ping_response
              After two IPv4 devices, uses protocol start/stop (START/STOP) to
              express whether the pinged side responds; active ping: `#S047_run_ping`.
            - #S013_create_device_dhcpv4_bound_stream
              One device runs a DHCPv4 server (address pool with start_address/
              count/lease) and the other acts as a DHCPv4 client under its Ethernet
              interface; after the stack starts the client runs the DHCP exchange and
              the learned lease is queried to verify assignment (supported from
              TestCenter v1.55.0).
            - #S014_create_device_rocev2_qp
              One RoCEv2 device per port, each with a peer and a reliable-connection
              (RC) QP (source_qp_number/initial_psn/udp_source_port) on its IPv4
              interface, plus one RoCEv2 stateful flow (config.stateful_flows.rocev2)
              whose endpoint is that QP: once the protocol stack is up, the flow is what
              instantiates the QP and drives the CM handshake, and the per-peer counters
              are polled for qp_up (the QP is created only by the stateful flow;
              protocol.rocev2.peers.state=up is not needed and, if issued before the QP
              exists, leaves the QP stuck in down). Device-level rocev2 is supported from
              TestCenter v1.55.0; requires ports on a RoCEv2-capable card -- the OTG
              model cannot set or query a port's Performance Mode.

        (2) Raw Traffic Templates/Examples (13), S015–S027:
            - #S015_config_raw_stream_ipv4
              The most basic unidirectional port-level raw flow (Ethernet + IPv4)
              with manually set src/dst MAC and IP; configuration only — the base
              raw-flow template in this set.
            - #S016_config_raw_stream_ipv6
              Unidirectional raw flow with the network layer switched to an IPv6
              header and manually specified source/destination IPv6 addresses.
            - #S017_config_raw_stream_udp
              Adds a UDP header on top of the basic flow, forming an
              Eth/IPv4/UDP three-layer header stack.
            - #S018_config_raw_stream_tcp
              Adds a TCP transport header to a unidirectional flow with explicit
              source/destination ports.
            - #S019_config_raw_stream_vlan
              Inserts a VLAN header between Ethernet and IPv4 with vid set,
              verifying tagged Layer-2 encapsulation.
            - #S020_config_raw_stream_bidirectional
              Two antiparallel independent flows between two ports (f1: p1->p2,
              f2: p2->p1), each with its own flow metrics enabled.
            - #S021_config_raw_stream_auto_frame
              Does not set size; the whole-frame length is auto-derived from the
              header stack and payload (auto frame mode).
            - #S022_config_raw_stream_incr_frame
              Frame length increments per packet by step within [start, end]
              (size.increment), traversing the full frame-length range.
            - #S023_config_raw_stream_fixed_frame_ttl
              Fixed-size (size.fixed) unidirectional flow that also explicitly sets
              time_to_live in the IPv4 header.
            - #S024_config_raw_stream_random_frame_constant_fill
              Random frame length (size.random) with the payload constant-filled via
              a custom header.
            - #S025_config_raw_stream_dscp_phb_numeric
              Sets the IPv4 DSCP priority using a raw numeric PHB (phb.value, 0-63).
            - #S026_config_raw_stream_dscp_ecn
              Layers an ECN marking (the low 2 bits of the DS field) on top of the
              symbolic PHB configuration.
            - #S027_config_raw_stream_pfc_pause
              PFC priority flow control back-pressure: a reverse flow sends PFC
              pause frames (class 3, max quanta) to suppress the Tx port while a
              forward flow carries AF11 DSCP with loss metrics enabled;
              configure -> start -> run 12 s -> stop -> query the forward flow's
              Tx/Rx/loss counters.

        (3) Bound Device Traffic Templates/Examples (7), S028–S034:
            - #S028_config_bound_stream_ipv6
              Bidirectional bound flows between two emulated IPv6 devices;
              tx_rx.device references the IPv6 interface name, headers auto-filled.
            - #S029_config_bound_stream_fixed_frame
              Bidirectional bound flow over IPv4 device interfaces (fixed frame
              size); src/dst MAC and IP auto-filled by the emulated interface.
            - #S030_config_bound_stream_auto_frame
              Device-bound bidirectional flow with frame length auto-derived from
              the header stack (auto frame mode).
            - #S031_config_bound_stream_pair_incr_frame
              Device-bound bidirectional flow with frame length incrementing across
              a range (increment mode).
            - #S032_config_bound_stream_bidirectional_random_frame
              Device-bound bidirectional flow with randomly distributed frame length.
            - #S033_config_bound_stream_bidirectional_arp
              Device-bound bidirectional flow plus a protocol-stack start, triggering
              ARP to resolve the peer gateway MAC for L2 reachability; ARP check:
              `#S046_get_device_arp_table`.
            - #S034_config_bound_stream_port_based_rate
              Demonstrates driving transmit rate with Flow.Rate rate.percentage (a
              percentage of the port's maximum line rate) on a unidirectional flow.

        (4) Traffic Control Templates/Examples (3), S035–S037:
            - #S035_start_traffic
              After configuring a unidirectional raw flow, explicitly starts traffic
              via `control_state.traffic.flow_transmit`, demonstrating the
              separation between the Config and Control phases.
            - #S036_stop_traffic
              Full bidirectional lifecycle: configure -> start -> run/wait -> stop,
              for scenarios that actively control transmit duration or assert on an
              intermediate state.
            - #S037_config_link_flap
              Performs a link-down -> link-up flap on the Tx port during continuous
              traffic (using the top-level enum `snappi.StatePortLink`), verifying
              full frame delivery survives the flap window.

        (5) Metrics & Control-Action Templates/Examples (12), S038–S049:
            - #S038_get_stream_results
              Unidirectional flow -> start -> polls flow-level Flow Metrics
              (frames_tx/frames_rx); PASS once Tx==Rx==expected within a 30 s
              window — a complete closed loop.
            - #S039_get_port_results
              Polls port-level Port Metrics (column-trimmed to FRAMES_TX/FRAMES_RX),
              summing both ports, for scenarios that only need port totals.
            - #S040_get_stream_loss_results
              UDP flow with loss metrics enabled (metrics.loss); a single query
              after a fixed wait prints a Tx/Rx/loss counter snapshot.
            - #S041_get_stream_latency_results
              Enables store-forward latency (latency.mode=store_forward) and prints
              average and maximum latency in nanoseconds.
            - #S042_get_bgp_state_ipv4
              eBGP IPv4 peers: after starting the protocol stack, polls
              `bgpv4_metrics.session_state` for UP — the minimal BGP bring-up loop.
            - #S043_get_bgp_state_ipv6
              eBGP+ IPv6 peers: starts the stack and polls `bgpv6_metrics` session
              state, PASSing once both sides report UP.
            - #S044_get_bgp_stream_results
              Full eBGP closed loop: wait for session UP -> start flows bound to the
              advertised BGP routes -> poll flow metrics to verify reachability of
              the target prefix.
            - #S045_get_isis_session_results
              IS-IS point-to-point adjacency: polls `isis_metrics.l2_sessions_up`,
              using an extended 300 s request timeout for slower convergence.
            - #S046_get_device_arp_table
              After starting the stack, queries the IPv4 neighbor table via
              `get_states()` (ipv4_neighbors) and verifies both gateway MACs resolved.
            - #S047_run_ping
              Issues an ICMP ping between two emulated IPv4 devices via
              `set_control_action()` and verifies all responses returned succeeded.
            - #S048_send_bgp_notification
              eBGP IPv4 peers: after the session is UP, actively sends a BGP
              NOTIFICATION (Cease / Administrative Shutdown, subcode=
              `admin_shutdown_code6_subcode2`) via control_action and verifies the
              session transitions down.
            - #S049_run_raw_stream_capture_save
              Enables capture (pcap format) on the Rx port, sends a burst of an IPv4
              UDP raw flow, stops, then fetches the captured bytes via get_capture
              and writes them to a local pcap file for offline analysis (config.
              captures supported from TestCenter v1.55.0).

3.2 Dot-Triggered Intelligent Auto-Completion
    Inside any Python file, typing `.` after any OTG object instantly displays
    precise child property candidates sourced from the internal dictionary:
    - Property Items: Displayed with a Property icon. Each entry shows an
      official OpenAPI description in the detail pane, plus a support badge:
      "Supported (v1.55.0)" for properties implemented in TestCenter, or
      "Not supported" (visually tagged as deprecated) for those that are part
      of the broader OTG specification but not yet available in this TestCenter
      version.
	  
3.3 Contextual Variable Type Inference Engine
    Addressing the weakly-typed nature of the underlying OTG object model, the
    helper applies a document-wide variable scanning engine that resolves short
    alias names to their full OTG type paths, enabling completions on variables
    without requiring explicit type annotations:
    - Simple Assignment Inference: If you write
      `flw = cfg.flows.flow(name='f1')`, then typing `flw.` correctly displays
      completions scoped to the `config.flows.flow` node.
    - Destructuring Assignment Inference: If you write
      `eth, ip, udp = flw.packet.ethernet().ipv4().udp()`, each variable is
      independently mapped to its correct header type. Typing `ip.` shows only
      IPv4 header fields; `udp.` shows only UDP header fields.
    The engine rescans the full document on every edit, ensuring inferred types
    remain accurate as the script evolves.

3.4 Structured Hover Documentation (Hover Provider)
    Hovering over any OTG property token in the editor opens a Markdown card
    assembled directly from the internal dictionary. Each card shows:
    - OTG Path: The full dotted canonical key
      (e.g., `config.flows.packet.ipv4.src`).
    - Support Status: "Supported (v1.55.0)" or "Not supported".
    - Description: The official OpenAPI description, cleaned of residual markup.
    - Type & Format: Data type (e.g., `string`, `integer`) and format
      constraint (e.g., `mac`, `ipv4`) where applicable.
    - Default Value: The schema-defined default, if one exists.
    - Min / Max: Numeric bounds for integer and number properties.
    - Enum Values: The complete list of valid enumeration choices for string
      properties with a fixed set (e.g., `choice` properties).
    Hover also activates within keyword argument contexts — hovering the
    parameter name inside a factory method call (e.g., `address` inside
    `ipv4(address="10.0.0.1", ...)`) shows the description for that specific
    parameter without requiring you to leave the cursor position.


4. OTG Object & Results Coverage
----------------------------------
The internal dictionary fully covers the following OTG namespaces:

- config:          The complete OTG Config object tree (ports, flows, devices,
                   lags, layer1, captures, lldp, options), including all packet
                   header stacks (Ethernet, IPv4, IPv6, TCP, UDP, VLAN, MPLS,
                   GRE, ICMPv4, ICMPv6, ARP, PFC Pause, Custom) and their full
                   field hierarchies (fixed value, increment, decrement, random,
                   value_list, metric_tags).
- api:             Top-level API method nodes (set_config, get_config,
                   get_metrics, get_states, get_capture, set_control_state,
                   set_control_action, etc.).
- config_update:   The ConfigUpdate / incremental update object tree.
- metrics_request: MetricsRequest and all sub-objects (flow, port, bgpv4,
                   bgpv6, isis, lacp, lldp, rsvp, etc.) with choice enums.
- states_request:  StatesRequest and all sub-objects (bgpv4_peers, isis_lsps,
                   dhcpv4_clients, etc.) with choice enums.
- control_state:   ControlState object (flow transmit, port link, protocol
                   start/stop) with full enum lists.
- control_action:  ControlAction object.
- capture_request: CaptureRequest object.
- snappi:          The top-level snappi Python module path nodes.

Support Status Breakdown:
- TestCenter v1.55.0 Supported:     13,249 properties
- OTG Spec Only (Not yet in TC):   11,969 properties


5. Template/Example Usage & Code Example
-----------------------------------------

5.1 Inserting a Template/Example
    Type `#` followed by a template/example trigger word in any `.py` file. The
    editor immediately shows the matching templates/examples as a completion
    list; continue typing to narrow it, then press `Enter` or `Tab` to insert.
    A trigger word is exactly the name listed in section 3.1.1, e.g.
    `S001_create_device_ipv4` -- the leading `S001`–`S049` is the scenario
    serial, matching the ID column of the Summary of Plugin Examples workbook
    and the numbering used in the roadmap and in issue references.
    The `#<trigger>` text is automatically replaced by the full, runnable code
    snippet.

    5.1.1 Placeholder Constants
        Each template/example exposes three constants at the top of the script
        that you substitute before running:
        1. API  — OTG server endpoint address (e.g. "0.0.0.0:50051")
        2. PTX  — Tx port chassis location (e.g. "//10.126.32.98/4/5")
        3. PRX  — Rx port chassis location (e.g. "//10.126.32.98/4/6")

    5.1.2 Choosing the Right Template/Example
        - Use `#S015_config_raw_stream_ipv4` (configuration only) or
          `#S038_get_stream_results` (with a flow-metrics PASS/FAIL closed loop) for
          basic unidirectional raw traffic.
        - Use `#S039_get_port_results` when you only need port-level Tx/Rx totals
          rather than per-flow breakdowns.
        - Use `#S001_create_device_ipv4` followed by `#S029_config_bound_stream_fixed_frame`
          when flows must be bound to emulated device interfaces rather than raw
          ports.
        - Use `#S044_get_bgp_stream_results` when the test requires BGP session bring-up
          before sending traffic — the template/example includes the BGP
          session UP polling loop automatically.
        - Use `#S041_get_stream_latency_results` when store-forward latency measurement
          is required — the template/example enables `metrics.latency` and prints
          average and maximum latency in nanoseconds alongside the frame counters.
        - Use `#S047_run_ping` to verify Layer-3 reachability between two emulated
          devices before committing to a full traffic test.

5.2 Basic Code Workflow
    A typical script-authoring flow after inserting the `#S038_get_stream_results`
    template/example:

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

    # After insertion, the variable inference engine recognizes all bindings:
    # - `flw` is inferred as config.flows.flow — typing `flw.` opens completions
    #   scoped to flow properties (size, rate, duration, metrics, packet, etc.).
    # - `eth`, `ip`, `udp` are each inferred from the destructuring assignment.
    #   Typing `ip.` shows only IPv4 header fields; `udp.` shows only UDP fields.
    #
    # Example: to add DSCP marking, type `ip.priority.` → select `choice`,
    # then type `ip.priority.dscp.` → navigate to `phb.` for the PHB field.

5.3 Using Hover to Check Property Details
    Before modifying an unfamiliar property, hover the mouse over it to open
    the documentation card. For example, hovering over `flw.metrics.enable`
    displays:
    - OTG Path:   config.flows.flow.metrics.enable
    - Status:     Supported (v1.55.0)
    - Type:       boolean
    - Default:    false
    - Description: Enables flow metrics collection for this flow.

6. Support, Enhancements & Continuous Roadmap
---------------------------------------------

6.1 Continuous Updates & Evolution
    The helper is under ongoing maintenance. Future releases will update the
    knowledge base dictionary to align with new TestCenter software versions
    and new OTG specification revisions, and extend the built-in
    template/example library to cover a broader range of complex testing
    workflows, including additional emulated device and protocol session
    scenarios.

6.2 Technical Support & Feedback Contact
    Your feedback is vital to improving the helper. If you encounter any bugs,
    require technical assistance, or wish to suggest features/enhancements,
    please reach out to our support desk:

    - Support Email: HSESupportBJ@viavisolutions.com

    Please feel free to contact us regarding:
    - Bug Reports & Troubleshooting: Completion, hover, or inference issues.
    - Feature Requests & Enhancements: Structural additions or improvements.
    - New Templates, Examples and Protocol Requirements: Desired test workflows 
	or templates/examples to be supported in subsequent releases.


7. Important Notes & Environment Prerequisites
----------------------------------------------

7.1 Lazy Activation Mechanism
    To maintain a lightweight environment, the helper uses a lazy-loading
    architecture. It activates and loads the full 25,218-node dictionary only
    when an actual Python file ending in `.py` is opened, ensuring zero idle
    memory consumption during regular coding sessions in other languages.

7.2 Prerequisites
    - The helper functions strictly as a front-end syntax assistant. To execute
      the generated scripts, the local or remote environment must have the
      snappi Python package installed (`pip install snappi`) and network
      connectivity to a running TestCenter OTG server endpoint.
    - No internet connection is required for the helper itself; the entire OTG
      knowledge base is bundled locally inside the VSIX package.
