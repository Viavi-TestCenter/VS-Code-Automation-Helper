================================================================================
Viavi TestCenter Restful API Python VS Code Helper Readme
Version: 1.0.2
Release Date: 2026-10-28
================================================================================

1. Overview
-----------

1.1 Introduction
    Viavi TestCenter Restful API Python VS Code Helper is an extension designed
    specifically for Viavi TestCenter Restful API (HTTP protocol via the
    stcrestclient library) automation scripting. By deeply parsing the REST data
    schema, it lowers the lookup overhead caused by the weakly-typed HTTP
    interface, thereby enhancing script delivery quality and protocol simulation
    development efficiency across major VS Code-based editors.

1.2 Key Features at a Glance
    - Built-in Code Samples & Code Blocks — 56 code samples + 7 code blocks, one-click insertion.
    - 20 Core API Methods — instant `tc.` method scaffolding.
    - Context Inference Engine — automatic handle-type deduction.
    - Intelligent Auto-Completion — object types, commands, and attribute suggestions.
    - Structured Hover Documentation — clean Markdown with Type / Default / enum.
    - Numbered Code Samples — every code sample prefix carries a unique sequence
      number (e.g. `R013`), making it easy to tell samples apart by source when
      multiple extensions are installed side by side.

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
    1. Open the Extensions panel (`Ctrl+Shift+X`) and locate TC Restful API Python Helper.
    2. Click the gear icon (⚙) → Uninstall, then restart the editor.
    3. Follow steps 1–4 in 2.1 above to install the new `.vsix` file.

    Note: Some editors support installing a new VSIX directly over the existing
    version — the old version is replaced automatically without a manual
    uninstall step.


3. Feature Coverage & Characteristics
-------------------------------------

