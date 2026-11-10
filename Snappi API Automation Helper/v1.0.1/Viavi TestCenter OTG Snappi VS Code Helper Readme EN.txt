================================================================================
Viavi TestCenter OTG Snappi Python API VS Code Helper — User Guide
Version: 1.0.1
Release Date: 2026-08-17
================================================================================

1. Overview
-----------

1.1 Introduction
    Viavi TestCenter OTG Snappi Python API VS Code Helper is an extension
    designed for writing automation scripts using the snappi Python library.
    snappi is the client-side implementation of the Open Traffic Generator
    (OTG) API. By deeply parsing the OTG OpenAPI specification and
    cross-referencing it against the TestCenter implementation, this extension
    reduces the overhead of navigating deeply nested OTG object hierarchies,
    improving script delivery quality and OTG-based protocol simulation
    development efficiency.

1.2 Feature Overview
    - Interactive code snippet manager — 30 ready-to-use code snippets,
      triggered by a `#` prefix and inserted with a single selection.
    - Dot-triggered intelligent auto-completion — powered by a 21,323-node
      static dictionary, surfacing precise sub-property candidates.
    - Contextual variable type inference engine — full-document variable
      scanning supporting simple and destructuring assignment inference.
    - Structured hover documentation — each property displays its full OTG
      path, support status, type, default value, min/max, and enum values.

1.3 Supported Editor Environments
    All editors below support local offline VSIX installation:
    - VS Code             (Microsoft)
    - Trae                (ByteDance)
    - Cursor              (SpaceX)
    - Qoder               (Alibaba)
    - Code Buddy          (Tencent)
    - Devin               (Codeium)


2. Installation Guide (Offline VSIX)
-------------------------------------

2.1 Installation Steps
    The procedure is the same for all VS Code-based editors:
    1. Open the editor and go to the Extensions panel (Ctrl+Shift+X).
    2. Click the More Actions icon (···) in the top-right corner.
    3. Select "Install from VSIX..." from the dropdown menu.
    4. Browse to the target .vsix file, click Install, then restart the editor.

2.2 Updating / Uninstalling
    To upgrade to a newer version or perform a clean reinstall:
    1. Open the Extensions panel (Ctrl+Shift+X) and locate OTG Snappi Helper.
    2. Click the gear icon (⚙) → Uninstall, then restart the editor.
    3. Follow steps 1–4 in section 2.1 to install the new .vsix file.

    Note: Some editors allow installing a new VSIX directly over an existing
    version — the old version is replaced automatically without manual
    uninstallation.


3. Features and Coverage
------------------------

3.1 Built-in Code Snippets
    In any .py file, type # followed by a snippet prefix to trigger a filtered
    completion list of matching snippets. Selecting an entry replaces the
    #<prefix> trigger text with a complete, immediately runnable Python test
    script. Every snippet is self-contained — it includes all imports, API
    initialization, configuration, traffic control, and result verification.
    Only the chassis IP and port location constants at the top of the script
    need to be updated before running.

    See section 5.1 for step-by-step insertion instructions.

    Snippet Prefix Naming Convention:
        - config_*      Configuration only, no traffic started
        - get_*         Config + start + poll + PASS/FAIL verify (full loop)
        - start_* / stop_*  Fine-grained traffic lifecycle control
        - run_* / send_*    One-shot actions (ping, BGP message, etc.)

    3.1.1 Available Snippet Prefixes (30 total)

        (1) Raw Port Flow Snippets (5):
            - #config_flow
              Basic unidirectional Raw flow (Ethernet + IPv4).
            - #config_udp_flow
              Unidirectional Raw flow (Ethernet + IPv4 + UDP).
            - #config_bidirflow
              Two opposing port-level Raw flows (bidirectional traffic).
            - #config_flow_rate_percentage
              Unidirectional Raw flow with rate controlled via
              `rate.percentage`.
            - #config_link_flap
              Port link down/up flap (Link Flap) test.

        (2) Traffic Control & Metrics Snippets (9):
            - #start_flow_by_control
              Configure unidirectional Raw flow and start via Control State.
            - #start_bidirflow_by_snappi
              Bidirectional flow + start (snappi enum-style Control State).
            - #stop_bidirflow
              Bidirectional flow full lifecycle (config → start → wait →
              stop).
            - #get_flow_metrics
              Unidirectional flow → start → poll Flow Metrics → PASS/FAIL.
            - #get_port_metrics
              Unidirectional traffic → poll Port Metrics → PASS/FAIL.
            - #get_bidirflow_flow_metrics
              Bidirectional flow → start → poll Flow Metrics summary.
            - #get_bidirflow_port_metrics
              Bidirectional flow → start → poll port-level Metrics summary.
            - #get_flow_loss_metrics
              Query flow loss metrics (`flow_metrics.loss`).
            - #get_flow_latency_metrics
              Query flow latency metrics (`flow_metrics.latency`).

        (3) Bound Device Flow Snippets (4):
            - #config_bound_bidirflow
              Bidirectional flow bound to simulated Device/IPv4 interfaces.
            - #config_bound_bidirflow_arp
              Device-bound bidirectional flow + start protocols (ARP gateway
              MAC resolution).
            - #get_bound_bidirflow_arp_table
              Query IPv4 ARP neighbor table to verify gateway MAC learning.
            - #get_bound_bidirflow_flow_metrics
              Full closed loop: Device-bound flow (config → ARP → traffic →
              verify).

        (4) QoS Snippets (3):
            - #config_dscp_ecn
              ECN (Explicit Congestion Notification) marking layered on DSCP.
            - #config_dscp_phb_numeric
              DSCP priority configured with a raw numeric PHB value.
            - #config_dscp_phb_symbolic
              DSCP priority configured with symbolic PHB constants (cycling
              per packet).

        (5) BGP / Emulated Device Snippets (8):
            - #config_ebgp
              Basic dual-sided eBGP (External BGP) session configuration.
            - #config_ebgp_flow
              eBGP session + bidirectional flow bound to BGP-advertised
              routes.
            - #config_bgpv6
              Basic dual-sided eBGP over IPv6 (BGP+) configuration.
            - #get_ebgp_state
              eBGP session establishment + poll BGP session state (UP).
            - #get_bgpv6_state
              eBGP over IPv6 session establishment + poll session state.
            - #get_ebgp_flow_metrics
              Full eBGP closed loop (session → route-bound traffic →
              forwarding verify).
            - #run_ping
              ICMP ping between simulated IPv4 interfaces with result check.
            - #send_bgp_notification
              Send BGP NOTIFICATION message to trigger session termination.

        (6) ISIS Snippets (1):
            - #config_isis_session
              ISIS adjacency session establishment + poll verification
              (PASS/FAIL).

