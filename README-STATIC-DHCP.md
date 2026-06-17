# Always Resolve Static DHCP Hostnames

This feature automatically synchronizes static DHCP configurations with the internal DNS resolver, ensuring that all statically defined DHCP hosts are resolvable by name regardless of their online status.

## Changes

### Web UI Implementation
- **Zero-Clutter Resolution**: Synchronization now uses `address=` directives in `misc.dnsmasq_lines`. This ensures hostnames (including FQDNs) resolve correctly while keeping the **Local DNS Records** list clean for your manual entries.
- **Automatic FQDN Support**: The Web UI automatically detects your configured DNS domain and adds the appropriate suffix to resolution rules.
- **Smart Management**: Synced records are internally tagged with `# from-dhcp` for automatic management.
- **Invisible Persistence**: The synchronization preference is stored using a valid dnsmasq marker (`id:pihole-dhcp-sync,ignore`), which is automatically hidden from the DHCP configuration UI.

### CLI Implementation
- **New Commands**:
  - `pihole adddhcphostname <mac> <ip> <hostname>`: Adds a static entry to `/etc/pihole/hosts/static-dhcp.list`.
  - `pihole removedhcphostname <mac>`: Reliably removes the entry.
- **Standardized Format**: Uses the industry-standard `IP FQDN Shortname` format for maximum compatibility.
- **Automatic Integration**: Ensures `/etc/dnsmasq.d/99-pihole-static-dhcp.conf` exists to link the static file to the DNS engine.
