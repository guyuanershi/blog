---
title: Update Jenkins SSL Certificate
date: 2018-03-29 14:40:33
tags:
---
Just write something down here. Because I spent a lot of time to figure this out. And fininally, it is so simple~~~~

##Windows
At first, download the cert file from the CA center. There are a lot of types of CA, here I use `.PFX`(PKCS#12) for example.

Go to the `keytool.exe` path (`%PROGRAMFILES{x86)%/Jenkins/jre/bin/`) and using the following cmd.

{% codeblock lang:bash line_number:false %}
$ keytool -importkeystore -srckeystore <path-to-cert-file.pfx> -srcstoretype pkcs12 -destkeystore jenkins.example.com.jks -deststoretype JKS
{% endcodeblock %}

Then copy the jks file to the Jenkins secret path (`%PROGRAMFILES{x86)%/Jenkins/secrets`).
Then modify the jenkins.xml (`%PROGRAMFILES{x86)%/Jenkins/jenkins.xml`)
{% codeblock lang:bash line_number:false %}
--httpPort=-1  (to stop Jenkins from listening over plain HTTP)
--httpsPort=443  (or 8443 or whatever SSL port you want Jenkins to listen on)
--httpsKeyStore="%JENKINS_HOME%\jenkins.example.com.jks"
--httpsKeyStorePassword="<cleartext-password-to-keystore>"
{% endcodeblock %}

At last,
{% codeblock lang:bash line_number:false %}
$ net stop jenkins
$ net start jenkins
{% endcodeblock %}

>So it also can tranform other type to keystore by choicing `-srcstoretype`
>`keytool` is a java's keytool