# Cloudflare Dynamic DNS Update Script for MikroTik
# Date: March 26, 2025
# Purpose: Automatically update a Cloudflare DNS A record with the current public IP address of the MikroTik router.
# Author: Open Source Community (Feel free to use and modify)
#
# Requirements:
# - A Cloudflare API token with DNS Edit permissions
# - MikroTik RouterOS with internet access
# - Replace the variables with your Cloudflare Zone ID, Record ID, API Token, and DNS record name
#
# DISCLAIMER: Use at your own risk. Always test before deploying in a production environment.

# --- User Configuration ---
:local cloudflareZoneID "YOUR_ZONE_ID"
:local cloudflareRecordID "YOUR_RECORD_ID"
:local cloudflareAPIToken "YOUR_CLOUDFLARE_API_TOKEN"
:local dnsName "yourdomain.com"

# --- Fetch Public IP ---
:local publicIP ([/tool fetch url="https://checkip.amazonaws.com" mode=https output=user as-value]->"data")
:put "Current Public IP: $publicIP"

# --- Construct API Request ---
:local cloudflareURL "https://api.cloudflare.com/client/v4/zones/$cloudflareZoneID/dns_records/$cloudflareRecordID"
:local jsonData "{\"type\":\"A\",\"name\":\"$dnsName\",\"content\":\"$publicIP\",\"ttl\":60}"

# --- Update Cloudflare DNS ---
/tool fetch url=$cloudflareURL \
http-method=put \
http-header-field="Authorization: Bearer $cloudflareAPIToken,Content-Type: application/json" \
http-data=$jsonData mode=https output=user

:put "Cloudflare DNS record updated successfully!"
