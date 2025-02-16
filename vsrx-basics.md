---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: basics, performing, accessing, ssh, device, gateway, configuration, mode, juniper, ui, dns, htp, password

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Performing vSRX Basics
{: #performing-ibm-cloud-juniper-vsrx-basics}

The {{site.data.keyword.vsrx_full}} gateway can be configured using a remote console session through SSH or by logging into the Juniper web management GUI.

Configuring the vSRX outside of its shell and interface may produce unexpected results and is not recommended.
{: note}

## Accessing the Device Using SSH
{: #accessing-the-device-using-ssh}

You can access the vSRX using SSH through a public IP address, or through a private IP address if you're on IBM Cloud VPN:

1. Go to Gateway Appliance Details screen and get the Public gateway IP or Private Gateway IP.

  <img src="images/gw-sa-details.png" alt="drawing" style="width: 700px;"/>

2. Click the "eye" icon to reveal the admin user's password.

3. Run the command `ssh admin@<gateway-ip>`, then enter the admin user's password.

If you do not see the "eye" icon, you may not have permission to view the password. Please check your access permissions with the account owner.
{: note}

## Accessing the Configuration Mode
{: accessing-the-configuration-mode}

You can enter the configuration mode, once a shell has been opened to the vSRX, by running the `config` command. You can do several things in this mode using the following commands:

* `show` - View configurations  
* `show | compare` - View staged changes
* `set` - Stage changes
* `commit check` - Verify the syntax of the configuration

If you are happy with your changes, you can commit them to the active configuration by running the commands `commit` and then `save`.  

To leave Configuration mode run the command `exit`.

## Accessing the Device using the Juniper Web Management UI
{: #accessing-the-device-using-the-juniper-web-management-ui}

The Juniper web management GUI has been configured by default, with vSRX generated self-signed certificate. Only https is enabled on port 8443. You can access it at `https://gateway-ip:8443`.

![Gateway Appliance HA Details](images/vSRX-webui.png)

## Creating system users
{: #creating-system-users}

By default, the {{site.data.keyword.vsrx_full}} is configured with SSH access for the username `admin`. Additional users can be added with their own set of priorities. For example:

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

In this example, `ops` is the username and `operator` is the class/permission level assigned to the user.

Customized classes can be also defined as opposed to pre-defined ones.

## Defining the vSRX hostname
{: #defining-the-vsrx-hostname}

You can set or change the vSRX hostname using the following command:

```
set system host-name <hostname>
```

## Configuring DNS and NTP
{: #configuring-dns-and-ntp}

To configure name server resolution and NTP, run the following commands:

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## Changing the root password
{: #changing-the-root-password}

You can change the root password by running the following command:

```
set system root-authentication plain-text-password
```

This prompts you to input a new password, which is encrypted and stored in the configuration, and is not visible.
