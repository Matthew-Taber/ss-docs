[title]: # (Moving Secret Server to Another Machine)
[tags]: # (Installation,moving)
[priority]: # (1000)

# Moving Secret Server to Another Machine

If you are moving/migrating Secret Server to a new machine and have installed IIS and .NET Framework as described in the Installation Guide on the new machine, you do not need to run the installer; you just need to follow the steps below:

1. If you use the "Force HTTPS/SSL" option, disable it by clicking **Configuration** from the **Administration** menu, and then click the **Security** tab, and **Edit**. You can re-enable the "Force HTTPS/SSL" option after you set up and install an SSL certificate on the new machine.

   >**Note**: If you are also moving the SQL Server database, be sure to create a new backup of the database, as this setting is written to it. To move the database, follow the steps in [Moving the Microsoft SQL Server Database to Another Machine](../moving-sql-server/index.md).

1. If you have configured encryption of your key using DPAPI, you will also need to turn this off before continuing with Step 3. To do so, click **Configuration** from the **Administration** menu, then click the **Security** tab. Click **Decrypt Key** to *not use* DPAPI and enter your Secret Server account password.

1. Copy the folder that holds your Secret Server instance to the new computer.
1. Shut down the old web site and recycle its application pool as it is running background threads that are accessing the database.
1. Set up the new folder in Internet Information Server (IIS) as a virtual directory/application under the Default Web Site or as a separate Website. For detailed instructions, refer to [Advanced Installation](../advanced-installation-manual/index.md) in the Installation Guide.
1. If your database server and credentials have not changed, skip this step. If they have changed, follow the steps below:
   1. Delete the database.config file from the secretserver folder (on the ASP.NET/IIS machine).
   1. Restart your new Secret Server website, so it is running.
   1. Browse to your Secret Server URL \ dbconnectionreset.aspx `http:\\secretserverurl\dbconnectionreset.aspx` and you will be prompted to enter your new database connection details.
   1. Enter your new SQL Server and the account information.
   1. Click **Next** and the site will connect to the new database. Your site is now pointing the new database.
1. When you browse to Secret Server on the new machine it will usually state that it is a secondary node. This is because the database still knows about the previous server. If the old machine was a primary node, then follow these steps to change the new machine to being the primary node:
   1. On the server you will make the primary node, navigate to Secret Server locally.
   1. Log in as an administrator, and click **Server Nodes** from the **Administration** menu.
   1. Click the **Make Current Node Primary** button.
1. Activate the licenses for the new server by going to the **Licenses** page.
1. If you are using certs, remember to set them on your new IIS, and then browse to Secret Server over HTTPS and re-enable force HTTPS if this was set on the original machine.
1. Re-enable DPAPI if this was disabled in the earlier step.
   >**Note**: If you are moving Secret Server web application from Windows Server 2008 to 2012 AND your Secret Server is below version 8.5, make sure that:

  * .Net extensions 3.5 and ASP.Net 3.5 when adding the IIS role on the new server.
  * Change the Secret Server application pool to 2.0 and recycle the application pool after running the installer.
