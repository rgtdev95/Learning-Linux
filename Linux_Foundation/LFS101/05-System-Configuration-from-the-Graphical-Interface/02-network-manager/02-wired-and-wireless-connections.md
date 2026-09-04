# Wired and Wireless Connections

## 1. Wired Connections

Wired Ethernet connections are the simplest to manage and typically require no manual setup. Plugging in a network cable causes Network Manager to detect the connection automatically and configure it using **DHCP** (Dynamic Host Configuration Protocol) — the standard mechanism by which a router or network server automatically assigns a machine's IP address, subnet mask, default gateway, and DNS server settings.

> [!NOTE]
> This is exactly how wired connections work on Windows and macOS as well.

### Static IP Configuration

On a network that requires a fixed (static) IP address rather than one assigned automatically, Network Manager supports manual configuration:

1. Open **Settings → Network**.
2. Locate the wired connection and click the **gear icon** next to it.
3. In the **IPv4** and **IPv6** tabs, switch from **Automatic (DHCP)** to **Manual** and enter the specific IP address, subnet mask, gateway, and DNS server.

### Viewing or Changing the MAC Address

The same connection settings panel also shows the **MAC address** of the network interface, and lets it be changed if the hardware supports it. A MAC address is a unique identifier assigned to every network card, expressed as a 12-character hexadecimal value (e.g., `00:1A:2B:3C:4D:5E`), used by routers and switches to identify devices on the local network.

> [!NOTE]
> Changing the MAC address is occasionally useful for troubleshooting, or in environments that control network access based on MAC addresses.

## 2. Wireless Connections

Wireless networks are usually not connected by default. Network Manager can:

- View the list of available wireless networks, and which one (if any) is currently connected.
- Add, edit, or remove known wireless networks.
- Specify which networks should connect automatically when present.

Wi-Fi connections require a brief manual step the first time a new network is joined, but are managed automatically after that.

### Connecting to a Wireless Network

1. **Open the Wi-Fi menu** — select the system menu in the upper-right corner of the top bar to open the quick-access panel showing current connection status. Expand the **Wi-Fi** section to see a list of available networks in range, each showing its name (SSID) and signal strength. If Wi-Fi hardware is present but disabled, a toggle at the top of the panel turns it on.
2. **Select a network** — an open network connects immediately. A password-protected network (shown with a padlock icon) prompts for its password; enter it and click **Connect**.
3. **Automatic reconnection** — by default, the password is saved to the system keyring and the network is added to the list of known connections, so the machine reconnects automatically whenever that network is in range, without prompting again.

### Detailed Wi-Fi Settings

To view or modify a connected or saved network in more detail, select **Wi-Fi Settings** at the bottom of the Wi-Fi panel, or navigate to **Settings → Wi-Fi**. Selecting the gear icon next to any connection allows you to:

- View connection details — IP address, DNS server, MAC address.
- Switch from automatic (DHCP) to a manually configured static IP address, for both IPv4 and IPv6.
- Set whether the connection connects automatically when in range.
- **Forget** the network, removing the saved password and connection profile.
