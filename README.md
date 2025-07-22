 Email Subscription System
A simple PHP-based system to let users subscribe and receive the latest public GitHub timeline activity via email. Features include email verification, automatic updates every 5 minutes, and easy unsubscription.

Features
Email Verification:
Users submit their email and receive a 6-digit code for verification. On successful verification, their email is stored for updates.

Periodic GitHub Updates:
The system fetches new events from the GitHub public events API every 5 minutes and emails a formatted summary to subscribers.

Easy Unsubscription:
Every update email has a unique "Unsubscribe" link. Users can confirm unsubscription via a verification code.

Folder Structure
text
src/
├── cron.php                # Sends periodic updates (every 5 mins)
├── functions.php           # Mailing, verification, formatting logic
├── index.php               # Subscribe UI
├── unsubscribe.php         # Unsubscribe UI
├── registered_emails.txt   # Local "database" of subscribers
├── setup_cron.sh           # Linux CRON job script (optional)
├── cron.log                # CRON run logs
├── test_fetch.json         # Debugging API fetches
Local Setup (Windows Example)
Requirements
PHP for Windows

MailHog (fake SMTP server for local email)

Web browser

1. Configure PHP for MailHog
In your php.ini file:

text
[mail function]
SMTP = localhost
smtp_port = 1025
sendmail_from = no-reply@example.com

[openssl]
openssl.cafile = "C:\php\extras\ssl\cacert.pem"

[curl]
curl.cainfo = "C:\php\extras\ssl\cacert.pem"
Ensure curl and openssl extensions are enabled.

2. Start Services
Run MailHog:

bash
MailHog.exe
Visit: http://localhost:8025

Start the PHP server:

bash
php -S localhost:8000
3. Subscribe
Visit http://localhost:8000/index.php in your browser.

Enter your email to subscribe.

Check MailHog for the verification email.

Enter the verification code to complete subscription.

4. Simulating Cron Jobs (Windows)
Use Windows Task Scheduler to run:

bash
php src/cron.php
every 5 minutes.
Logs are saved to cron.log.

On Linux, use setup_cron.sh to automate cron setup.

How It Works
Subscribe
Submit your email via the site UI. A 6-digit code is sent for verification.

Receive Updates
Every 5 minutes, subscribers get a summary of the latest GitHub public events.

Unsubscribe Anytime
Use the unsubscribe link in any email, enter your email, and confirm with a code to be removed.

Sample Email Formats
Verification Email:

xml
<p>Your verification code is: <strong>123456</strong></p>
GitHub Updates:

xml
<h2>GitHub Timeline Updates</h2>
<table border="1">
  <tr><th>Event</th><th>User</th></tr>
  <tr><td>PushEvent</td><td>octocat</td></tr>
</table>
<p><a href="unsubscribe_url" id="unsubscribe-button">Unsubscribe</a></p>
Unsubscribe Confirmation:

xml
<p>To confirm unsubscription, use this code: <strong>654321</strong></p>
