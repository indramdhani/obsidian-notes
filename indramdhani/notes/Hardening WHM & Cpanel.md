# Hardening WHM & Cpanel

## Set WHM Contact Email Address

_Location: Home → Server Configuration → Basic WebHost Manager Setup_

-   \[ \] setup contact email to receive notification

## Install Munin Monitor

_Location: Home → cPanel → Manage Plugins_

-   \[ \] install munin as the monitoring service

## Install ClamAV

_Location: Home → cPanel - Manage Plugins_

-   \[ \] install ClamAV
-   \[ \] setup ClamAV to scan needed directory

## Set suPHP as default PHP Handler

## Tweak Settings Security Configuration

_Location: Home → Server Configuration → Tweak Settings_

### Disable unnecessary stats programs

Enable only one stats programs

-   \[ \] Enable Analog Stats → Off
-   \[ \] Enable Awstats stats → Off
-   \[ \] Enable Webalizer stats → Off

### Email security tweaking

-   \[ \] Enable DKIM on domains for newly created accounts → On
-   \[ \] Enable SPF on domains for newly created accounts → On
-   \[ \] BoxTrapper Spam Trap → Off
-   \[ \] Initial default/catch-all forwarder destination → Fail
-   \[ \] Track email origin via X-Source email headers → On
-   \[ \] Enable Apache SpamAssassins spam filter → On

### Disable old buggy horde

-   \[ \] Enable Horde Webmail → Off

### Enable system notifications

-   \[ \] System disk space usage warnings → On
-   \[ \] Enable mailbox usage warnings → On
-   \[ \] Send bandwidth limit notification emails → On

### Disable unnecessary CGI stuff

-   \[ \] CGIEmail and CGIEch → Off

### Enforce cPanel/WHM/Webmail SSL usage

-   \[ \] Always redirect to SSL → On
-   \[ \] Require SSL → On

### Extra security checks

-   \[ \] Blank referrer safety checks → On
-   \[ \] Referrer safety checks → On

### Misc security settings

-   \[ \] use cpanel jailshell by default → on
-   \[ \] Include password in the raw log download link in cpanel (via ftp) → Off

### Limit Server status allowed IPs

-   \[ \] allow server info and server status

### Prevent Spam - Abuse issues

