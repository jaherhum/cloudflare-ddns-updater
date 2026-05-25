# cloudflare-ddns-updater

Lightweight bash script to automatically update a Cloudflare DNS A record with your current public IP (DDNS).

## Requirements

- `curl`
- `jq`

## Cloudflare Setup

### 1. API Token

Go to [dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens) and create a new token with the following permission:

- **Zone → DNS → Edit**

Set the scope to the specific zone (domain) you want to update.

Save the token — you'll need it in the `.env` file.

### 2. Zone ID

In the Cloudflare dashboard, open your domain. You'll find the **Zone ID** in the right-hand sidebar. Copy it.

### 3. DNS Record

Manually create an **A record** in your domain pointing to any IP (e.g. `1.2.3.4`). The script will overwrite it with your actual public IP on each run.

## Setup

1. Clone the repository:
```bash
   git clone https://github.com/jaherhum/cloudflare-ddns-updater.git
   cd cloudflare-ddns-updater
```

2. Copy the example config and fill in your values:
```bash
   cp .env.example .env
```

```env
   CF_API_TOKEN=your_token_here
   CF_ZONE_ID=your_zone_id_here
   CF_RECORD_NAME=subdomain.yourdomain.com
```

3. Make the script executable:
```bash
   chmod +x update-dns.sh
```

4. Run it:
```bash
   ./update-dns.sh
```

## Automation with cron

To run every 5 minutes:

```bash
crontab -e
```

Add:
```bash
*/5 * * * * /absolute/path/to/update-dns.sh >> /var/log/ddns.log 2>&1
```

## License

MIT