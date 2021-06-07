[title]: # (Enabling Common Criteria Security)
[tags]: # (Common Criteria,Security Hardening)
[priority]: # (1000)

# Enabling Common Criteria Security

Secret Server versions 10.4 and newer provide every security feature and capability required for administrators to achieve Common Criteria certification by following the procedures below. Due to the stringency of the standard and the need for administrators to configure some of the capabilities, not all of these features are enabled by default in our standard installer.

The Common Criteria for Information Technology Security Evaluation (ISO/IEC 15408), known as *Common Criteria*, is an international standard for certifying the security of computer systems, networks, and application software. The certification provides independent validation of security claims about the specified evaluated product in the evaluated environment with the evaluated configuration. The certification provides no validation of security claims applied to the product outside of the evaluated environment or the evaluated configuration.

To perform these procedures, you must have administrator access, privileges, and responsibilities for installing, configuring, and operating enterprise infrastructure for your organization. You must also have sufficient knowledge of your organization’s network infrastructure and applicable policies. To ensure that each parameter setting matches those evaluated and certified as secure by Common Criteria standards, you must follow this procedure in its entirety.

This procedure refers frequently to the Common Criteria Hardening Guide, or *CCHG*.

## Follow the Security Hardening Checklist

After installing Secret Server, navigate to the **Reports \> Security Hardening** tab, and follow the checklist to enhance the default settings that Common Criteria requires.

## Configure Transport Layer Security

Common Criteria requires using Transport Layer Security in Secret Server (TLS). To securely enable TLS, follow the steps in the sections below:

### Manually Disable Transport Layer Security Version 1.0

Transport Layer Security 1.0 is no longer considered secure, so it is important to disable this version of the protocol on Secret Server. See the CCHG section, *Manually Disabling Transport Layer Security v1.0.*

### Transport Layer Security Diffie-Hellman Hardening Overview

To configure your servers with stronger Ephemeral Diffie-Hellman hardening, see the CCHG, section 11.3.4.

### Restrict Server Cipher Suites for Transport Layer Security

Common Criteria requires restricting the cipher suites configured on your server to only the following:

* Transport Layer Security_DHE_RSA_WITH_AES_128_CBC_SHA

* Transport Layer Security_DHE_RSA_WITH_AES_256_CBC_SHA

* Transport Layer Security_RSA_WITH_AES_128_CBC_SHA

* Transport Layer Security_RSA_WITH_AES_128_CBC_SHA256

* Transport Layer Security_RSA_WITH_AES_256_CBC_SHA

* Transport Layer Security_RSA_WITH_AES_256_CBC_SHA256

Restricting cipher suites can cause communication issues with other servers if they cannot communicate using any of the above ciphers. In that case, you need to modify those servers to include these cipher suites to securely communicate according to Common Criteria guidelines.

### Change Cipher Suites with the IIS Crypto Tool

One way to change the cipher suites on a computer is to use the free IIS Crypto tool:

1. Download the GUI version of the [IIS Crypto Tool] (https://www.nartac.com/Products/IISCrypto/Download).

1. Run the tool:

   1. Click the **Cipher Suites** button on the left.

   1. In the Cipher Suites window, click the **Uncheck All** button.

   1. Find and click to select the suites in the list above.

   1. Click the **Apply** button.

### Configure Transport Layer Security with IIS

Common Criteria requires using HTTPS/SSL for all connections to the Secret Server server Web page. Follow the instructions in the CCHG section, *Transport Layer Security Configuration with IIS*.

### Enable Transport Layer Security Auditing

To have Secret Server audit TLS connections and connection failures, follow the instructions in the CCHG section, *Configuring Auditing for Transport Layer Security Connections*.

### Configuring TLS with Active Directory

To ensure that TLS is configured with Active Directory Follow the instructions in the CCHG section, *Configuring Transport Layer Security with Active Directory*.

>**Note**: If you have any existing domains configured in Secret Server, you must edit them and enable LDAPS on each one.

### Configure Transport Layer Security with Syslog

To configure TLS with Syslog, follow the steps in the CCHG section, *Configuring Syslog/CEF External Audit Server*.

## Additional Common Criteria Configurations

### Configuring X.509v3 Certificates

See the CCHG section, *Configuring X.509v3 Certificates* for instructions on installing and configuring certificates on the Secret Server Web servers.

## Enabling DPAPI

The Windows Data Protection API (DPAPI) is a pair of functions that allow access to operating-system-level data protection services to protect the master encryption key file, encryption.config.

To enable DPAPI, follow the instructions in the CCHG section, *Verify DPAPI Setting Is Enabled*.

## Enable FIPS Mode

To configure your server and Secret Server to use the Federal Information Processing Standard (FIPS), follow the instructions in the CCHG section, *Verify FIPS Mode Is Enabled*.

>**Note**: Also see: https://thycotic.force.com/support/s/article/Enabling-FIPS-Compliance-in-Secret-Server

## Ensuring Zero Information Disclosure

To comply with Common Criteria regulations, you must configure Secret Server to not display any unnecessary information. This applies to unhandled errors as well as the application version number.

### Configure Custom Error Messages

To hide detailed error messages and display a custom message when an unhandled error occurs:

1. Open https://<your_secret_server_url>/ConfigurationAdvanced.aspx in your browser.

1. Scroll to the bottom of the page and click the **Edit** button.

1. Type the message you want displayed to users in the **Zero Information Disclosure Message** text box.

1. Click the **Save** button.

### Hide the Application Version Number

To hide the application version number in the application header and footer:

1. Go to **Admin \> Configuration \> Security**.

1. Click the **Edit** button. The Configuration page appears: 

1. Click the **Security** tab.

1. In the **Web Services** section of the page, click to select the **Hide Secret Server Version Numbers** check box.

1. Click the **Save** button.

>**Note**: For diagnostic purposes, the application version number is still displayed on the Diagnostics page. Make sure that permissions to this page is limited to employees that may need to access this page when contacting Thycotic technical support.

## Configure the Login Banner

For Common Criteria compliance, when a user first logs in, the login banner must reveal the user policy agreement and force that user to agree to the policy before logging into Secret Server. To configure the Login Banner according to Common Criteria guidelines, follow the instructions in the CCHG section, *Configuring the Login Banner*.

## Configure Account Lockout

To access Secret Server, users must login with local or domain credentials. To comply with Common Criteria, Secret Server must use "account lockouts" to prevent repeated unsuccessful login attempts. Configurable by a Secret Server admin, an account becomes inaccessible after a defined number of unsuccessful authentication attempts until an admin unlocks the user’s account.

To configure settings for account lockouts:

1. Navigate to **Admin \> Configuration**.

1. Click the **Login** tab.

1. Click the **Edit** button.

1. Adjust the number in the **Maximum Login Failures** text box. The default is five attempts.

To Unlock a user’s account:

1. Navigate to **Admin \> Users \> Select the User**.

1. Click the **Edit** button.

1. Click to deselect the **Locked Out** check box.

1. Click the **Save** button.

## Disable *Remember Me* logins

A browser's "remember me" login function stores the user's login name and password so the user does not need to enter it again on that browser, which is both convenient and insecure. To disable *Allow Remember Me* during logins, follow the instructions in the CCHG section, *How to Disable Allow Remember Me during Logins*.

## Configure SQL Server

To meet Common Criteria, Microsoft SQL Server must be installed on the local machine—the same as the Secret Server Web server. During the install process for MS SQL, ensure that you use Windows authentication mode.

If you have an installed instance of Secret Server that does not meet this requirement, you can migrate the remote database to the server hosting Secret Server. If MS SQL Server is not installed and configured on the Secret Server server, you must install it. The server must be configured with enough RAM, storage space, and processors to support running MS SQL Server and the Web site simultaneously. After copying the database, you can go to **Admin \> Database** to point Secret Server to the new database location.

>**Note**: Because the database must be installed locally with the Secret Server Web application for Common Criteria compliance, Secret Server is not fully compliant when running multiple nodes.

## Run the IIS Application Pool with a Service Account

To use Windows authentication to access the SQL database, you should create a service account. To run the Secret Server IIS Application Pool with a service account:

1. Open a command prompt window, and use the `cd` command to change the directory to your .NET framework installation directory (usually `C:\Windows\Microsoft.NET\Framework…` )

1. Type `.\aspnet_regiis -ga <user name>` and press `<Enter>`. The username is from the MS SQL Server user account.

1. Give your service account "modify" access to `C:\Windows\TEMP.`

1. Open the **Local Security Policy App** from your start menu.

## Grant batch logon permissions to your service account:

1. Open the **Local Security Policy Console** (search for and open secpol.msc): 

1. Expand the **Local Policies** folder (not shown).

1. Click to select the **User Rights Assignment** folder. 

1. Right-click **Log on as a batch job** in the right panel and select **Properties**. 

1. Click the **Add User or Group** button.

1. Add your service account.

1. Click the **OK** button.

>**Note**: If you use group policy to enforce *Log on as a batch job* and you have group-managed service accounts, that will overwrite any local permissions to *Log on as a batch job* on all computers that have the policy applied. Using the local security policy is a safer option if you are not sure about your usage across your domain.

Grant **Impersonate a client after authentication** permission to the service account under **User Rights Assignment** the same way *Log on as a batch job* was assigned above.

If you now get a *Service Unavailable* error after applying *Log on as a batch job* permissions:

Update your group policy settings (Start > Run > Cmd and type gpupdate /force) and restart the **Windows Process Activation** service.

>**Note**: For information on configuring a Windows account for database access, see: https://thycotic.force.com/support/s/article/Using-Windows-Authentication-for-Database-Access.

## Assigning Common Criteria Roles and Permissions

See the CCHG section, *Common Criterial Roles and Permissions*.

## Managing User Passwords

See the CCHG section, *Managing User Passwords*.

## Configuring Secret Templates

To enable only the secret templates that are certified Common Criteria compliant and to set Common Criteria-compliant password policies on those templates, see the CCHG sections, *Configuring Secret Templates* and *Configuring Password Policy for Secret Templates*.

## Setting Authentication Strength for Non-Password Credentials

See the CCHG section, *Authentication Strength for Non-Password Credentials*

## Configuring Remote Password Changing for Secret ServerH Key Rotation

See the CCHG section, *Configuring Remote Password Changing for Secret ServerH Key Rotation*.

## Configuring External Auditing

Connecting to an External Audit Server
To connect to an external syslog/CEF audit server, see the CCHG sections, *Security—Connecting to an External Audit Server* and *Configuring Syslog/CEF External Audit Server*.

## Configuring Local Windows Event Log Auditing

See the CCHG section, *Configuring Local Windows Event Log Auditing*.

## Related Articles and Resources

[Secret Server: Security Hardening Guide](https://thycotic.force.com/support/s/article/Security-Hardening-Secret-Server)

[Common Criteria Harding Guide](https://updates.thycotic.net/secretserver/documents/gov/SS_CommonCriteria_HardeningGuide_v10.pdf)