3.2 Dot-Triggered Intelligent Auto-Completion
    In any Python file, typing . after any OTG object immediately surfaces
    precise sub-property candidates from the internal dictionary:
    - Property entries: displayed with a property icon. Each entry shows the
      official OpenAPI description in the detail pane, together with a support
      status badge: "Supported (v1.19.0)" indicates the property is
      implemented in TestCenter; "Not supported" (marked deprecated) indicates
      the property belongs to the broader OTG specification but is not yet
      supported in the current TestCenter version.

3.3 Contextual Variable Type Inference Engine
    To compensate for the weakly-typed nature of the underlying OTG object
    model, the extension applies a full-document variable scanning engine that
    resolves short aliases to complete OTG type paths, enabling completion on
    variables without explicit type annotations:
    - Simple assignment inference: writing `flw = cfg.flows.flow(name='f1')`
      causes typing `flw.` to show completions scoped to the
      `config.flows.flow` node.
    - Destructuring assignment inference: writing
      `eth, ip, udp = flw.packet.ethernet().ipv4().udp()` maps each variable
      to its respective header type independently. Typing `ip.` shows only
      IPv4 header fields; typing `udp.` shows only UDP header fields.
    The inference engine rescans the full document after every edit, keeping
    inferred types accurate as the script evolves.

3.4 Structured Hover Documentation (Hover Provider)
    Hovering over any OTG property token in the editor opens a Markdown card
    generated directly from the internal dictionary, containing:
    - OTG path: the full dot-notation specification key
      (e.g. `config.flows.packet.ipv4.src`).
    - Support status: "Supported (v1.19.0)" or "Not supported".
    - Description: the cleaned official OpenAPI description.
    - Type and format: data type (e.g. `string`, `integer`) and format
      constraints (e.g. `mac`, `ipv4`, where applicable).
    - Default value: the model-defined default (where present).
    - Min / Max: numeric range for integer and number properties.
    - Enum values: the complete enumeration list for string properties with a
      fixed value set (e.g. `choice` properties).
    Hover also works in keyword-argument context — hovering over `address` in
    `ipv4(address="10.0.0.1", ...)` shows that parameter's OpenAPI
    description, type, and format (ipv4 string) without moving the cursor.


4. OTG Object and Result Coverage
----------------------------------
The internal dictionary fully covers the following OTG namespaces:

- config:          The complete OTG Config object tree (ports, flows, devices,
                   lags, layer1, captures, lldp, options), including all
                   packet header stacks (Ethernet, IPv4, IPv6, TCP, UDP, VLAN,
                   MPLS, GRE, ICMPv4, ICMPv6, ARP, PFC Pause, Custom) and
                   their full field hierarchies (fixed value, increment,
                   decrement, random, value_list, metric_tags).
- api:             Top-level API method nodes (set_config, get_config,
                   get_metrics, get_states, get_capture, set_control_state,
                   set_control_action, etc.).
- config_update:   ConfigUpdate / incremental update object tree.
- metrics_request: MetricsRequest and all sub-objects (flow, port, bgpv4,
                   bgpv6, isis, lacp, lldp, rsvp, etc.), including choice
                   enums.
- states_request:  StatesRequest and all sub-objects (bgpv4_peers, isis_lsps,
                   dhcpv4_clients, etc.), including choice enums.