3.1 Built-in Code Samples & Code Block Manager
    This version includes 56 code samples and 7 code blocks, supporting three rapid
    deployment workflows within Python files.

    3.1.1 Three Ways to Insert
        - [Workflow A] Inline Trigger: type `#` at the start of a line in any
          `.py` file — the editor immediately pops up the full sample/block list.
          Continue typing a prefix keyword (e.g. `#raw_stream` or `#create_bgp`)
          to filter in real time, then press `Enter` or `Tab` to insert; the `#`
          character is automatically replaced by the generated code.
        - [Workflow B] Full Prefix + Tab: type the complete prefix name
          (e.g. `R027_config_raw_stream_fixed_frame_ttl`) then press `Tab` to expand.
        - [Workflow C] Interactive Code Sample Menu (Recommended): press
          `Ctrl+Shift+I` to open a two-level Quick Pick UI — pick a category,
          then a code sample or code block, and the snippet drops in at the cursor:

                Category                                Count
                Raw StreamBlock Code Samples               20
                Bound StreamBlock Code Samples              8
                Emulated Device Code Samples               27
                Benchmark Test Code Samples                 1
                Code Blocks                                 7

        Full step-by-step instructions are in section 5.1.

    3.1.2 Available Code Sample Prefixes
        Trigger by typing `#` followed by the prefix name. The prefix name
        shown below is what appears in the completion popup (no `#` displayed).
        Except for code blocks, every code sample prefix now carries a unique
        sequence number (`R001`–`R056`), making it easy to tell code samples
        apart by source when multiple Viavi TestCenter API extensions (e.g. the
        Native API and REST API editions) are installed side by side — `#`
        completion no longer gets confused by duplicate prefixes. The numbering
        is globally continuous; code blocks are not numbered.

        (1) Raw Traffic Code Samples (20):
            - R025_config_raw_stream_auto_frame_signature
              Auto frame length + insert signature field (EthernetII+IPv4, TTL).
            - R026_config_raw_stream_prbs_fcs_error
              PRBS payload + FCS error insertion.
            - R027_config_raw_stream_fixed_frame_ttl
              Fixed frame length + TTL adjustment (EthernetII+IPv4).
            - R028_config_raw_stream_incr_frame
              Incrementing frame length (EthernetII+IPv4, no signature).
            - R029_config_raw_stream_random_frame_constant_fill
              Random frame length + constant fill (EthernetII+IPv4).
            - R030_config_raw_stream_tcp
              Raw stream with EthernetII + IPv4 + TCP header.
            - R031_config_raw_stream_udp
              Raw stream with EthernetII + IPv4 + UDP header.
            - R032_config_raw_stream_ipv6
              Raw stream with EthernetII + IPv6 headers + port stats subscribe/collect.
            - R033_config_raw_stream_vlan
              Raw stream with EthernetII + VLAN + IPv4 headers + port stats subscribe/collect.
            - R034_run_raw_stream_capture_save
              Raw stream transmission + port packet capture saved to PCAP file.
            - R036_config_raw_stream_ipv4
              Basic Raw StreamBlock configuration and result collection.
            - R037_config_raw_stream_bidirectional
              Bidirectional fixed-frame Raw stream + Tx/Rx result collection, port release and cleanup.
            - R038_get_port_results
              Retrieve Generator/Analyzer port-level results (Tx/Rx port statistics).
            - R039_get_raw_stream_results
              Retrieve RxStreamSummaryResults/TxStreamResults (per-stream statistics).
            - R040_get_raw_stream_loss_results
              Retrieve Raw stream loss results (reading DroppedFrameCount directly).
            - R041_get_raw_stream_latency_results
              Retrieve Raw stream latency results (AvgLatency/MinLatency/MaxLatency).
            - R043_config_raw_stream_dscp_phb_numeric
              Configure DSCP PHB numeric values via tosDiffserv+diffServ.
            - R044_config_raw_stream_dscp_ecn
              Configure DSCP PHB + ECN via tosDiffserv+diffServ.
            - R055_start_traffic
              Start and stop StreamBlock traffic.
            - R056_stop_traffic
              Configure, start, and stop StreamBlock traffic (self-contained example).

        (2) Bound Traffic Code Samples — StreamBlocks Bound to Emulated Devices (8):
            - R019_config_bound_stream_fixed_frame
              Fixed-frame bound stream between two emulated devices.
            - R020_config_bound_stream_pair_incr_frame
              Device-pair bound stream with incrementing frame length.
            - R021_config_bound_stream_auto_frame
              Auto frame length bound stream.
            - R022_config_bound_stream_port_based_rate
              Port-load-based bound stream allocation.
            - R023_config_bound_stream_bidirectional_random_frame
              Random frame length bidirectional bound stream.
            - R024_config_bound_stream_ipv6
              Bound stream between two IPv6 devices (global + link-local addresses).
            - R042_config_bound_stream_bidirectional_arp
              Bidirectional bound stream + ArpNdStartCommand to resolve gateway MAC.
            - R054_get_bgp_bound_stream_results
              Retrieve BGP bound stream results (ProtocolStart + RxStreamSummaryResults).

        (3) Emulated Device Code Samples — Protocol Stacks (27):
            - R002_create_device_ipv4
              Basic IPv4 emulated device configuration.
            - R003_create_device_bgp_ipv4_routes
              IPv4 BGP dual-device + route block configuration.
            - R004_create_device_dhcpv4_bound_stream
              DHCPv4 Server + Client full simulation with traffic.
            - R005_create_device_ospfv2_lsa
              OSPFv2 two devices with LSA topology generator.
            - R006_create_device_isis_lsp
              IS-IS Level-2 IPv4 two devices with LSP topology.
            - R007_create_device_group_ip_mac_step
              Multi-device group with IP / MAC / GW step configuration.
            - R008_create_devices_one_port
              Three emulated devices bound to one port.
            - R009_create_device_l2
              Pure Layer-2 Ethernet emulated device (no IPv4), dual port.
            - R010_create_device_ipv6
              Two emulated devices with global IPv6 + link-local IPv6 interfaces.
            - R011_create_device_vlan
              Two emulated devices with VLAN interface (VlanIf stacked on EthIIIf).
            - R012_create_device_vlan_bound_stream
              Two VLAN devices + Ipv4If-over-VlanIf-over-EthIIIf bound stream.
            - R013_create_device_igmp_bound_stream
              IGMP host dual-device subscribed to same multicast group + bound stream.
            - R014_create_device_gptp
              gPTP (IEEE 802.1AS-2020) clock dual-device + result subscription.
            - R015_create_device_dot1x_eap_md5
              802.1X Dot1x Supplicant + EAP-MD5 authentication configuration.
            - R016_create_device_pppoe
              PPPoE Client + Server dual-device with full interface stack.
            - R017_create_device_stp
              Two devices + BridgePortConfig (STP bridge port priority emulation).
            - R018_create_device_rocev2_qp
              RoCEv2 Queue Pair dual-port with PFC / ECN / CNP / VLAN and traffic binding.
            - R035_config_device_ping_response
              Configure device Ping response (parameterized RouterId, PrefixLength) — two devices.
            - R045_get_device_arp_table
              Retrieve port ARP table via ArpNdUpdateArpCacheCommand.
            - R046_run_ping
              Execute ICMP Ping via PingStartCommand and read PingReport.
            - R047_send_bgp_notification
              Send BGP CEASE notification via L2TestBreakLinkCommand.
            - R048_config_link_flap
              Link flap via L2TestBreakLinkCommand + L2TestRestoreLinkCommand.
            - R049_get_bgp_state_ipv4
              Retrieve BGP IPv4 session state.
            - R050_get_bgp_state_ipv6
              Retrieve BGP IPv6 session state.
            - R051_get_isis_session_results
              Retrieve ISIS session results (IsisRouterResults).
            - R052_create_device_bgp_ipv6_routes
              Two IPv6 eBGP devices + BgpIpv6RouteConfig configuration.
            - R053_create_device_bgp_ipv4_bound_stream
              eBGP IPv4 device + bound stream configuration (with UsesIf).

        (4) Benchmark Test Code Samples (1):
            - R001_create_rfc2544_throughput
              RFC 2544 throughput test (two devices + binary search).

        (5) Code Blocks (7):
            Trigger by typing `#tc_block_`, or select the Code Blocks category
            from the `Ctrl+Shift+I` menu. Code blocks are not part of the R0xx
            numbering sequence.
            - tc_block_init
              StcHttp import + Lab Server connection + session creation.
            - tc_block_project_ports
              Project + two Port objects + AttachPorts + apply framework block.
            - tc_block_device_ipv4
              EmulatedDevice + EthIIIf + Ipv4If device creation block.
            - tc_block_device_bind_ipv4
              IPv4 device interface association binding block.
            - tc_block_raw_stream_ipv4
              Raw StreamBlock + EthernetII + IPv4 header traffic block.
            - tc_block_run_devices
              Start all devices + sleep + stop all devices block.
            - tc_block_subscribe_port_results
              Subscribe to Analyzer and Generator port-level result block.