-   \[ \] max hourly emails per domain → 200
-   \[ \] the percentage of email messages ( above the account's hourly maximum) to queue and retry for delivery → 100
-   \[ \] count mailman deliveries towards a domain's max hourly emails → on
-   \[ \] maximum percentage of failed or deferred messages a domain may send per hour → 35%
-   \[ \] prevent "nobody" from sending mail → on
-   \[ \] allow users to relay mail if they use an ip address through which someone has validated an imap or pop3 login within the last hour (pop-before-smtp) → off
-   \[ \] add x-popbeforesmtp header for mail sent via pop-before-smtp → off
-   \[ \] prefix "mail." onto mailman urls → on

## WHM Security Center

_Location: WHM → Security Center_

-   \[ \] apache mod\_userdir tweak → on
-   \[ \] Compiler access → off
-   \[ \] PHP open\_basedir tweak → on
-   \[ \] shell fork bomb protection → on
-   \[ \] traceroute enable/disable → disable
-   \[ \] two factor authentication → enable

### Define Password Strength Configuration

_Location: WHM → Security Center → Password Strength Configuration_

Default Required Password Strength – 65

Check ‘Default’ on all the available options.

### Enable cPHulk Brute Force Protection

_Location: WHM → Security Center → cPHulk Brute Force Protection_

cPHulk is cPanel’s Brute Force Protection service. It helps to mitigate and block username and ip based attacks.

### Enable background process killer

Background Process Killer allows you to select process that if found, the cPanel system will terminate after the daily maintenance scripts run (/scripts/maintenance).

_Location: WHM → System Health → Background Process Killer_

### Enable SSL for your hostname

Check **Enforce cPanel/WHM/Webmail SSL usage** \*\*Section

### Configure Security Policies

_Location: WHM → Security Center → Configure Security Policies_

Recommended configuration are

-   \[ \] Limit logins to verified IP Address → Enabled
-   \[ \] Password Strength → Enabled

### Run Security Advisor Periodically

_Location: Home → Security Center → Security Advisor_

The [cPanel Security Advisor](https://www.inmotionhosting.com/support/edu/cpanel/how-to-scan-your-server-with-the-cpanel-security-advisor/) in WHM offers configuration recommendations for passwords, cPHulk, MySQL/MariaDB, SSH, SMTP, and more.

**Recommended:** Run the Security Advisor periodically and follow its recommendations.

# ConfigServer Security & Firewall (CSF)

ConfigServer Security & Firewall (CSF) is a versatile server-level firewall with the ability to detect and prevent brute-force login attempts, port scans, and other network-based attacks.

### Check For IPs in RBLs

_Location: Home → Plugins → ConfigServer Security & Firewall_

-   Open **Check for IPs in RBLs**
-   At the bottom, select the frequency of RBLs report and email address to get the report

Another article related with CSF:

-   [CSF Installation](https://www.notion.so/CSF-Installation-bee8e9363afb4fd3a178e8934e11ce68)

# Configure Host Access Control

# Email Authentication

# ModSecurity

[ModSecurity](https://www.inmotionhosting.com/support/security/what-is-modsecurity-and-why-is-it-important/) is generally left alone unless it blocks an important task. If that’s the case, [enable ModSec](https://www.inmotionhosting.com/support/edu/cpanel/how-to-disable-modsecurity-cpanel/) once you’re done. Contact Live Support for assistance troubleshooting the block, and/or consider another method to complete the task to maintain security.

**Recommended:** Keep ModSecurity enabled.

## configserver mod security control

## configserver mail queues

## configserver mail manage

# DNS Records

Enable domain privacy to protect your WhoIs information. Remove old DNS records that are no longer needed. Ask your registrar how to enable DNS security extensions (DNSSEC).

Recommended: Enable DNS security extensions (DNSSEC) when possible via your domain registrar and server or within proxy servers such as Cloudflare.

# PHP Versions

The newest PHP version is PHP 7.3 while 7.2 is the most commonly supported. All older PHP versions should be avoided and removed if not required to run important software.

# Change SSH Port & Disable root Login

# rootkit hunter

# anonymousfox

```php
1) Disable password reset.
2) On WHM list your accounts sorted by contact email, and try to determine if non-sensical addresses are present. Double check and fix what you consider wrong, as they may be already modified.
3) On Apache Configuration, enable Apache Symlink Protection (beware: you need FollowSymlinks and SymLinksIfOwnerMatch active first).
4) On Apache Configuration > Include Editor > Post VirtualHost Include > All Versions, add the below sequence, which are the iThemes htaccess filters, which will stop the most common forms of virus and backdoors with a shot in their feet.
5) Run Imunify AV, even the free version is enough, in all of your accounts, with RapidScan and Binary (ELF) malware detection both enabled, and delete/clean infected files.
```

---

### References

[](https://nixcp.com/whm-security/)[https://nixcp.com/whm-security/](https://nixcp.com/whm-security/)

[](https://www.inmotionhosting.com/support/product-guides/vps-hosting/ways-to-harden-your-vps-hosting/)[https://www.inmotionhosting.com/support/product-guides/vps-hosting/ways-to-harden-your-vps-hosting/](https://www.inmotionhosting.com/support/product-guides/vps-hosting/ways-to-harden-your-vps-hosting/)

[](https://docs.cpanel.net/knowledge-base/security/tips-to-make-your-server-more-secure/#use-secure-passwords)[https://docs.cpanel.net/knowledge-base/security/tips-to-make-your-server-more-secure/#use-secure-passwords](https://docs.cpanel.net/knowledge-base/security/tips-to-make-your-server-more-secure/#use-secure-passwords)

[](https://help.liquidweb.com/s/article/What-is-Hardening-Your-Server)[https://help.liquidweb.com/s/article/What-is-Hardening-Your-Server](https://help.liquidweb.com/s/article/What-is-Hardening-Your-Server)

[](https://support.cpanel.net/hc/en-us/articles/360058051173-What-is-the-anonymousfox-address-on-my-system-)[https://support.cpanel.net/hc/en-us/articles/360058051173-What-is-the-anonymousfox-address-on-my-system-](https://support.cpanel.net/hc/en-us/articles/360058051173-What-is-the-anonymousfox-address-on-my-system-)

#server #whm #cpanel #security 