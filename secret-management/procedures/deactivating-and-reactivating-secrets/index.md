[title]: # (Deleting and Undeleting Secrets)
[tags]: # (Secret)
[priority]: # (1000)

# Deactivating and Reactivating Secrets

> **Note:** Deactivating (previously called "deleting") a secret is *not* the same as erasing one—the former hides it but it can still be viewed or undeleted by administrators—the latter is a permanent removal of data and requires more effort, including an access request. Deleting secrets is common. Erasing them is rare, only needed in special circumstances. See [Erasing Secrets](../erasing-secrets/index.md) for details.

To deactivate a secret:

1. Navigate to the secret **View** page by searching or drilling down the folder tree.

1. Click the **Options** dropdown list and select **Deactivate**. A confirmation appears.

1. Click the **Confirm Deactivate** button.

1. The secret is logically deleted and hidden from users who do not have a role containing the View Deactivated Secrets permission.

   > Note: SS uses deactivations to maintain the audit history for all data. However, deactivated secrets are still accessible by administrators (like a permanent Recycle Bin) to ensure that audit history is maintained and to support recovery. A user must have the View Deactivated Secrets permission in addition to Owner permission on a secret to access the secret View page for a deactivated secret. For more information about these permissions, see [Roles](../../../roles/index.md) and [Sharing a Secret](../sharing-secrets/index.md).

To reactivate a secret:

1. Navigate to the secret view page.
1. Click the **Active** menu link and select **Inactive**. The secret list now shows inactive secrets.
1. Click the name link for the desired secret. Its secret page appears.
1. Click the **Options** button and select **Activate**.

> **Note:** Secrets can also be deactivated and reactivated in bulk. See [Running Dashboard Bulk Operations](../../../application-administration/application-dashboard/index.md#running-dashboard-bulk-operations).
