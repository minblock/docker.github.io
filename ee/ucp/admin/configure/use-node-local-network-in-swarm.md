---
title: Use a local node network in a cluster
description: Learn how to use a local node network, like MAC VLAN, in a UCP cluster.
keywords: ucp, network, macvlan
ui_tabs:
- version: ucp-3.0
  orhigher: false
- version: ucp-2.2
  orlower: true
---
{% if include.version=="ucp-3.0" %}

Docker Universal Control Plane can use your local networking drivers to
orchestrate your cluster. You can create a *config* network, with a driver like
MAC VLAN, and you use it like any other named network in UCP. If it's set up
as attachable, you can attach containers.

> Security
>
> Encrypting communication between containers on different nodes works only on
> overlay networks. 

## Use UCP to create node-specific networks

Always use UCP to create node-specific networks. You can use the UCP web UI 
or the CLI (with an admin bundle). If you create the networks without UCP,
the networks won't have the right access labels and won't be available in UCP.

## Create a MAC VLAN network

1. Log in as an administrator.
2. Navigate to **Networks** and click **Create Network**.
3. Name the network "macvlan".
4. In the **Driver** dropdown, select **Macvlan**.
5. In the **Macvlan Configure** section, select the configuration option.
   Create all of the config-only networks before you create the config-from
   network.

   - **Config Only**: Prefix the `config-only` network name with a node hostname
   prefix, like `node1/my-cfg-network`, `node2/my-cfg-network`, *etc*. This is
   necessary to ensure that the access labels are applied consistently to all of
   the back-end config-only networks. UCP routes the config-only network creation
   to the appropriate node based on the node hostname prefix. All config-only
   networks with the same name must belong in the same collection, or UCP returns
   an error. Leaving the access label empty puts the network in the admin's default
   collection, which is `/` in a new UCP installation.
   - **Config From**: Create the network from a Docker config. Don't set up an
   access label for the config-from network. The labels of the network and its
   collection placement are inherited from the related config-only networks.

6. Click **Create** to create the network.

{% elsif include.version=="ucp-2.2" %}

Learn about [using a local node network in a cluster](/datacenter/ucp/2.2/guides/admin/configure/use-node-local-network-in-swarm.md).

{% endif %}