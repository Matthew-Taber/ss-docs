[title]: # (Trusting an SSL Certificate on a Client Machine)
[tags]: # (authentication,ssl certificate,client machine)
[priority]: #

# Trusting an SSL Certificate on a Client Machine

For public websites, only SSL certificates issued by trusted authorities are recognized as valid. Self-signed certificates used only within a company or domain might generate security warnings but these can be ignored. The same is true of self-signed certificates installed on a server for the Secret Server website. However, these security warnings can also interfere with the use of the Secret Server Launcher and Web Password Filler. To resolve these issues, install the certificate on the client machine, either through Internet Explorer or Certificates snap-in.

To enable trust in the Secret Server self signed certificates, following these steps:

## Step 1: Compare Host Names

Make sure that the host to which the certificate is issued is the same as the host name for your Secret Server website:

1. Open Internet Explorer and navigate to Secret Server.

1. Click **Continue to this website** if you are prompted.

1. Click the **Certificate Error** icon next to the navigation bar.
1. Click the **View certificate** button. The value next to **Issued to** should match the host name for your website. For example, if your website is `https://www.mydomain.local/SecretServer`, it should say **Issued to:** `www.mydomain.local`. If these fields do not match, the client will not be able to fully trust the certificate.

## Step 2: Transfer a copy from your server to the client computer

Obtain a copy of the certificate file and transfer it to the client computer:

1. On the server where Secret Server is installed, find **Run** from the start menu or screen and type in `mmc`, then click the **Enter** button.
1. From the **File** menu, select **Add/Remove Snap-in**.
1. Select the **Certificates** snap-in, then click the right arrow button to add it.
1. In the window that appears, select **Computer Account**.
1. Select **Local Computer**.
1. Click **Finish**. You should now see the **Certificates (Local Computer)** node.
1. Expand the **Personal** folder and then the **Certificates** folder under it.
1. Right-click the certificate that Secret Server uses.
1. Click **All tasks**.
1. Select **Export**.
1. Keep clicking the **Next** button to accept defaults in the wizard.
1. Type in a filename.
1. Click the **Finish** button. The certificate has now been exported.

>**Note:** If you have Firefox, the certificate can be saved to your client computer by viewing and exporting it after navigating to the website.

## Step 3: Install the certificate on the client computer

1. On the client computer, find **Run** from the start menu or screen and type in `mmc`, then hit the **Enter** button.
1. From the **File** menu, select **Add/Remove Snap-in**.
1. Select the **Certificates** snap-in, then click the right arrow button to add it.
1. In the window that appears, select **My user account**.
1. Click the **Finish** button.
1. Expand the **Trusted Root Certification Authorities** folder.
1. Right-click the **Certificates** folder and select **All Tasks \> Import**.
1. Click **Next** and **Yes** to accept default settings for all steps of the wizard.
1. When prompted for the certificate file, select the file you saved in the previous Step 2.

>**Note:** You may need to re-open Internet Explorer and browse to Secret Server once more to see the change reflected on the client machine.
