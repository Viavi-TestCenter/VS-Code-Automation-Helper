================================================================================
Viavi TestCenter Native Python API VS Code Helper Readme
Version: 2.0.3
Release Date: 2026-09-21
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
    - Built-in Code Examples & Code Blocks — 38 code examples + 7 code blocks, one-click insertion.
    - 17 Core API Methods — instant `stc.` method scaffolding.
    - Context Inference Engine — automatic handle-type deduction.
    - Intelligent Auto-Completion — object types, commands, and auto-import.
    - Structured Hover Documentation — clean Markdown with Type / Default / enum.

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
    This version includes 38 code examples and 7 code blocks, supporting three rapid
    deployment workflows within Python files.

    3.1.1 Three Ways to Insert
        - [Workflow A] Inline Trigger: type `#` at the start of a line in any
          `.py` file — the editor immediately pops up the full template/example list.
          Continue typing a prefix keyword (e.g. `#raw_stream` or `#create_bgp`)
          to filter in real time, then press `Enter` or `Tab` to insert; the `#`
          character is automatically replaced by the generated code.
        - [Workflow B] Full Prefix + Tab: type the complete prefix name
          (e.g. `raw_stream_fixed_frame_ipv4_ttl`) then press `Tab` to expand.
        - [Workflow C] Interactive Code Example Menu (Recommended): press
          `Ctrl+Shift+I` to open a two-level Quick Pick UI — pick a category,
          then a code example, and the snippet drops in at the cursor:

                Category                                Count
                Raw StreamBlock Code Examples              12
                Bound StreamBlock Code Examples             6
                Emulated Device Code Examples              20

        Full step-by-step instructions are in section 5.1.

    3.1.2 Available Code Example Prefixes
        Trigger by typing `#` followed by the prefix name. The prefix name
        shown below is what appears in the completion popup (no `#` displayed).

        (1) Raw Traffic Code Examples (12):
            - raw_stream_ipv4_send_collect_port_results
              End-to-end Raw IPv4 stream + port-level Tx/Rx result subscription.
            - raw_stream_auto_frame_with_sig
              Auto frame length + insert signature field.
            - raw_stream_prbs_fill_with_fcs_error
              PRBS payload + FCS error insertion.
            - raw_stream_fixed_frame_ipv4_ttl
              Fixed frame length + TTL adjustments.
            - raw_stream_incr_frame_no_sig
              Incrementing frame length + no-signature mode.
            - raw_stream_random_frame_constant_fill
              Random frame length + constant fill.
            - raw_stream_bidir_collect_txrx_results
              Bidirectional streams + dual-end Tx/Rx stats.
            - raw_stream_ipv4_tcp_header
              Raw TCP stream with EthernetII + IPv4 + TCP header.
            - raw_stream_ipv4_udp_header
              Raw UDP stream with EthernetII + IPv4 + UDP header.
            - raw_stream_ipv6_basic
              Raw IPv6 stream with EthernetII + IPv6 headers, port-level stats.
            - raw_stream_ipv4_with_vlan
              Raw stream with EthernetII + VLAN + IPv4 headers, port-level stats.
            - raw_stream_capture_save
              Raw stream transmission + port packet capture saved to PCAP file.
        (2) Bound Traffic Code Examples — StreamBlocks Bound to Emulated Devices (6):
            - bound_stream_fixed_frame_two_devices
              Fixed-frame bound stream between two devices.
            - bound_stream_pair_incr_frame
              Device-pair bound stream with incrementing frame length.
            - bound_stream_auto_frame
              Auto frame length bound stream.
            - bound_stream_port_based_load_config
              Port-load-based bound stream allocation.
            - bound_stream_random_frame_bidir
              Random frame length bidirectional bound stream.
            - bound_stream_ipv6_two_devices
              Bound stream between two IPv6 devices (global + link-local addresses).
        (3) Emulated Device Code Examples — Protocol Stacks (20):
            - create_ipv4_device_basic
              Basic static IPv4 emulated device setup.
            - create_l2_ethernet_device_no_ipv4
              Pure Layer-2 MAC emulated device (no IPv4).
            - create_bgp_ipv4_two_devices_with_routes
              IPv4 BGP dual-device + route block configuration.
            - create_dhcpv4_server_client_with_traffic
              DHCPv4 Server + Client full simulation with traffic.
            - create_ospfv2_two_devices_lsa_gen
              OSPFv2 two devices with LSA topology generator.
            - create_isis_ipv4_two_devices_lsp
              IS-IS Level-2 IPv4 two devices with LSP topology.
            - create_device_group_with_ip_mac_step
              Multi-device group with IP / MAC / GW step configuration.
            - create_three_devices_one_port
              Three named devices bound to one port.
            - create_device_ping_with_routerid
              Device with EnablePingResponse=TRUE and RouterId.
            - create_device_no_ping_with_prefix_length
              Device with EnablePingResponse=FALSE and PrefixLength.
            - create_ipv6_device_basic
              Two devices with global IPv6 + link-local IPv6 full interface stack.
            - create_device_with_vlan
              Two devices with VLAN interface (VlanIf stacked on EthIIIf).
            - create_device_with_vlan_with_stream
              Two VLAN devices + IPv4-over-VlanIf bound stream.
            - create_igmp_host_two_devices_with_stream
              IGMP host dual-device subscribed to same multicast group + bound stream.
            - create_gptp_clock_two_devices
              gPTP (IEEE 802.1AS-2020) clock dual-device + result subscription.
            - create_dot1x_eap_md5
              802.1X Dot1x Supplicant + EAP-MD5 authentication configuration.
            - create_pppoe_client_server_two_devices
              PPPoE Client + Server dual-device with full PPPoE/PPP interface stack.
            - create_stp_two_devices
              Two devices + BridgePortConfig (STP bridge port priority emulation).
            - create_rocev2_qp_two_ports
              RoCEv2 Queue Pair dual-port with PFC / ECN / CNP / VLAN and traffic binding.
            - create_rfc2544_throughput
              RFC 2544 throughput test with two devices and binary search auto-run.

        (4) TC Code Blocks (7):
            Trigger by typing `#tc_block_`, or select the TC Code Block category
            from the `Ctrl+Shift+I` menu.
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
    `stc.` in a Python context instantly generates the standard method structure
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
    - Creation Inference: If you type `stc.config(hPortTx, )`, the helper traces
      back to find `hPortTx = stc.create("port", ...)`. It locks `hPortTx` as a
      `port` entity and restricts completion hints to its exclusive writable
      properties (e.g., UseDefaultHost=).
    - Retrieval Inference: Added support for child object relation deduction. If
      a handle is retrieved via a relation like `hGenerator = stc.get(hPort,
      "children-Generator")`, the helper correctly recognizes it as a `Generator`
      entity in subsequent calls, displaying correct counters and properties.

