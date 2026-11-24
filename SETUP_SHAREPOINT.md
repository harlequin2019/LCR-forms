# LCR Field Forms – SharePoint upload setup (for the Microsoft 365 admin)

This is a one-off setup, about 10 minutes. Once it's done, the app can upload its PDFs straight into:

`LagoonCreekResourcesPtyLtd › Shared Documents › Lagoon Creek Resources Pty Ltd › Aus Geo Admin › 01. Health and Safety`

## What it does and doesn't do
- Users sign in with their normal Laramide Microsoft account. The app only gets *delegated* access, so each person can upload only where they already have write permission in SharePoint.
- There is no client secret and no server. The app runs entirely on the phone (a static web page hosted on GitHub Pages) and talks directly to Microsoft Graph.
- Records made offline wait on the phone and upload automatically next time there's signal and the user is signed in.

## Steps (Microsoft Entra admin centre)
1. **Applications → App registrations → New registration**
   - Name: `LCR Field Forms`
   - Supported account types: *Accounts in this organizational directory only*
   - Redirect URI: platform **Single-page application (SPA)**, URI `https://harlequin2019.github.io/LCR-forms/index.html`
2. Open the new app → **Authentication** → under Single-page application, add a second redirect URI: `https://harlequin2019.github.io/LCR-forms/`
3. **API permissions → Add a permission → Microsoft Graph → Delegated permissions**. Add:
   - `Files.ReadWrite.All`
   - `offline_access`, `openid`, `profile`

   Then click **Grant admin consent for Laramide**.
4. From the app's **Overview** page, copy the **Directory (tenant) ID** and the **Application (client) ID** and send them to the field team.

## Then, in the app
In **Settings → SharePoint upload**, paste the two IDs, tap **Save**, then **Sign in to Microsoft**.

To avoid doing this on every phone: after one phone is set up, use **Settings → Export current lists as a team pack**. The exported file includes the two IDs; the other phones import it.

## Notes
- Microsoft limits sign-ins for single-page apps to 24 hours. After that, the app asks the user to sign in again the next time they have signal. Records keep saving offline in the meantime.
- If uploads fail with "Access denied", check that the user can add files to the Health and Safety folder in SharePoint.
- Optional per-form sub-folders can be set under Settings → Advanced. Leave them blank to put every PDF straight into `01. Health and Safety`.
