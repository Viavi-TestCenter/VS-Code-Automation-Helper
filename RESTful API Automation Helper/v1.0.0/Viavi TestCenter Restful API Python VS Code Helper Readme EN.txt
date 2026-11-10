================================================================================
Viavi TestCenter Restful API Python VS Code Helper — User Guide
Version: 1.0.0
Release Date: 2026-08-11
================================================================================

1. Overview
-----------

1.1 Introduction
    Viavi TestCenter Restful API Python VS Code Helper is an extension designed
    for automating scripts with the Viavi TestCenter Restful API. Based on the
    stcrestclient HTTP protocol library, it deeply parses the REST data schema
    to reduce the lookup overhead inherent in weakly-typed HTTP interfaces,
    improving script delivery quality and protocol simulation development
    efficiency across all major VS Code-based editors.

1.2 Feature Summary
    - Interactive code example manager — 36 examples, one-click insertion.
    - 20 core API methods — type `tc.` to instantly generate a method skeleton.
    - Context inference engine — automatically infers handle types.
    - Intelligent autocomplete — precise object type and command suggestions.
    - Structured hover documentation — clean Markdown with Type / Default /
      enum values.

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
    The installation procedure is identical across all VS Code-based editors:
    1. Open the editor and go to the Extensions panel (Ctrl+Shift+X).
    2. Click the More Actions icon (···) in the top-right corner.
    3. Select "Install from VSIX..." from the dropdown menu.
    4. Browse to and select the target .vsix file, click Install, then restart
       the editor.

2.2 Updating / Uninstalling
    To upgrade to a new version or perform a clean reinstall:
    1. Open the Extensions panel (Ctrl+Shift+X) and locate
       Viavi TestCenter Restful API Python VS Code Helper.
    2. Click the gear icon (⚙) → Uninstall, then restart the editor.
    3. Follow steps 1–4 in section 2.1 above to install the new .vsix file.

    Note: Some editors support installing a new VSIX directly over an existing
    version, replacing it automatically without a manual uninstall.


3. Features and Capabilities
-----------------------------