3.4 Intelligent Auto-Completion
    When the helper detects a syntax context containing an `stc.` call, it
    automatically filters and provides precise candidate suggestions:
    - Object Type Hints: Inside `stc.create("`, it triggers autocomplete for
      all Viavi TestCenter object classes like StreamBlock, BgpRouterConfig, etc.
    - Command Hints: Inside `stc.perform("`, it populates available system
      commands with official Markdown descriptions (e.g., AttachPortsCommand).
    - Auto-Import Insertion: The first time an `stc.` method is autocompleted,
      the helper silently prepends standard import statements at the top line:
      from StcPython import StcPython
      stc = StcPython()

3.5 Structured Hover Documentation (Hover Provider)
    Hovering over Viavi TestCenter methods, object classes, attributes, or
    commands opens a polished Markdown window. Each document undergoes precise
    field extraction:
    - Hierarchy & Rules: Features a clean, unified, card-style visual layout.
    - Metadata Row: Extracts explicit fields for Type (e.g., bool, handle)
      and Default values, alongside valid enum values and Deprecated flags.
    - Descriptions: Strips residual punctuation from raw data to offer clean,
      official descriptions.


4. Protocol & Results Object Support Range
------------------------------------------
The underlying data of the helper fully covers the fields below:
- Routing Protocols: BGP, OSPFv2/v3, IS-IS.
- Access & Auth Protocols: DHCPv4/v6, 802.1X Dot1x, PPPoE.
- Multicast & Time Sync: IGMP, MLD, IEEE 802.1AS / gPTP.
- Layer 2 Protocols: STP / RSTP / MSTP, VLAN.
- RoCEv2.
- RFC 2544: Full four-test coverage — Throughput, Latency, Frame Loss, and Back-to-Back.
- Traffic Models: Raw StreamBlocks (IPv4/IPv6/VLAN/TCP/UDP + capture),
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
           (e.g. `raw_stream_ipv4_send_collect_port_results`).
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

    5.1.5 Example — `raw_stream_ipv4_send_collect_port_results` placeholder order
        1. chassis_ip  — TestCenter chassis IP address
        2. tx_slot     — Tx port slot number
        3. tx_port     — Tx port number
        4. rx_slot     — Rx port slot number
        5. rx_port     — Rx port number
        6. src_mac     — Source MAC address (Port A), default: 22:22:22:22:22:25
        7. dst_mac     — Destination MAC address (Port B), default: 22:22:22:22:22:22
        8. src_ip      — Source IP address, default: 20.0.0.2
        9. dst_ip      — Destination IP address, default: 30.0.0.2

5.2 Basic Code Workflow
    A typical script-authoring flow inside a `.py` file:

    from StcPython import StcPython
    stc = StcPython()

    # 1. Option A: Press 'Ctrl+Shift+I' inside a Python file to visually pick a framework.
    #    Option B: Autocomplete triggers candidate object types. Select "Project".
    hProject = stc.create("Project", under="system1")

    # 2. Define the port handles
    hPortTx = stc.create("port", under=hProject, location="//192.168.1.10/1/1")

    # 3. Context inference locks 'hPortTx' as a 'port' object type.
    # Writable port attributes pop up instantly with auto-appended equals signs.
    stc.config(hPortTx, UseDefaultHost="False")

    # 4. Command autocomplete: pull commands and complete internal parameters.
    stc.perform("AttachPortsCommand", PortList=hPortTx, AutoConnect=True)


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
