# Automate UAlbany SSO
UAlbany login SSO automation ( for use with Tampermonkey )

UAlbany’s SSO and EZProxy login flow is a textbook UX anti-pattern. Between rapid cross-domain redirects, aggressive session timeouts, and zero dark-mode support across Shibboleth and Duo Security, researchers are constantly subjected to blinding white screen flashes (FOUC) and repetitive login clicks just to open a PDF via EZProxy.

This script is a simple, all-in-one Tampermonkey Band-Aid that makes the proxy invisible:


- **Dark-Mode**: Injects a `#121212` CSS shroud at document-start over UAlbany SSO and Duo pages so you never get flashbanged during redirects.

- **0ms Instant Auto-Login**: Stores credentials locally in Tampermonkey's isolated storage to populate and submit the Shibboleth form and Duo's "Trust this browser" prompt instantaneously.
- **Silent Keep-Alive**: Pings EZProxy in the background via `GM_xmlhttpRequest` every 10 minutes while you browse Google Scholar, IEEE, ACM, or arXiv so your session never expires.


## ⚠️ Disclaimers & Fair Warning

1. **Security vs. UX:** This does not bypass or compromise the frankly **excellent security architecture** the university has in place (Shibboleth + Duo 2FA still validate every session).  _I just wish they studied UX, "human" factor of cyber security, and session timeouts with the same enthusiasm..._
2. **This work is made for GROWNUPS:** I am not kidding about this—for folks who know what they are doing, storing credentials locally in browser extension storage carries inherent risks if your local machine is unlocked or compromised. No one is responsible for your actions if you are playing with fire.
3. **I am a teacher at heart:** For those who have never played around with password managers, userscripts, or uBlock Origin (uBO), I'd love to talk about how the web works with you :)

--- 

## First-Time Setup


Your credentials are **never** hardcoded into the script—they are stored locally inside Tampermonkey's isolated extension storage (`GM_setValue`).

1. **Install the script** in [Tampermonkey](https://www.tampermonkey.net/).
2. **Set your NetID & Password** :
   * **Manual Setup (Recommended):** Open any matching tab (e.g. `albany.edu`), click the **Tampermonkey extension icon** in your browser toolbar, and click **"Set / Update UAlbany Credentials"** under the script's menu.
3. **Allow Background Keep-Alive:** The first time you open Google Scholar, IEEE, ACM, or arXiv, Tampermonkey will ask for permission to connect to `libproxy.albany.edu`. Click **"Always allow domain"** so the silent session heartbeat can run in the background.
4. **Duo 2FA:** The first time you authenticate, approve the Duo push as usual—the script will automatically click **"Trust this browser"** so subsequent logins pass through silently.

> **Need to update or clear your password later?** Click the Tampermonkey icon on any supported page and select **"Set / Update UAlbany Credentials"** or **"Clear UAlbany Credentials"**.


---

## Related

- Ohter in this series : [Removing Brightspace annoyances and tracking](https://github.com/ninadpchaudhari/UAlbany-Brightspace-Annoyances)