3.2 Core API Methods
    The helper encapsulates 20 core methods of the Viavi TestCenter REST API.
    Typing `tc.` in a Python context instantly generates the standard method
    structure populated with placeholders:
    - apply              Commits and applies current test configuration to chassis.
    - config             Sets or modifies one or more object attributes/relations.
    - connect            Establishes connection to a Viavi TestCenter chassis.
    - create             Creates an automation object under the specified parent.
    - delete             Deletes specified object handle from the test config.
    - disconnect         Terminates connection with a Viavi TestCenter chassis.
    - download           Downloads and saves a specified file from the Lab Server.
    - download_all       Downloads all files from the Lab Server.
    - end_session        Ends the test session (optionally terminates server-side session).
    - files              Gets the list of available files on the Lab Server.
    - get                Retrieves attribute values, read-only data, or handles.
    - help               Queries data model and API commands for help information.
    - join               Joins an existing test session on the Lab Server.
    - log                Writes diagnostic messages with severity levels to logs.
    - new_session        Creates and joins a new test session on the Lab Server.
    - perform            Executes a Viavi TestCenter Command (e.g., AttachPorts).
    - set_timeout        Sets the response wait timeout in seconds (0 = no timeout).
    - system_info        Retrieves system information from the Lab Server.
    - upload             Uploads a configuration file or other file to the Lab Server.
    - wait_until_complete Blocks execution until an asynchronous Sequencer command completes.

3.3 Static Schema & Context Inference Engine
    Addressing the weakly-typed nature of the REST API, the helper applies a
    static AST (Abstract Syntax Tree) type-deduction engine to eliminate property
    name conflicts across different objects:
    - Creation Inference: If you type `tc.config(hPortTx, )`, the helper traces
      back to find `hPortTx = tc.create("Port", hProject, ...)`. It locks `hPortTx`
      as a `Port` entity and restricts completion hints to its exclusive writable
      properties (e.g., useDefaultHost=).
    - Retrieval Inference: Supports child object relation deduction. If a handle
      is retrieved via a relation like `hGenerator = tc.get(hPort,
      "children-Generator")`, the helper correctly recognizes it as a `Generator`
      entity in subsequent calls, displaying correct counters and properties.

