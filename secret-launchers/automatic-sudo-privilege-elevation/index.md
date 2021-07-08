[title]: # "Automatic Sudo or Su Privilege Elevation"
[tags]: # "Sudo or Su Elevation,SSH proxy,Unix, root account"
[priority]: # "1000"

# Automatic Sudo or Su Privilege Elevation

Secret Server has a convenience feature that eliminates the need to manually enter a su or sudo command's password when using a proxied SSH session to a Unix or Linux server. When a user manually types a su or sudo command with a valid secret ID, the SSH proxy automatically provides the username and password to use. The user does not need to know either.

For su, the connection procedure is as follows:

1. Secret A is created to contain the username and password for the su privilege elevation. Any potentially elevated users must have access to this secret. 
1. Using secret B, a user (with access to secret A) starts a SS proxied SSH session.
1. When the user types su at the command prompt, the SSH proxy detects it, determines the user has access to secret A, and augments the command with the secret ID for secret A via a command line argument. Any other arguments the user may have typed are left as is. 
1. The user runs the su command, and the secret ID is replaced with the user and credential from secret A. 
1. With the elevated permissions (temporarily as another user) from secret A, the user completes the desired tasks.
1. When finished, the user uses an exit command to return to their non-elevated status based on secret B.

> **Note:** The added argument appears as `–-secret-id <secret ID>` or `–id <secret ID>`, such as `su --secret-id ElevationSecret`, which is replaced by a username and password when the command runs.

> **Note:** Sudo does not take either secret argument and automatically types the current user's password.

