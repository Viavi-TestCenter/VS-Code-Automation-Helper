================================================================================
Viavi TestCenter Native Python API VS Code Helper Readme
Version: 2.0.4
Release Date: 2026-10-28
================================================================================

1. Overview
-----------

1.1 Introduction
    Viavi TestCenter Native Python API VS Code Helper is an extension designed
    specifically for Viavi TestCenter Native Python API automation scripting.
    By deeply parsing the native data schema, it lowers the lookup overhead
    caused by the low-level weakly-typed API, thereby enhancing script delivery
    quality and protocol simulation development efficiency across major
    VS Code-based editors.

1.2 Key Features at a Glance
    - Built-in Code Examples & Code Blocks — 56 code examples + 7 code blocks, one-click insertion.
    - 17 Core API Methods — instant `tc.` method scaffolding.
    - Context Inference Engine — automatic handle-type deduction, including multi-line calls.
    - Intelligent Auto-Completion — object types, commands, subscribe parameters, and auto-import.
    - Structured Hover Documentation — clean Markdown with Type / Default / enum.
    - Numbered Code Examples — every code example prefix carries a unique sequence
      number (e.g. `N013`), making it easy to tell examples apart by source when
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
    1. Open the Extensions panel (`Ctrl+Shift+X`) and locate TC Python Helper.
    2. Click the gear icon (⚙) → Uninstall, then restart the editor.
    3. Follow steps 1–4 in 2.1 above to install the new `.vsix` file.

    Note: Some editors support installing a new VSIX directly over the existing
    version — the old version is replaced automatically without a manual
    uninstall step.


3. Feature Coverage & Characteristics
-------------------------------------