3.4 Intelligent Auto-Completion
    The helper automatically scans the document to identify the variable names of
    every StcHttp instance in the current file, and filters and provides precise
    candidate suggestions whenever a method call on one of those variables is
    detected:
    - Object Type Hints: Inside `tc.create("`, it triggers autocomplete for all
      Viavi TestCenter object classes like StreamBlock, BgpRouterConfig, etc.
    - Command Hints: Inside `tc.perform("`, it populates available system commands
      with official Markdown descriptions (e.g., AttachPortsCommand).

    Note: In `tc.create(object_type, parent, **kwargs)`, the parent handle is a
    positional argument — the `under=` keyword is not used.

3.5 Structured Hover Documentation (Hover Provider)
    Hovering over Viavi TestCenter methods, object classes, attributes, or
    commands opens a polished Markdown window. Each document undergoes precise
    field extraction:
    - Hierarchy & Rules: Features a clean, unified, card-style visual layout.
    - Metadata Row: Extracts explicit fields for Type (e.g., bool, handle) and
      Default values, alongside valid enum values and Deprecated flags.
    - Descriptions: Strips residual punctuation from raw data to offer clean,
      official descriptions.


4. Protocol & Results Object Support Range
------------------------------------------
- Routing Protocols: BGP, OSPFv2/v3, IS-IS.
- Access & Authentication: DHCPv4/v6, 802.1X Dot1x, PPPoE.
- Multicast & Time Sync: IGMP, MLD, IEEE 802.1AS / gPTP.
- Layer 2 Protocols: STP / RSTP / MSTP, VLAN.
- RoCEv2.
- RFC 2544: Full four-test coverage — Throughput, Latency, Frame Loss, and Back-to-Back.
- Traffic Models: Raw StreamBlocks (IPv4/IPv6/VLAN/TCP/UDP/DSCP + capture),
  Bound StreamBlocks (IPv4/IPv6, bidirectional, port load config).
- Results Objects: Port-level, Stream-level, and Protocol Session-level.


5. Code Sample / Code Block Usage & Workflow
--------------------------------------------

5.1 Using Code Samples and Code Blocks
    There are three ways to insert a code sample or code block into your Python script:

    5.1.1 Method 1 — Type `#` to trigger inline completion (Recommended)
        1. In any `.py` file, type `#` at the start of a line.
        2. The editor immediately shows all available code samples and code blocks
           as a completion list.
        3. Continue typing a keyword to filter (e.g. `#raw_stream` for Raw stream
           code samples, `#create_bgp` for the BGP device sample,
           `#tc_block_` for code blocks).
        4. Select the desired entry and press `Enter` or `Tab` to insert —
           the `#` character is automatically replaced by the full code snippet.
        5. Navigate placeholders with `Tab` / `Shift+Tab`.

    5.1.2 Method 2 — Type the full prefix and press Tab
        1. In any `.py` file, type the complete code sample prefix name
           (e.g. `R027_config_raw_stream_fixed_frame_ttl`).
        2. Press `Tab` — the prefix expands into a complete, runnable code snippet.
        3. The cursor jumps to the first placeholder. Enter the required value
           (e.g. Lab Server IP).
        4. Press `Tab` to advance to the next placeholder; press `Shift+Tab` to go back.
        5. Continue until all placeholders are filled, then run the completed script.

    5.1.3 Method 3 — Hierarchical picker (Ctrl+Shift+I)
        1. Place your cursor at the target insertion point in a `.py` file.
        2. Press `Ctrl+Shift+I` (or open the Command Palette and run
           `TC: Insert Code Template`).
        3. Select a category from the first list (sample count shown on the right).
        4. Select a specific code sample or code block from the second list.
        5. The full snippet is inserted — use `Tab` / `Shift+Tab` to navigate placeholders.

    5.1.4 Placeholder Navigation Keys
        - Tab          Move to the next placeholder
        - Shift+Tab    Move to the previous placeholder
        - Escape       Exit placeholder mode (retains current values)

    5.1.5 Example — `R036_config_raw_stream_ipv4` placeholder order
        1. szServerIp      — Lab Server IP address (REST API server), default: 192.168.0.200
        2. szUser          — Session user name label, default: JoeUser
        3. szSessionName   — Session name, default: ExampleTest
        4. szChassisIp     — TestCenter chassis IP address, default: 192.168.0.100
        5. iTxSlot         — Tx port slot number, default: 1
        6. iTxPort         — Tx port number, default: 1
        7. iRxSlot         — Rx port slot number, default: 1
        8. iRxPort         — Rx port number, default: 2
        9. szMacAddrPortA  — Source MAC address (Port A), default: 22:22:22:22:22:25
        10. szMacAddrPortB — Destination MAC address (Port B), default: 22:22:22:22:22:22
        11. txIpAddr       — Source IP address, default: 20.0.0.2
        12. rxIpAddr       — Destination IP address, default: 30.0.0.2

