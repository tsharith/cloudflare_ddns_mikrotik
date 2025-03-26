# Cloudflare DDNS on MikroTik

This repository contains a MikroTik RouterOS script to automatically update a Cloudflare DNS A record with the router's current public IP address. Useful for Dynamic DNS (DDNS) setups.

---

## 🔧 How It Works
- The script fetches the current public IP using an external IP-check service.
- If the IP changes, it updates the specified DNS A record in Cloudflare using their API.
- The update interval and credentials are configurable in the script.

---

## 📂 File Information
- **cloudflare_ddns_script.txt:** The main MikroTik RouterOS script. Save it to your MikroTik router and run it using the **"/import"** command.

---

## 🛠️ Configuration Instructions
1. **Upload the Script:**
   - Download the `cloudflare_ddns_script.rsc` file.
   - Open MikroTik **Winbox** or terminal.
   - Use **Files** to upload or use **/import** to import the script.
   
2. **Edit Script Variables:**
   Open the script and update these values:
   - `:local cfToken "YOUR_CLOUDFLARE_API_TOKEN"`
   - `:local zoneId "YOUR_CLOUDFLARE_ZONE_ID"`
   - `:local recordId "YOUR_DNS_RECORD_ID"`
   - `:local domain "YOUR_DOMAIN"`
   
3. **Schedule the Script:**
   - Go to **System** ➔ **Scheduler** ➔ **Add New**.
   - Name: `Cloudflare-DDNS`
   - Interval: Set your desired interval (e.g., 5 minutes)
   - On Event: `/system script run cloudflare_ddns_script`

---

## 🔎 How to Get Required Information
- **API Token:** Go to **Cloudflare Dashboard** ➔ **API Tokens** ➔ **Create Token**.
- **Zone ID:** In the Cloudflare dashboard, click your domain ➔ **Overview** ➔ find **Zone ID**.
- **DNS Record ID:** Use Cloudflare API or check the DNS records in the Cloudflare dashboard.

---

## ⚠️ Notes
- Ensure your router has internet access.
- If using NAT, configure the router's **Firewall/NAT rules** appropriately.
- Test the script manually before scheduling.
