# Mobile Broadband and VPN Connections

## 1. Mobile Broadband

Mobile broadband connections — USB cellular modems or tethered mobile devices — are also managed through Network Manager. When a mobile broadband device is connected, Network Manager detects it and launches a setup wizard that guides through selecting a carrier and entering the connection details. Once configured, the connection profile is saved, and the connection is established automatically each time the device is attached.

## 2. VPN Connections

Network Manager supports the most widely used VPN protocols in enterprise and personal use:

| Protocol | Notes |
| :--- | :--- |
| **OpenVPN** | The most widely deployed open-source VPN solution |
| **IPSec** | The standard protocol suite for encrypted IP communications, used extensively in enterprise environments |
| **Cisco OpenConnect** | Compatible with both the official Cisco AnyConnect client and the open-source equivalent |
| **Microsoft PPTP** | For compatibility with older Windows-based VPN infrastructure |
| **WireGuard** | A modern, high-performance VPN protocol |

> [!NOTE]
> Unlike other VPNs, WireGuard support is baked directly into the Linux kernel (since version 5.6), offering significantly better performance since it avoids jumping between "user space" and "kernel space."

### VPN Plugins

VPN support in Network Manager is provided through protocol-specific plugins, which may not be installed by default on every distribution. If a required VPN type doesn't appear as an option when adding a new connection, check the distribution's software repositories for the appropriate plugin — for example:

| Distribution | Package Name |
| :--- | :--- |
| Ubuntu | `network-manager-openvpn` |
| Fedora | `NetworkManager-openvpn` |

### Adding a VPN Connection

1. Go to **Settings → Network**, scroll to the **VPN** section, and click **+**.
2. Select the VPN type from the list.
3. Enter the connection details provided by the VPN service or administrator, and save the profile.

The VPN can then be toggled on and off from the system menu in the top bar. In recent GNOME versions (43+), this is found in the **Quick Settings** panel (the pill-shaped buttons in the top right), where selecting the VPN icon connects or disconnects it.
