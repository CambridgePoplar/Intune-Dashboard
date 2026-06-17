# Intune Device Dashboard

A lightweight, single-file executive dashboard for Microsoft Intune built on the **Microsoft Graph API**. Designed for IT and security teams to monitor device compliance, enrollment trends, and asset sprawl — no backend required.

---

## What It Shows

- **Overall compliance %** with 12-week trend
- **Compliance by platform** — Windows, iOS, macOS, Android
- **New device enrollments** over the last 30 days (daily breakdown)
- **Users with multiple devices** — top users by device count with platform and compliance status
- **Recently enrolled devices** — newest managed endpoints
- **Enrollment mix** and device count distribution

---

## How to Use

### Demo Mode
Open the dashboard and it loads immediately with sample data — no credentials needed. Good for previewing the layout or sharing a mockup.

### Live Mode (Graph API)
To pull real data from your Intune environment:

1. Click **Connect Graph API** in the top right
2. Enter your **Tenant ID**, **Client ID**, and **Client Secret**
3. Click **Connect** — the dashboard refreshes with live data

---

## Setting Up Your Azure App Registration

You need an app registration in Azure AD with read-only Graph API permissions.

### 1. Register the App
1. Go to [portal.azure.com](https://portal.azure.com)
2. Navigate to **Azure Active Directory → App registrations → New registration**
3. Name it `Intune Dashboard Reader`
4. Set supported account types to **Single tenant**
5. Click **Register**

### 2. Add API Permissions
1. Go to **API permissions → Add a permission → Microsoft Graph → Application permissions**
2. Add the following:

| Permission | Purpose |
|---|---|
| `DeviceManagementManagedDevices.Read.All` | Read all managed device data |
| `DeviceManagementConfiguration.Read.All` | Read compliance policy states |
| `User.Read.All` | Map devices to users |
| `Directory.Read.All` | Entra join status |

3. Click **Grant admin consent**

### 3. Create a Client Secret
1. Go to **Certificates & secrets → New client secret**
2. Set an expiry (12 months recommended)
3. **Copy the secret value immediately** — it won't be shown again

### 4. Find Your IDs
| Value | Where to find it |
|---|---|
| Tenant ID | Azure AD → Overview → Tenant ID |
| Client ID | Your app registration → Overview → Application (client) ID |
| Client Secret | The value you copied in step 3 |

---

## Running Locally

Browsers block the Microsoft login request when opening the file directly (`file://`). To run locally, serve it with Python:

```bash
python -m http.server 8080
```

Then open `http://localhost:8080` in your browser.

---

## Security Note

Credentials are used only to fetch a short-lived access token and are never stored. For production use, consider proxying the token request through a backend service to avoid exposing the client secret in the browser.

---

## Hosted on GitHub Pages

This dashboard is deployed via GitHub Pages and accessible at:

```
https://YOUR-USERNAME.github.io/intune-dashboard
```
