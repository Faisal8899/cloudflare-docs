---
pcx_content_type: concept
title: Pseudo IPv4
---

# Pseudo IPv4

Cloudflare customers can use **Pseudo IPv4** if their origin web server only understands IPv4 formatted IP addresses (meaning it would not support Cloudflare's default [IPv6 compatibility](/network/ipv6-compatibility/)).

## Availability

{{<feature-table id="network.pseudo_ipv4">}}

## Background

Some older origin server analytics and fraud detection software expect IP addresses in an IPv4 format and do not support IPv6 addresses.

**Pseudo IPv4** uses the [Class E IPv4 address space](https://tools.ietf.org/html/rfc1112#section-4) to provide as many unique IPv4 addresses corresponding to IPv6 addresses as possible.

-   Example Class E IPv4 address: `240.16.0.1`
-   Example IPv6 address: `2400:cb00:f00d:dead:beef:1111:2222:3333`

{{<Aside type="note">}}
Class E IPv4 addresses are designated as experimental and are not used
for production Internet traffic.
{{</Aside>}}

## Configure Pseudo IPv4

Cloudflare offers three options for configuring **Pseudo IPv4**:

-   **Off**: Default value.
-   **Add Header**: Cloudflare automatically adds the `Cf-Pseudo-IPv4` header with a Class E IPv4 address hashed from the original IPv6 address.
-   **Overwrite Headers**: {{<render file="_pseudo-ipv4-warning.md" productFolder="fundamentals">}}

{{<Aside type="note">}}
When using *Overwrite Headers*, no software changes are necessary in
your origin web server.
{{</Aside>}}

To configure **Pseudo IPv4**:

{{<tabs labels="Dashboard | API">}}
{{<tab label="dashboard" no-code="true">}}

To change the **Pseudo IPv4** setting in the dashboard:

1.  Log in to your [Cloudflare account](https://dash.cloudflare.com) and go to a specific domain.
2.  Go to **Network**.
3.  For **Pseudo IPv4**, choose your desired setting.

{{</tab>}}
{{<tab label="api" no-code="true">}}

To change **Pseudo IPv4** with the API, send a [`PATCH`](/api/operations/zone-settings-change-pseudo-i-pv4-setting) request with the `value` parameter set to your desired value (`"off"`, `"add_header"`, `"overwrite_header"`).

{{</tab>}}
{{</tabs>}}