5.2 Basic Code Workflow
    A typical script-authoring flow inside a `.py` file:

    from stcrestclient import stchttp

    tc = stchttp.StcHttp("192.168.0.200")
    tc.new_session("JoeUser", "ExampleTest")

    # 1. Option A: Press 'Ctrl+Shift+I' inside a Python file to visually pick a sample.
    #    Option B: Autocomplete triggers candidate object types. Select "Project".
    hProject = tc.create("Project")

    # 2. Define port handles (parent is a positional argument, not under=)
    hPortTx = tc.create("Port", hProject, location="//192.168.0.100/1/1",
                          useDefaultHost="False")

    # 3. Context inference locks 'hPortTx' as a 'Port' object type.
    #    Writable port attributes pop up instantly with auto-appended equals signs.
    tc.config(hPortTx, useDefaultHost="False")

    # 4. Command autocomplete: pull commands and complete internal parameters.
    tc.perform("AttachPortsCommand", autoConnect="TRUE")


6. Support, Enhancements & Continuous Roadmap
---------------------------------------------

6.1 Continuous Updates & Evolution
    The helper is under ongoing maintenance. Future releases will update the
    data schema dictionary to align with new Viavi TestCenter software versions,
    add deeper semantic analysis, and extend the built-in code sample and code
    block library to cover a broader range of testing workflows.

6.2 Technical Support & Feedback Contact
    Your feedback is vital to improving the helper. If you encounter any bugs,
    require technical assistance, or wish to suggest features/enhancements,
    please reach out to our support desk:

    - Support Email: HSESupportBJ@viavisolutions.com

    Please feel free to contact us regarding:
    - Bug Reports & Troubleshooting: Autocomplete, hover, or syntax issues.
    - Feature Requests & Enhancements: Structural additions or improvements.
    - New Code Sample/Protocol Submissions: Desired test workflows or code samples
      to be supported in subsequent releases.


7. Important Notes & Environment Prerequisites
----------------------------------------------

7.1 Lazy Activation Mechanism
    To maintain a lightweight environment, the helper uses a lazy-loading
    architecture. It activates and loads the schema dictionary only when an
    actual Python file ending in `.py` is opened, ensuring zero idle memory
    consumption during regular coding sessions.

7.2 Prerequisites
    - The stcrestclient Python library must be installed (pip install stcrestclient)
      with access to a Viavi TestCenter Lab Server.
    - Each Python script must include `from stcrestclient import stchttp` — the
      helper identifies StcHttp instances from this import to activate autocomplete
      and hover documentation features.


8. Changes in This Version (1.0.2) Relative to 1.0.1
-----------------------------------------------------

8.1 Added
    - Added a unified sequence-number prefix (`R001`–`R056`) to every code sample
      except code blocks, making it easy to tell code samples apart by source when
      multiple Viavi TestCenter API extensions (e.g. the Native API and REST API
      editions) are installed side by side — `#` completion no longer gets confused
      by duplicate prefixes.
    - Added a dedicated `Benchmark Test` category (currently 1 code sample:
      `R001_create_rfc2544_throughput`).

8.2 Changed
    - The code sample tables and placeholder examples in README/READMECN were
      rewritten to match the actual current prefixes in `tc_snippets.json`.
