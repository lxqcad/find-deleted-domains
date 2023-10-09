# find-deleted-expiring-domains
This is a PHP tool which finds recently deleted or expiring domain names that match a certain criteria.
You can set it up as a cron job on your server to check for deleted or expiring domain names.

The tool goes through a list of words from a dictionary and adds TLDs (Top Level Domains) to these words. It then
searches the WHOIS repository to check for domain expiry date. If it is expiring in less than N days (can be set in config file)
or if it has recently been deleted, the domain is listed in the output (or log file). 

You can setup a number of parameters in the config file like max number of characters in domain name (4-8), domain expiring in 
number of days, domains deleted in number of days, frequency of checking TLDs, etc.
You can add a dictionary of words by supplying a plain text file "words.txt" in the root directory of the application. 
You can also specify a list of TLDs you would like checked by adding them to "tlds.txt".

# Installation Instructions

1. Create database using the supplied "whois_one.sql.zip" file by importing it directly to your database
2. Unzip the "whois-complete.zip" to your server.
3. Edit the "config.php" file in the root folder and change the following parameters:
    $approot = "https://emulate.ml/whois"; // URL to the directory....not required
    $dbhost  = 'localhost';    // Unlikely to require changing
    $dbname  = 'whois_one';    // DATABASE NAME
    $dbuser  = 'username';     // DATABASE USER
    $dbpass  = 'password';     // DATABASE PASSWORD 
    
4. Edit the "config" text file in the root folder and change the following:
  # email message
    send_mail_to_name = John doe
    send_mail_to = someone@gmail.com
    mail_subject = Expiring / Deleted domains email report
    mail_body = Report for today is found in the attached text file. <br> Thanks.

  # send email configuration
    mailer_mailhost = smtp.gmail.com
    mailer_userid = somebody@gmail.com
    mailer_password = yourpassword
    mailer_secure = tls
    mailer_port = 587
    mailer_from = somebody@gmail.com
    mailer_from_name = Host Info

5. Delete the "log.txt" file in the root folder and make root folder writable by apache
6. Make sure to give correct permissions to email folder so it is writable by apache
7. Setup cron jobs to run "index.php" twice a week and "email.php" daily at any time convenient to you.
