### Prerequisites

Install sendmail package

```bash
sudo yum install sendmail-cf m4 cyrus-sasl-plain
```

Verify email address on Amazon SES & create smtp user

Attach elastic ip address to Amazon EC2 or Lightsail

### Configuring sendmail

1.  Open file `/etc/mail/authinfo`. If it doesn't exist, create it. Add the following block
    
    ```bash
    AuthInfo:email-smtp.us-west-2.amazonaws.com "U:root" "I:smtpUsername" "P:smtpPassword" "M:PLAIN"
    ```
    
    replace the
    
    -   [email-smtp.us-west-2.amazonaws.com](http://email-smtp.us-west-2.amazonaws.com) with AWS SES SMTP endpoint that used
    -   smtpUsername with SES SMTP username
    -   smtpPassword with SES SMTP password
    
    save the file
    
2.  Enter the following command to generate the `/etc/mail/authinfo.db`
    
    ```bash
    sudo sh -c 'makemap hash /etc/mail/authinfo.db < /etc/mail/authinfo'
    ```
    
3.  Enter the following command to add support for relaying to the Amazon SES SMTP endpoint.
    
    ```bash
    sudo sh -c 'echo "Connect:email-smtp.us-west-2.amazonaws.com RELAY" >> /etc/mail/access'
    ```
    
    replace [email-smtp.us-west-2.amazonaws.com](http://email-smtp.us-west-2.amazonaws.com) with AWS SES SMTP endpoint that used
    
4.  Enter the following command to regerenate `/etc/mail/access.db`
    
    ```bash
    sudo sh -c 'makemap hash /etc/mail/access.db < /etc/mail/access'
    ```
    
5.  Enter the following command to backup the `[sendmail.cf](<http://sendmail.cf>)` and `sendmail.mc`
    
    ```bash
    sudo sh -c 'cp /etc/mail/sendmail.cf /etc/mail/sendmail_cf.backup && cp /etc/mail/sendmail.mc /etc/mail/sendmail_mc.backup'
    ```
    
6.  Add the block below to `/etc/mail/sendmail.mc` file before any`MAILER()`definitions
    
    ```bash
    define(`SMART_HOST', `email-smtp.us-west-2.amazonaws.com')dnl
    define(`RELAY_MAILER_ARGS', `TCP $h 25')dnl
    define(`confAUTH_MECHANISMS', `LOGIN PLAIN')dnl
    FEATURE(`authinfo', `hash -o /etc/mail/authinfo.db')dnl
    MASQUERADE_AS(`example.com')dnl
    FEATURE(masquerade_envelope)dnl
    FEATURE(masquerade_entire_domain)dnl
    ```
    
    replace
    
    -   [email-smtp.us-west-2.amazonaws.com](http://email-smtp.us-west-2.amazonaws.com) with AWS SES SMTP endpoint that used
    -   25 with 587
    -   [example.com](http://example.com) with domain that used to send email
    
    save the file
    
7.  Enter the following command to make `sendmail.cf`writeable
    
    ```bash
    sudo chmod 666 /etc/mail/sendmail.cf
    ```
    
8.  Enter the command to regenerate `sendmail.cf`
    
    ```bash
    sudo sh -c 'm4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf'
    ```
    
9.  Reset the permission of [sendmail.cf](http://sendmail.cf) to readonly
    
    ```bash
    sudo chmod 644 /etc/mail/sendmail.cf
    ```
    
10.  Restart the sendmail
    
    ```bash
    sudo /etc/init.d/sendmail restart
    ```
	
#server #sendmail