[title]: # (Hiding HTTP Header Information)
[tags]: # (Best Practice,Security Hardening,iis server,http header,iis version,ASP.NET version,server type)
[priority]: # (1000)

# Hiding HTTP Header Information

From Web applications such as Secret Server, headers, error messages, version numbers, and other components can leak information an attacker could use to research vulnerabilities, attack the application, and breach the system. To hide HTTP header information in Secret Server, follow the procedures below.

## Hide the IIS Version

To hide the version of IIS used on the server, remove the HTTP header *X-Powered-By* by following the steps below.

1. Open the IIS Manager.
1. In the Connections tree, select the website that Secret Server is running under.
1. Click the **HTTP Response Headers** button on the right. The HTTP Response Headers panel appears.
1. Click to select the **X-Powered-By HTTP** header.
1. Click the **Remove** button in the **Actions** panel.

## Hide the ASP.NET Version

To hide the version of ASP.NET used by the Secret Server application pool, remove the HTTP header *X-ASPNET-VERSION* by following the steps below.

1. Open the `web.config` file for Secret Server, which is located in the root directory for the website.
1. Inside the `<system.web>` tag, add the tag `<httpRuntime enableVersionHeader="false"/>`.
1. Save the file.

## Hide the Server Type

To hide the server type used, remove the line, `Server: Microsoft-HTTPAPI/2.0` (added by the .NET framework) from the HTTP header using the procedure below.

>**Note**: Although there are other methods for hiding the server type, we strongly recommend updating the Windows registry using the procedure below. Do not simply remove the server header variable. Doing so will cause parts of Secret Server to malfunction.

1. Open the Windows registry editor.
1. Navigate to **Computer \> HKEY_LOCAL_MACHINE  \> SYSTEM  \> CurrentControlSet \> Services \> HTTP  \> Parameters**.
1. Change the **DisableServerHeader (REG_DWORD type)** registry key from `0` to `1`.
