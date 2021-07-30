[title]: # (Troubleshooting Google Authenticator)
[tags]: # (troubleshooting,google,authenticator,token,leniency)
[priority]: # (1000)

# Troubleshooting Google Authenticator

Google Authenticator relies on time to create tokens. If Secret Server's clock is inaccurate or is not synchronized with devices running Google Authenticator, user token validation may fail when enrolling or logging in.

## Solution A (preferred)

Ensure that Secret Server's clock is accurate and synchronized with the device running Google Authenticator. Set the web servers to synchronize their clocks with an accurate domain controller clock or with an NTP server.

## Solution B

By default the leniency value for token time accuracy is zero, which means the token supplied must be accurate. Follow the steps below to configure Secret Server with higher leniency to accept tokens with times that are slightly behind or slightly ahead.

1. Open the `web-appSettings.config` file and add the following key between the `appSettings` tags.

   `<add key="TOTPLeniency" value="0 or greater value here" />`

1. Change the leniency value. We recommend setting this value to no higher than 2.

1. Recycle your IIS application pool. You must recycle your IIS application pool for the setting to take effect.