3.1 Built-in Code Examples & Code Block Manager
    This version includes 56 code examples and 7 code blocks, supporting three rapid
    deployment workflows within Python files.

    3.1.1 Three Ways to Insert
        - [Workflow A] Inline Trigger: type `#` at the start of a line in any
          `.py` file — the editor immediately pops up the full template/example list.
          Continue typing a prefix keyword (e.g. `#raw_stream` or `#create_bgp`)
          to filter in real time, then press `Enter` or `Tab` to insert; the `#`
          character is automatically replaced by the generated code.
        - [Workflow B] Full Prefix + Tab: type the complete prefix name
          (e.g. `N027_config_raw_stream_fixed_frame_ttl`) then press `Tab` to expand.
        - [Workflow C] Interactive Code Example Menu (Recommended): press
          `Ctrl+Shift+I` to open a two-level Quick Pick UI — pick a category,
          then a code example, and the snippet drops in at the cursor:

                Category                                Count
                Raw StreamBlock Code Examples               20
                Bound StreamBlock Code Examples              8
                Emulated Device Code Examples               27
                Benchmark Test Code Examples                 1

        Full step-by-step instructions are in section 5.1.

        Note: As of 2.0.4, the category picker groups items by the explicit
        `category` field in the code example JSON instead of guessing from the
        prefix string. An example with a missing or misspelled `category` falls
        back into an "Other Templates" bucket instead of disappearing from the list.

    3.1.2 Available Code Example Prefixes
        Trigger by typing `#` followed by the prefix name. The prefix name
        shown below is what appears in the completion popup (no `#` displayed).
        Except for TC Code Blocks, every code example prefix now carries a
        unique sequence number (`N001`–`N056`), making it easy to tell code
        examples apart by source when multiple Viavi TestCenter API extensions
        (e.g. the Native API and REST API editions) are installed side by side —
        `#` completion no longer gets confused by duplicate prefixes. The
        numbering is globally continuous; code blocks are not numbered.

        (1) Raw Traffic Code Examples (20):
            - N025_config_raw_stream_auto_frame_signature
              Auto frame length + insert signature field (EthernetII+IPv4, TTL).
            - N026_config_raw_stream_prbs_fcs_error
              PRBS payload + FCS error insertion.
            - N027_config_raw_stream_fixed_frame_ttl
              Fixed frame length + TTL adjustment (EthernetII+IPv4).
            - N028_config_raw_stream_incr_frame
              Incrementing frame length (EthernetII+IPv4, no signature).
            - N029_config_raw_stream_random_frame_constant_fill
              Random frame length + constant fill (EthernetII+IPv4).
            - N030_config_raw_stream_tcp
              Raw stream with EthernetII + IPv4 + TCP header.
            - N031_config_raw_stream_udp
              Raw stream with EthernetII + IPv4 + UDP header.
            - N032_config_raw_stream_ipv6
              Raw stream with EthernetII + IPv6 headers + port stats subscribe/collect.
            - N033_config_raw_stream_vlan
              Raw stream with EthernetII + VLAN + IPv4 headers + port stats subscribe/collect.
            - N034_run_raw_stream_capture_save
              Raw stream transmission + port packet capture saved to PCAP file.
            - N036_config_raw_stream_ipv4
              Basic Raw StreamBlock configuration and result collection.
            - N037_config_raw_stream_bidirectional
              Bidirectional fixed-frame Raw stream + Tx/Rx result collection, port release and cleanup.
            - N038_get_port_results
              Retrieve Generator/Analyzer port-level results (Tx/Rx port statistics).
            - N039_get_raw_stream_results
              Retrieve RxStreamSummaryResults/TxStreamResults (per-stream statistics).
            - N040_get_raw_stream_loss_results
              Retrieve Raw stream loss results (reading DroppedFrameCount directly).
            - N041_get_raw_stream_latency_results
              Retrieve Raw stream latency results (AvgLatency/MinLatency/MaxLatency).
            - N043_config_raw_stream_dscp_phb_numeric
              Configure DSCP PHB numeric values via tosDiffserv+diffServ.
            - N044_config_raw_stream_dscp_ecn
              Configure DSCP PHB + ECN via tosDiffserv+diffServ.
            - N055_start_traffic
              Start and stop StreamBlock traffic.
            - N056_stop_traffic
              Configure, start, and stop StreamBlock traffic (self-contained example).
        (2) Bound Traffic Code Examples — StreamBlocks Bound to Emulated Devices (8):
            - N019_config_bound_stream_fixed_frame
              Fixed-frame bound stream between two emulated devices.
            - N020_config_bound_stream_pair_incr_frame
              Device-pair bound stream with incrementing frame length.
            - N021_config_bound_stream_auto_frame
              Auto frame length bound stream.
            - N022_config_bound_stream_port_based_rate
              Port-load-based bound stream allocation.
            - N023_config_bound_stream_bidirectional_random_frame
              Random frame length bidirectional bound stream.
            - N024_config_bound_stream_ipv6
              Bound stream between two IPv6 devices (global + link-local addresses).
            - N042_config_bound_stream_bidirectional_arp
              Bidirectional bound stream + ArpNdStartCommand to resolve gateway MAC.
            - N054_get_bgp_bound_stream_results
              Retrieve BGP bound stream results (ProtocolStart + RxStreamSummaryResults).
        (3) Emulated Device Code Examples — Protocol Stacks (27):
            - N002_create_device_ipv4
              Basic IPv4 emulated device configuration.
            - N003_create_device_bgp_ipv4_routes
              IPv4 BGP dual-device + route block configuration.
            - N004_create_device_dhcpv4_bound_stream
              DHCPv4 Server + Client full simulation with traffic.
            - N005_create_device_ospfv2_lsa
              OSPFv2 two devices with LSA topology generator.
            - N006_create_device_isis_lsp
              IS-IS Level-2 IPv4 two devices with LSP topology.
            - N007_create_device_group_ip_mac_step
              Multi-device group with IP / MAC / GW step configuration.
            - N008_create_devices_one_port
              Three emulated devices bound to one port.
            - N009_create_device_l2
              Pure Layer-2 Ethernet emulated device (no IPv4), dual port.
            - N010_create_device_ipv6
              Two emulated devices with global IPv6 + link-local IPv6 interfaces.
            - N011_create_device_vlan
              Two emulated devices with VLAN interface (VlanIf stacked on EthIIIf).
            - N012_create_device_vlan_bound_stream
              Two VLAN devices + Ipv4If-over-VlanIf-over-EthIIIf bound stream.
            - N013_create_device_igmp_bound_stream
              IGMP host dual-device subscribed to same multicast group + bound stream.
            - N014_create_device_gptp
              gPTP (IEEE 802.1AS-2020) clock dual-device + result subscription.
            - N015_create_device_dot1x_eap_md5
              802.1X Dot1x Supplicant + EAP-MD5 authentication configuration.
            - N016_create_device_pppoe
              PPPoE Client + Server dual-device with full interface stack.
            - N017_create_device_stp
              Two devices + BridgePortConfig (STP bridge port priority emulation).
            - N018_create_device_rocev2_qp
              RoCEv2 Queue Pair dual-port with PFC / ECN / CNP / VLAN and traffic binding.
            - N035_config_device_ping_response
              Configure device Ping response (parameterized RouterId, PrefixLength) — two devices.
            - N045_get_device_arp_table
              Retrieve port ARP table via ArpNdUpdateArpCacheCommand.
            - N046_run_ping
              Execute ICMP Ping via PingStartCommand and read PingReport.
            - N047_send_bgp_notification
              Send BGP CEASE notification via L2TestBreakLinkCommand.
            - N048_config_link_flap
              Link flap via L2TestBreakLinkCommand + L2TestRestoreLinkCommand.
            - N049_get_bgp_state_ipv4
              Retrieve BGP IPv4 session state.
            - N050_get_bgp_state_ipv6
              Retrieve BGP IPv6 session state.
            - N051_get_isis_session_results
              Retrieve ISIS session results (IsisRouterResults).
            - N052_create_device_bgp_ipv6_routes
              Two IPv6 eBGP devices + BgpIpv6RouteConfig configuration.
            - N053_create_device_bgp_ipv4_bound_stream
              eBGP IPv4 device + bound stream configuration (with UsesIf).

        (4) Benchmark Test Code Examples (1):
            - N001_create_rfc2544_throughput
              RFC 2544 throughput test (two devices + binary search auto-run).

        (5) TC Code Blocks (7):
            Trigger by typing `#tc_block_`, or select the TC Code Block category
            from the `Ctrl+Shift+I` menu. Code blocks are not part of the N0xx
            numbering sequence.
            - tc_block_init
              StcPython import initialization with environment setup instructions.
            - tc_block_project_ports
              Project + two ports + AttachPorts framework block.
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
    The helper encapsulates 17 core methods of the Viavi TestCenter API. Typing
    `tc.` in a Python context instantly generates the standard method structure
    populated with placeholders:
    - apply              Commits and applies current test configuration to chassis.
    - config             Sets or modifies one or more object attributes/relations.
    - connect            Establishes connection to a Viavi TestCenter chassis.
    - create             Creates a specified automation object (e.g., StreamBlock).
    - delete             Deletes specified object handle from the test config.
    - disconnect         Terminates connection with a Viavi TestCenter chassis.
    - get                Retrieves attribute values, read-only data, or handles.
    - help / help_list   Queries data model and API commands for help info.
    - log                Writes diagnostic messages with severity levels to logs.
    - perform            Executes a Viavi TestCenter Command (e.g., AttachPorts).
    - reserve / release  Reserves or releases a physical port group (Port List).
    - sleep              Suspends execution of the current script (in seconds).
    - subscribe          Subscribes to and enables real-time results collection.
    - unsubscribe        Removes or cancels an established result subscription.
    - waitUntilComplete  Blocks execution until asynchronous commands complete.