- control_state:   ControlState object (traffic transmit, port link,
                   protocol start/stop), with full enum lists.
- control_action:  ControlAction object.
- capture_request: CaptureRequest object.
- snappi:          Top-level snappi Python module path nodes.

Support status breakdown:
- Supported in TestCenter v1.19.0:    9,347 properties
- OTG spec only (not yet in TC):     11,976 properties


5. Snippet Usage and Code Examples
------------------------------------

5.1 Inserting a Snippet
    In any .py file, type # followed by a prefix keyword. The editor
    immediately shows a completion list of all matching snippets. Continue
    typing to filter (e.g. #config for configuration-only snippets, #get for
    snippets with polling and verification, #bgp for BGP snippets), then press
    Enter or Tab to insert. The #<prefix> trigger text is replaced with the
    complete runnable code snippet.

    5.1.1 Placeholder Constants
        Each snippet exposes three constants at the top of the script that
        must be replaced with actual values before running:
        1. API  — OTG server endpoint address (e.g. "0.0.0.0:50051")
        2. PTX  — Tx port chassis location (e.g. "//10.126.32.98/4/5")
        3. PRX  — Rx port chassis location (e.g. "//10.126.32.98/4/6")

    5.1.2 Choosing the Right Snippet
        - Basic unidirectional Raw traffic (config only): use `#config_flow`.
        - Basic unidirectional Raw traffic (with start + collect + verify):
          use `#get_flow_metrics` (flow-level) or `#get_port_metrics`
          (port-level).
        - Bidirectional Raw traffic: use `#config_bidirflow` (config only) or
          `#get_bidirflow_flow_metrics` (full verify loop).
        - Traffic bound to simulated IPv4 devices rather than raw ports: use
          `#get_bound_bidirflow_flow_metrics`.
        - Test requires BGP session UP before sending traffic: use
          `#get_ebgp_flow_metrics` — the snippet includes a BGP session UP
          polling loop.
        - Latency measurement needed: use `#get_flow_latency_metrics` — the
          snippet enables `metrics.latency` and prints average and maximum
          latency in nanoseconds.
        - Verify Layer 3 reachability between two simulated devices before a
          full traffic test: use `#run_ping`.
        - Fine-grained traffic control (start/stop independently): use
          `#start_flow_by_control` / `#stop_bidirflow`.

5.2 Basic Code Workflow
    Typical scripting workflow after inserting the `#get_flow_metrics` snippet:

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

    # After insertion, the variable inference engine automatically recognizes
    # all variable bindings:
    # - `flw` is inferred as config.flows.flow — typing `flw.` shows flow
    #   property completions (size, rate, duration, metrics, packet, etc.).
    # - `eth`, `ip`, `udp` are each inferred from the destructuring
    #   assignment. Typing `ip.` shows only IPv4 header fields; typing `udp.`
    #   shows only UDP header fields.
    #
    # Example: to add DSCP marking, type `ip.priority.` → select `choice`,
    # then type `ip.priority.dscp.` → select `phb.` to reach PHB fields.

5.3 Viewing Property Details with Hover Documentation
    Before editing an unfamiliar property, hover over it to open the
    documentation card. For example, hovering over `flw.metrics.enable`
    displays:
    - OTG path:      config.flows.flow.metrics.enable
    - Support:       Supported (v1.19.0)
    - Type:          boolean
    - Default:       false
    - Description:   Enables flow metrics collection for this flow.


6. Support, Enhancements, and Ongoing Updates
----------------------------------------------

6.1 Ongoing Development
    This extension is under active maintenance. Future releases will update
    the knowledge-base dictionary to align with new TestCenter software
    versions and OTG specification revisions, and will expand the built-in
    snippet library to cover a broader range of complex test workflows,
    including additional emulated device and protocol session scenarios.

6.2 Technical Support and Feedback
    Your feedback is essential to improving this extension. For any defects,
    technical assistance, or feature suggestions and enhancement requests,
    please contact our support team:

    - Support Email: HSESupportBJ@viavisolutions.com

    We welcome inquiries on the following:
    - Bug Reports & Troubleshooting: completion, hover, or inference issues.
    - Feature Requests & Enhancements: structural additions or improvements.
    - New Snippets & Protocol Requests: test workflows or snippets you would
      like supported in future releases.


7. Important Notes and Prerequisites
--------------------------------------

7.1 Lazy-Loading Activation
    To keep the environment lightweight, the extension uses a lazy-loading
    architecture. It activates and loads the full 21,323-node dictionary only
    when a Python file (.py) is actually opened, ensuring zero idle memory
    overhead during work in other languages.

7.2 Prerequisites
    - This extension operates strictly as a front-end syntax assistance tool.
      To execute the generated scripts, the local or remote environment must
      have the snappi Python package installed (`pip install snappi`) and be
      able to connect to a running TestCenter OTG server endpoint.
    - The extension itself requires no internet connection; the complete OTG
      knowledge base is bundled as a local file inside the VSIX package.
