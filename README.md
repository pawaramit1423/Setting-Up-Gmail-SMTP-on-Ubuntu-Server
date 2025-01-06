# Setting-Up-Gmail-SMTP-on-Ubuntu-Server

Certainly! Here's a README file formatted for GitHub that incorporates all the steps to set up Gmail SMTP on an Ubuntu server.

# Setting Up Gmail SMTP on Ubuntu Server

This guide provides a step-by-step process to configure Gmail SMTP on your Ubuntu server using Sendmail. By following these instructions, you will be able to send emails via your Gmail account from your Ubuntu server.

## Prerequisites

- An Ubuntu server
- A Gmail account
- Basic knowledge of terminal commands

## Step-by-Step Instructions

1. **Update Your Package List**

   ```bash
   sudo apt update
   ```

2. **Install Required Packages**

   ```bash
   apt install mailutils
   sudo apt-get install sendmail
   ```

3. **Configure Sendmail**

   ```bash
   sudo sendmailconfig
   ```

4. **Navigate to the `/etc` Directory**

   ```bash
   cd /etc/
   ```

5. **View the Hosts File**

   ```bash
   cat hosts
   ```

6. **Change Directory to Mail Configuration**

   ```bash
   cd /etc/mail/
   ```

7. **Create a Local Host Names File**

   ```bash
   touch local-host-names
   ```

8. **View the Local Host Names File**

   ```bash
   cat local-host-names
   ```

9. **Create the Authentication Directory**

   ```bash
   mkdir /etc/mail/auth
   ```

10. **Change Directory to the Auth Directory**

    ```bash
    cd /etc/mail/auth
    ```

11. **Create Client-Info File**

    ```bash
    touch client-info
    ```

12. **Edit the Client-Info File**

    ```bash
    vim client-info
    ```

    Add the following line, replacing fields with your credentials:

    ```
    AuthInfo:smtp.gmail.com "U:root" "I:YOUR_MAIL@gmail.com" "P:YOUR_APP_PASSWORD" "M:LOGIN"
    ```

13. **Create the Hash Map from Client-Info**

    ```bash
    makemap hash client-info < client-info
    ```

14. **Edit the Sendmail Configuration File**

    ```bash
    vim sendmail.mc
    ```

    Add the following lines:

    ```bash
    dnl # Default Mailer setup
    MAILER_DEFINITIONS
    define(`SMART_HOST',`smtp.gmail.com')dnl
    define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
    define(`RELAY_MAILER',`esmtp')dnl
    define(`RELAY_MAILER_ARGS', `TPC $h 587')dnl
    FEATURE(`authinfo',`hash /etc/mail/auth/client-info')dnl
    MAILER(`local')dnl
    MAILER(`smtp')dnl
    ```

15. **Build the Configuration Files**

    ```bash
    make
    ```

16. **Reload Sendmail Service**

    ```bash
    /etc/init.d/sendmail reload
    ```

17. **Check Mail Queue**

    ```bash
    mailq
    ```

18. **View Mail Log**

    ```bash
    cat /var/log/mail.log 
    ```

19. **Check Sendmail Service Status**

    ```bash
    service sendmail status
    ```

20. **Test Your Setup**

    Send a test email:

    ```bash
    echo "Hello, I am from $(hostname)" | mail -s "Testing Gmail Setup on Ubuntu Server" amit61508@gmail.com
    ```

## Conclusion

You have successfully configured Gmail SMTP on your Ubuntu server using Sendmail. You can now send emails directly from your server using your Gmail account. Make sure to replace any example email addresses and passwords with your actual details.

For any issues, refer to the mail log located at `/var/log/mail.log` to troubleshoot.
```

You can save this text into a file named `README.md` in your GitHub repository. Adjust the content as needed to fit your project's style or requirements!