3.3 Static Schema & Context Inference Engine
    Addressing the weakly-typed nature of the underlying API, the helper
    applies a static AST (Abstract Syntax Tree) type-deduction engine to
    eliminate property name conflicts across different objects:
    - Creation Inference: If you type `tc.config(hPortTx, )`, the helper traces
      back to find `hPortTx = tc.create("port", ...)`. It locks `hPortTx` as a
      `port` entity and restricts completion hints to its exclusive writable
      properties (e.g., UseDefaultHost=).
    - Retrieval Inference: Supports child object relation deduction. If
      a handle is retrieved via a relation like `hGenerator = tc.get(hPort,
      "children-Generator")`, the helper correctly recognizes it as a `Generator`
      entity in subsequent calls, displaying correct counters and properties.
    - Multi-line Call Recognition (New): When an argument list is broken across
      multiple lines — whether with a line-continuation backslash `\` or simply
      inside an unclosed parenthesis — the helper still correctly locates the
      enclosing call and object type, so hover and auto-completion no longer
      degrade into "guesswork." This fixes an issue where attribute descriptions
      from unrelated objects could bleed into multi-line calls.

3.4 Intelligent Auto-Completion
    When the helper detects a syntax context containing a `tc.` call, it
    automatically filters and provides precise candidate suggestions:
    - Object Type Hints: Inside `tc.create("`, it triggers autocomplete for
      all Viavi TestCenter object classes like StreamBlock, BgpRouterConfig, etc.
    - Command Hints: Inside `tc.perform("`, it populates available system
      commands with official Markdown descriptions (e.g., AttachPortsCommand).
    - Subscribe Parameter Hints (New): Inside `tc.subscribe(...)`, it
      auto-completes the fixed parameter names Parent, ResultType, ConfigType,
      FilenamePrefix, ResultParent, Interval, ViewAttributeList, and ViewName,
      correctly popping up the next suggestion after a comma.
    - Auto-Import Insertion: The first time a `tc.` method is autocompleted,
      the helper silently prepends standard import statements at the top line:
      from StcPython import StcPython
      tc = StcPython()

3.5 Structured Hover Documentation (Hover Provider)
    Hovering over Viavi TestCenter methods, object classes, attributes, or
    commands opens a polished Markdown window. Each document undergoes precise
    field extraction:
    - Hierarchy & Rules: Features a clean, unified, card-style visual layout.
    - Metadata Row: Extracts explicit fields for Type (e.g., bool, handle)
      and Default values, alongside valid enum values and Deprecated flags.
    - Descriptions: Strips residual punctuation from raw data to offer clean,
      official descriptions.
    - Lookup Performance (New): The hover fallback lookup was switched from a
      linear scan of all object types to a prebuilt index (O(1)), improving
      responsiveness on large schemas.


4. Protocol & Results Object Support Range
------------------------------------------
The underlying data of the helper fully covers the fields below:
- Routing Protocols: BGP, OSPFv2/v3, IS-IS.
- Access & Auth Protocols: DHCPv4/v6, 802.1X Dot1x, PPPoE.
- Multicast & Time Sync: IGMP, MLD, IEEE 802.1AS / gPTP.
- Layer 2 Protocols: STP / RSTP / MSTP, VLAN.
- RoCEv2.
- RFC 2544: Full four-test coverage — Throughput, Latency, Frame Loss, and Back-to-Back.
- Traffic Models: Raw StreamBlocks (IPv4/IPv6/VLAN/TCP/UDP/DSCP + capture),
  Bound StreamBlocks (IPv4/IPv6, bidirectional, port load config).
- Results Objects: Port-level, Stream-level, and Protocol Session-level.


5. Code Example / Code Block Usage & Workflow
---------------------------------------------

5.1 Using Code Examples and Code Blocks
    There are three ways to insert a code example or code block into your Python script:

    5.1.1 Method 1 — Type `#` to trigger inline completion (Recommended)
        1. In any `.py` file, type `#` at the start of a line.
        2. The editor immediately shows all available code examples and code blocks
           as a completion list.
        3. Continue typing a keyword to filter (e.g. `#raw_stream` for Raw stream
           code examples, `#create_bgp` for the BGP device example,
           `#tc_block_` for code blocks).
        4. Select the desired entry and press `Enter` or `Tab` to insert —
           the `#` character is automatically replaced by the full code snippet.
        5. Navigate placeholders with `Tab` / `Shift+Tab`.

    5.1.2 Method 2 — Type the full prefix and press Tab
        1. In any `.py` file, type the complete code example prefix name
           (e.g. `N027_config_raw_stream_fixed_frame_ttl`).
        2. Press `Tab` — the prefix expands into a complete, runnable code snippet.
        3. The cursor jumps to the first placeholder. Enter the required value
           (e.g. chassis IP).
        4. Press `Tab` to advance to the next placeholder; press `Shift+Tab` to go back.
        5. Continue until all placeholders are filled, then run the completed script.

    5.1.3 Method 3 — Hierarchical picker (Ctrl+Shift+I)
        1. Place your cursor at the target insertion point in a `.py` file.
        2. Press `Ctrl+Shift+I` (or open the Command Palette and run
           `TC: Insert Code Template`).
        3. Select a category from the first list (code example count shown on the right).
        4. Select a specific code example or code block from the second list.
        5. The full snippet is inserted — use `Tab` / `Shift+Tab` to navigate placeholders.

    5.1.4 Placeholder Navigation Keys
        - Tab          Move to the next placeholder
        - Shift+Tab    Move to the previous placeholder
        - Escape       Exit placeholder mode (retains current values)

    5.1.5 Example — `N036_config_raw_stream_ipv4` placeholder order
        1. szChassisIp     — TestCenter chassis IP address, default: 192.168.0.100
        2. iTxSlot         — Tx port slot number, default: 1
        3. iTxPort         — Tx port number, default: 1
        4. iRxSlot         — Rx port slot number, default: 1
        5. iRxPort         — Rx port number, default: 2
        6. szMacAddrPortA  — Source MAC address (Port A), default: 22:22:22:22:22:25
        7. szMacAddrPortB  — Destination MAC address (Port B), default: 22:22:22:22:22:22
        8. txIpAddr        — Source IP address, default: 20.0.0.2
        9. rxIpAddr        — Destination IP address, default: 30.0.0.2

5.2 Basic Code Workflow
    A typical script-authoring flow inside a `.py` file:

    from StcPython import StcPython
    tc = StcPython()

    # 1. Option A: Press 'Ctrl+Shift+I' inside a Python file to visually pick a framework.
    #    Option B: Autocomplete triggers candidate object types. Select "Project".
    hProject = tc.create("Project", under="system1")

    # 2. Define the port handles
    hPortTx = tc.create("port", under=hProject, location="//192.168.1.10/1/1")

    # 3. Context inference locks 'hPortTx' as a 'port' object type.
    # Writable port attributes pop up instantly with auto-appended equals signs.
    tc.config(hPortTx, UseDefaultHost="False")

    # 4. Command autocomplete: pull commands and complete internal parameters.
    tc.perform("AttachPortsCommand", PortList=hPortTx, AutoConnect=True)


6. Support, Enhancements & Continuous Roadmap
---------------------------------------------

6.1 Continuous Updates & Evolution
    The helper is under ongoing maintenance. Future releases will update the
    data schema dictionary to align with new Viavi TestCenter software versions,
    add deeper semantic analysis, and extend the built-in code example and code
    block library to cover a broader range of testing workflows.

6.2 Technical Support & Feedback Contact
    Your feedback is vital to improving the helper. If you encounter any bugs,
    require technical assistance, or wish to suggest features/enhancements,
    please reach out to our support desk:

    - Support Email: HSESupportBJ@viavisolutions.com

    Please feel free to contact us regarding:
    - Bug Reports & Troubleshooting: Autocomplete, hover, or syntax issues.
    - Feature Requests & Enhancements: Structural additions or improvements.
    - New Code Example/Protocol Submissions: Desired test workflows or code examples
      to be supported in subsequent releases.


7. Important Notes & Environment Prerequisites
----------------------------------------------

7.1 Lazy Activation Mechanism
    To maintain a lightweight environment, the helper uses a lazy-loading
    architecture. It activates and loads the schema dictionary *only* when an
    actual Python file ending in `.py` is opened, ensuring zero idle memory
    consumption during regular coding sessions.

7.2 Prerequisites
    - The helper functions strictly as a front-end syntax assistant. The local
      or remote development environment must have the official Viavi TestCenter
      application installed (to satisfy runtime dynamic-link dependencies).


8. Changes in This Version (2.0.4) Relative to 2.0.3
-----------------------------------------------------

8.1 Added
    - Added a unified sequence-number prefix (`N001`–`N056`) to every code
      example except TC Code Blocks, making it easy to tell code examples apart
      by source when multiple Viavi TestCenter API extensions (e.g. the Native
      API and REST API editions) are installed side by side — `#` completion no
      longer gets confused by duplicate prefixes.
    - Added a dedicated `Benchmark Test` category (currently 1 code example:
      `N001_create_rfc2544_throughput`).
    - Added fixed-parameter auto-completion and hover documentation for
      `tc.subscribe(...)`: `Parent`, `ResultType`, `ConfigType`,
      `FilenamePrefix`, `ResultParent`, `Interval`, `ViewAttributeList`,
      `ViewName`.

8.2 Changed
    - The instance-variable naming convention was changed from `stc` to `tc`
      company-wide (removing the Spirent-derived `s` prefix), affecting code
      examples, code blocks, documentation, and the auto-inserted import
      statement; the `StcPython` class name and its import statement are
      unchanged.
    - Data files renamed: `stc_schema.json` → `tc_schema.json`,
      `stc_snippets.json` → `tc_snippets.json`.
    - The code example / code block category picker (`Ctrl+Shift+I`) now
      groups items by the explicit `category` field instead of guessing from
      the prefix string; added an "Other Templates" fallback group so that a
      missing or misspelled `category` no longer makes an example disappear
      from the list.

8.3 Fixed
    - Fixed hover and auto-completion failing to correctly infer the enclosing
      object type for multi-line calls, which previously caused attribute
      descriptions from different objects to be confused with one another.
    - Fixed a possible full activation failure when `tc_schema.json` is missing.
    - Fixed `tc.subscribe(...)` parameter completion not popping up the next
      suggestion after typing a comma.

8.4 Performance
    - The hover fallback lookup was switched from a linear scan of all object
      types to a prebuilt index lookup, improving responsiveness on large schemas.
    - The import-statement detection scan was bounded to the first several
      lines of the document instead of scanning the entire file, reducing
      overhead on large files.
