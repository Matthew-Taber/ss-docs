[title]: # (Using Connect As Command and SSH Proxy with a PuTTY launcher)
[tags]: # (Connect As Command,PuTTY launcher,SSH proxy,Unix, root account)
[priority]: # (1000)
[redirect]: # (SshProxyWithConnectAs)

# Using Connect As Command and SSH Proxy with a PuTTY Launcher

## Overview

Connect As Command is an advanced setting for the PuTTY launcher type where SSH proxy automatically runs the su command for a Unix root account secret after the user launches a PuTTY session. This provides a user elevated privileges without allowing a remote root connection or giving the user direct access to the credentials. 

The connection procedure is as follows:

1. An admin uses this instruction to set up secret A (a Unix root account secret) to use secret B (a regular Unix account secret) as its "connect as" secret.
1. A user launches secret A.
1. SSH proxy connects using secret B's credentials.
1. SSH proxy issues the su command to switch the user back to secret A. 

The procedure is performed once at the beginning of the session.

As noted, to implement this feature, you typically use a Unix *root* account secret and a Unix *regular* account secret. The session usually launches as the Unix *regular* account secret that is specified in the **Secret To Use** field on a Unix *root* account secret's **Settings** page.

## Setting up SSH Proxy to Use the Connect As Feature

This procedure explains how to set a "connect as" secret when using SSH Proxy to allow connecting with a less privileged account and then using sudo or su to elevate privileges.

1. Make sure SSH proxy is enabled in Secret Server's global configuration settings.

1. Open a secret based on a template with SSH proxy enabled that specifies PuTTY as the launcher type to use.

   >**Note:** For this feature, we recommend building a custom secret based on a copy of the built-in **Unix Root Account (SSH)** template, and associating the PuTTY launcher with it.

1. Click the secret's **Settings** tab.

1. Next to **Connect Using**, select **Credentials on another Secret**.

1. Next to **Secret to Use**, click **No Selected Secret**.

   ![image-connect-as-command2](images/connect-as-command2.png)

1. Navigate to **Admin \> Secret Templates**.

1. Select a template from the drop-down and click **Edit**.

1. Scroll down the page and click **Configure Launcher**.

1. Locate the PuTTY launcher type and  click **Edit**.

1. Verify that the commands in the **Connect As Command** field are correct.

1. If you change anything, click **Save**.

   ![image-connect-as-command3](images/connect-as-command3.png)