3.1 Built-in Code Examples and Interactive Example Manager
    This version includes 36 ready-to-use code examples with three insertion
    workflows available in any Python file.

    3.1.1 Three Insertion Methods
        - [Workflow A] Inline trigger: In any .py file, type # at the start of
          a line. The editor immediately pops up the full example list.
          Continue typing a prefix keyword (e.g. #raw_stream or #create_bgp)
          to filter in real time, then press Enter or Tab to insert — the #
          character is automatically replaced by the generated code.
        - [Workflow B] Full prefix + Tab: Type the complete prefix name (e.g.
          raw_stream_fixed_frame_ipv4_ttl), then press Tab to expand.
        - [Workflow C] Interactive example menu (recommended): Press
          Ctrl+Shift+I to open a two-level Quick Pick — select a category,
          then select an example, and the code snippet is inserted at the
          cursor:

                Category                                 Count
                Raw StreamBlock Examples                   12
                Bound StreamBlock Examples                   6
                Emulated Device Examples                    18

        See section 5.1 for a full step-by-step walkthrough.

    3.1.2 Available Example Prefixes
        Type # followed by the prefix name to trigger. The prefix names shown
        below are the exact names displayed in the completion popup (without #).

        (1) Raw Stream Examples (12):
            - raw_stream_ipv4_send_collect_port_results
              End-to-end Raw IPv4 stream + port-level Tx/Rx result subscription.
            - raw_stream_auto_frame_with_sig
              Auto frame length + insert signature field.
            - raw_stream_prbs_fill_with_fcs_error
              PRBS fill + FCS error injection.
            - raw_stream_fixed_frame_ipv4_ttl
              Fixed frame length + TTL adjustment.
            - raw_stream_incr_frame_no_sig
              Incrementing frame length + no-signature mode.
            - raw_stream_random_frame_constant_fill
              Random frame length + constant fill.
            - raw_stream_bidir_collect_txrx_results
              Bidirectional stream + dual-port Tx/Rx statistics.
            - raw_stream_ipv4_tcp_header
              Raw TCP stream with EthernetII + IPv4 + TCP header.
            - raw_stream_ipv4_udp_header
              Raw UDP stream with EthernetII + IPv4 + UDP header.
            - raw_stream_ipv6_basic
              Raw IPv6 stream with EthernetII + IPv6 + port stats and capture.
            - raw_stream_ipv4_with_vlan
              Raw stream with EthernetII + VLAN + IPv4 + port stats and capture.
            - raw_stream_capture_save
              Raw stream transmission + port capture saved as PCAP file.

        (2) Bound Stream Examples — StreamBlocks bound to emulated devices (6):
            - bound_stream_fixed_frame_two_devices
              Fixed frame length bound stream between two devices.
            - bound_stream_pair_incr_frame
              Incrementing frame length bound stream between a device pair.
            - bound_stream_auto_frame
              Auto frame length bound stream.
            - bound_stream_port_based_load
              Bound stream with port-based load distribution.
            - bound_stream_random_frame_bidir
              Random frame length bidirectional bound stream.
            - bound_stream_ipv6_two_devices
              Bound stream between two IPv6 devices (global + link-local).

        (3) Emulated Device Examples — protocol stacks (18):
            - create_ipv4_device
              Basic static IPv4 emulated device configuration.
            - create_l2_ethernet_device_no_ipv4
              Layer-2 only MAC emulated device (no IPv4).
            - create_bgp_ipv4_two_devices_with_routes
              IPv4 BGP two-device setup + route block configuration.
            - create_dhcpv4_server_client_with_traffic
              Complete DHCPv4 Server + Client emulation with traffic.
            - create_ospfv2_two_devices_lsa
              OSPFv2 two devices + LSA topology generator.
            - create_isis_ipv4_two_devices_lsp
              IS-IS Level-2 IPv4 two devices + LSP topology.
            - create_device_group_with_ip_mac_step
              Multi-device group with IP / MAC / gateway step configuration.
            - create_three_devices_one_port
              Three named emulated devices bound to the same port.
            - create_device_ping_with_routerid
              Device with EnablePingResponse=TRUE and RouterId configured.
            - create_device_no_ping_with_prefix_length
              Device with EnablePingResponse=FALSE and PrefixLength configured.
            - create_ipv6_device_basic
              Two devices with full global IPv6 + link-local IPv6 interface stack.
            - create_device_with_vlan
              Two devices with VLAN interface (VlanIf stacked on EthIIIf).
            - create_device_with_vlan_with_stream
              Two VLAN devices + IPv4 over VlanIf bound stream.
            - create_igmp_host_two_devices_with_stream
              IGMP host two-device multicast group subscription + multicast stream.
            - create_gptp_clock_two_devices
              gPTP (IEEE 802.1AS-2020) two-device clock emulation + result
              subscription.
            - create_dot1x_eap_md5
              802.1X Dot1x Supplicant + EAP-MD5 authentication configuration.
            - create_pppoe_client_server_two_devices
              PPPoE client + server two-device setup with full PPPoE/PPP stack.
            - create_bridge_port_config_two_devices
              Two devices + BridgePortConfig (STP bridge port priority emulation).

3.2 Core API Methods
    This extension covers 20 core methods of the Viavi TestCenter REST API.
    Type the instance variable name followed by . (e.g. tc.) in a Python
    context to instantly generate a standard method structure with placeholders:
    - apply              Commit and apply the current test configuration to the
                         chassis.
    - config             Set or modify one or more object attributes or
                         relations.
    - connect            Connect to a Viavi TestCenter chassis.
    - create             Create an automation object under the specified parent
                         (e.g. StreamBlock).
    - delete             Delete the specified object handle.
    - disconnect         Disconnect from a Viavi TestCenter chassis.
    - download           Download and save a specified file from the Lab Server.
    - download_all       Download all files from the Lab Server.
    - end_session        End the test session (optionally terminate the
                         server-side session).
    - files              Get the list of available files on the Lab Server.
    - get                Retrieve attribute values, read-only data, or handles.
    - help               Query help information for the data model and API
                         commands.
    - join               Join an existing test session on the Lab Server.
    - log                Write a diagnostic message with severity level to the
                         log.
    - new_session        Create and join a new test session on the Lab Server.
    - perform            Execute a Viavi TestCenter command (including port
                         reserve/release, result subscription, etc.).
    - set_timeout        Set the response wait timeout in seconds (0 = no
                         timeout).
    - system_info        Retrieve system information from the Lab Server.
    - upload             Upload a configuration file or other file to the Lab
                         Server.
    - wait_until_complete Block execution until an asynchronous Sequencer
                         command completes.

    Note: In the REST API, port reserve/release is performed via
    tc.perform("reservePort"/"releasePort") and result subscription via
    tc.perform("ResultsSubscribe").

3.3 Static Model and Context Type Inference Engine
    To address the weakly-typed nature of the REST API, this extension uses a
    static AST (Abstract Syntax Tree) type inference engine to eliminate
    attribute name collisions between different objects:
    - Creation inference: When you type tc.config(hPortTx, ), the extension
      traces back to find hPortTx = tc.create("Port", ...), locks hPortTx to
      the Port entity, and restricts completion to its writable attributes
      (e.g. useDefaultHost=).
    - Retrieval inference: Supports inference from child object relationships.
      If a handle is obtained via a relation such as
      hGenerator = tc.get(hPort, "children-Generator"), the extension correctly
      identifies it as a Generator entity in subsequent calls and displays the
      corresponding counters and attributes.

    Note: The extension automatically identifies all stchttp.StcHttp instance
    variable names in the document (e.g. tc, stc) and uses them to trigger
    the completion and inference logic above.

3.4 Intelligent Autocomplete
    The extension automatically scans the document, identifies all StcHttp
    instance variable names in the current file, and filters candidate
    suggestions when it detects a method call on those variables:
    - Object type suggestions: Inside tc.create("..."), autocomplete triggers
      for all Viavi TestCenter object types (StreamBlock, BgpRouterConfig, etc.)
    - Command suggestions: Inside tc.perform("..."), available system commands
      are listed with official Markdown descriptions (e.g. AttachPortsCommand).
    - Attribute suggestions: Inside tc.config(handle, ...) or
      tc.create("Type", parent, ...), the context inference engine locks the
      object type and presents its writable attributes with Type / Default info.

3.5 Structured Hover Documentation
    Hovering over a Viavi TestCenter method, object class, attribute, or command
    displays a Markdown card. Each card is built from precise field extraction:
    - Hierarchy and layout: Clean, consistent card-style visual structure.
    - Metadata row: Explicitly extracted Type (e.g. bool, handle) and Default
      value fields, with valid enum values and Deprecated markers.
    - Description: Official description with residual punctuation stripped for
      clean display.


4. Supported Protocols
-----------------------
The extension's underlying data model fully covers the following protocols:
- Routing Protocols: BGP, OSPFv2/v3, IS-IS.
- Access & Authentication: DHCPv4/v6, 802.1X Dot1x, PPPoE.
- Multicast & Time Sync: IGMP, PTP / gPTP.
- Layer 2 Protocols: STP, VLAN.
- Traffic Models: Raw StreamBlock, Bound StreamBlock.
- Result Objects: Port-level, stream-level, and protocol session-level.


5. Example Usage and Code Walkthrough
--------------------------------------

5.1 Inserting a Code Example
    There are three ways to insert an example into your Python script:

    5.1.1 Method A — Type # to trigger inline completion (Recommended)
        1. In any .py file, type # at the start of a line.
        2. The editor immediately shows all available examples as inline
           completion items.
        3. Continue typing keywords to filter (e.g. #raw_stream for Raw stream
           examples, #create_bgp for BGP device examples).
        4. Select the desired example and press Enter or Tab to insert — the #
           character is automatically replaced by the full code snippet.
        5. Navigate through placeholders using Tab / Shift+Tab.

    5.1.2 Method B — Type the full prefix and press Tab
        1. In any .py file, type the complete example prefix name
           (e.g. raw_stream_ipv4_send_collect_port_results).
        2. Press Tab — the prefix expands into a complete, runnable snippet.
        3. The cursor jumps to the first placeholder. Enter the required value
           (e.g. the Lab Server IP address).
        4. Press Tab to advance to the next placeholder; Shift+Tab to go back.
        5. Once all placeholders are filled, the script is ready to run.

    5.1.3 Method C — Hierarchical selector (Ctrl+Shift+I)
        1. Place the cursor at the target insertion point in a .py file.
        2. Press Ctrl+Shift+I (or open the Command Palette and run
           TC: Insert Code Template).
        3. Pick a category from the first list (example count shown on the
           right).
        4. Pick a specific example from the second list (prefix and description
           shown).
        5. The full snippet is inserted — use Tab / Shift+Tab to navigate
           placeholders.

    5.1.4 Placeholder Navigation Keys
        - Tab          Jump to the next placeholder
        - Shift+Tab    Return to the previous placeholder
        - Escape       Exit placeholder mode (keep the current value)

    5.1.5 Example — Placeholder Order for
          raw_stream_ipv4_send_collect_port_results
        1. server_ip  — Lab Server IP address (REST API server, e.g.
                        192.168.0.200)
        2. user       — Session user name label (e.g. JoeUser)
        3. session    — Session name (e.g. ExampleTest)
        4. chassis_ip — TestCenter chassis IP address
        5. tx_slot    — Tx port slot number
        6. tx_port    — Tx port number
        7. rx_slot    — Rx port slot number
        8. rx_port    — Rx port number
        9. src_mac    — Source MAC address (Port A), default: 22:22:22:22:22:25
        10. dst_mac   — Destination MAC address (Port B), default:
                        22:22:22:22:22:22
        11. src_ip    — Source IP address, default: 20.0.0.2
        12. dst_ip    — Destination IP address, default: 30.0.0.2

5.2 Basic Code Workflow
    A typical scripting session in a .py file:

    from stcrestclient import stchttp

    # Connect to Lab Server and create a session
    tc = stchttp.StcHttp("192.168.0.200")
    tc.new_session("JoeUser", "ExampleTest")

    # 1. Method A: Press Ctrl+Shift+I in a Python file to visually pick an
    #    example skeleton.
    #    Method B: Autocomplete triggers candidate object types — select
    #    "Project".
    hProject = tc.create("Project")

    # 2. Define port handles (parent is a positional argument, not under=).
    hPortTx = tc.create("Port", hProject,
                         location="//192.168.0.100/1/1",
                         useDefaultHost="False")

    # 3. Context inference locks 'hPortTx' to the 'Port' object type.
    #    Writable port attributes appear instantly with '=' appended.
    tc.config(hPortTx, useDefaultHost="False")

    # 4. Command autocomplete: pulls commands and completes internal parameters.
    tc.perform("AttachPortsCommand", autoConnect="TRUE")

    # 5. Disconnect the chassis and terminate the server-side session when done.
    tc.disconnect("192.168.0.100")
    tc.end_session(end_tcsession=True)


6. Support, Enhancements, and Roadmap
---------------------------------------

6.1 Ongoing Development
    This extension is under active maintenance. Future versions will update the
    data model dictionary to align with new Viavi TestCenter software releases,
    introduce deeper semantic analysis, and expand the built-in example library
    to cover a wider range of test workflows.

6.2 Technical Support and Feedback
    Your feedback is essential for improving this extension. For bug reports,
    technical assistance, or feature requests, please contact the support team:

    - Support email: HSESupportBJ@viavisolutions.com

    We welcome inquiries on:
    - Bug reports & troubleshooting — issues with autocomplete, hover, or syntax
      behavior.
    - Feature requests & enhancements — structural additions or improvement
      suggestions.
    - New example / protocol submissions — test workflows or examples you would
      like supported in future versions.


7. Important Notes and Prerequisites
--------------------------------------

7.1 Lazy-Loading Activation
    To keep the environment lightweight, this extension uses a lazy-loading
    architecture. It activates and loads the model dictionary only when a Python
    file ending in .py is actually opened, ensuring zero idle memory usage
    during normal coding sessions.

7.2 Prerequisites
    - This extension runs as a front-end syntax assistant — no local TestCenter
      application installation is required.
    - The stcrestclient Python library must be installed
      (pip install stcrestclient) with access to a Viavi TestCenter Lab Server
      in order to execute scripts.
    - Each Python script must include the following import statement. The
      extension identifies StcHttp instances from this import to activate
      autocomplete and hover documentation:
          from stcrestclient import stchttp
    - This extension provides editing-time intelligence and example insertion
      only. Runtime HTTP communication is handled by the stcrestclient library.
