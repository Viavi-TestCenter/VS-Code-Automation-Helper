================================================================================
Viavi TestCenter OTG Snappi Python API VS Code Helper Readme
Version: 1.0.0
Release Date: 2026-07-09
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
    - Interactive Template/Example Manager — 14 production-ready snippets,
      one-click insertion via `#` prefix trigger.
    - Dot-Triggered Intelligent Auto-Completion — precise child property
      candidates from a 21,323-node static dictionary.
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

    3.1.1 Available Template/Example Prefixes (14 total)

        (1) Raw Traffic Templates/Examples (5):
            - #raw_unidir_flow
              Unidirectional port-based flow (Eth/IPv4/UDP headers) with
              flow-level Tx/Rx metrics and a PASS/FAIL convergence loop.
            - #raw_unidir_port
              Same unidirectional pattern but polls port-level counters instead
              of per-flow metrics.
            - #raw_bidir_flow
              Two antiparallel flows (f1: p1->p2, f2: p2->p1) with different
              frame sizes; verifies combined Tx/Rx frame count via flow metrics.
            - #raw_bidir_port
              Bidirectional raw flows verified against port-level counters with
              explicit column selection (FRAMES_TX, FRAMES_RX).
            - #raw_link_flap
              Raw flow with an in-traffic port link-down/link-up sequence;
              verifies full frame delivery survives the flap window.

        (2) Bound Device Traffic Templates/Examples (1):
            - #bound_bidir_metrics
              Two emulated IPv4 devices on separate ports with bidirectional
              bound flows (tx_rx.device); starts ARP/protocol stack before
              traffic and verifies frame counts via flow metrics.

        (3) Device & Protocol State Templates/Examples (2):
            - #dev_arp_table
              Two emulated IPv4 devices; starts the protocol stack, waits for
              ARP exchange, then queries the IPv4 neighbor table via
              `get_states()` and verifies both MACs are resolved.
            - #dev_ping
              Two emulated IPv4 devices; starts the protocol stack, issues an
              IPv4 ping via `set_control_action()`, and verifies all responses
              succeeded.

        (4) BGP Templates/Examples (2):
            - #bgp_ebgp_traffic
              Two eBGP peers (IPv4, separate ASNs) each advertising 5 prefixes;
              waits for BGP session UP, then sends bound flows into the
              advertised routes and verifies end-to-end forwarding with a
              PASS/FAIL loop.
            - #bgp_v6
              eBGP+ over IPv6 link-local addresses advertising IPv6 prefixes;
              monitors session state via `bgpv6_metrics` and reports PASS/FAIL.

        (5) QoS Templates/Examples (4):
            - #qos_dscp_ecn
              Raw flow with DSCP PHB set to alternating AF11/AF21 values and
              ECN field explicitly cleared; runs for 30 s and prints per-flow
              stats.
            - #qos_dscp_phb_numeric
              Same QoS flow but sets the PHB field using a raw integer value
              instead of symbolic constants — useful for testing non-standard
              codepoints.
            - #qos_dscp_phb_symbolic
              Raw flow cycling through AF11/AF21 symbolic PHB constants
              per-packet; verifies DSCP marking via flow metric counters.
            - #qos_latency
              Raw flow with store-forward latency measurement enabled
              (`metrics.latency.mode = "store_forward"`); reports average and
              maximum latency in nanoseconds alongside Tx/Rx frame counts.

3.2 Dot-Triggered Intelligent Auto-Completion
    Inside any Python file, typing `.` after any OTG object instantly displays
    precise child property candidates sourced from the internal dictionary:
    - Property Items: Displayed with a Property icon. Each entry shows an
      official OpenAPI description in the detail pane, plus a support badge:
      "Supported (v1.19.0)" for properties implemented in TestCenter, or
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
    - Support Status: "Supported (v1.19.0)" or "Not supported".
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
- TestCenter v1.19.0 Supported:     9,347 properties
- OTG Spec Only (Not yet in TC):   11,976 properties


5. Template/Example Usage & Code Example
-----------------------------------------

5.1 Inserting a Template/Example
    Type `#` followed by a prefix keyword in any `.py` file. The editor
    immediately shows all matching templates/examples as a completion list.
    Continue typing to filter (e.g. `#raw` for Raw traffic templates/examples,
    `#bgp` for BGP templates/examples), then press `Enter` or `Tab` to insert.
    The `#<prefix>` trigger text is automatically replaced by the full,
    runnable code snippet.

    5.1.1 Placeholder Constants
        Each template/example exposes three constants at the top of the script
        that you substitute before running:
        1. API  — OTG server endpoint address (e.g. "0.0.0.0:50051")
        2. PTX  — Tx port chassis location (e.g. "//10.126.32.98/4/5")
        3. PRX  — Rx port chassis location (e.g. "//10.126.32.98/4/6")

    5.1.2 Choosing the Right Template/Example
        - Use `#raw_unidir_flow` or `#raw_unidir_port` for basic unidirectional
          raw traffic — flow metrics vs. port-level counters respectively.
        - Use `#bound_bidir_metrics` when flows must be bound to emulated IPv4
          devices rather than raw ports.
        - Use `#bgp_ebgp_traffic` when the test requires BGP session bring-up
          before sending traffic — the template/example includes the BGP
          session UP polling loop automatically.
        - Use `#qos_latency` when store-forward latency measurement is required
          — the template/example enables `metrics.latency` and prints average
          and maximum latency in nanoseconds alongside the frame counters.
        - Use `#dev_ping` to verify Layer-3 reachability between two emulated
          devices before committing to a full traffic test.

5.2 Basic Code Workflow
    A typical script-authoring flow after inserting the `#raw_unidir_flow`
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
    - Status:     Supported (v1.19.0)
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
    architecture. It activates and loads the full 21,323-node dictionary only
    when an actual Python file ending in `.py` is opened, ensuring zero idle
    memory consumption during regular coding sessions in other languages.

7.2 Prerequisites
    - The helper functions strictly as a front-end syntax assistant. To execute
      the generated scripts, the local or remote environment must have the
      snappi Python package installed (`pip install snappi`) and network
      connectivity to a running TestCenter OTG server endpoint.
    - No internet connection is required for the helper itself; the entire OTG
      knowledge base is bundled locally inside the VSIX package.
