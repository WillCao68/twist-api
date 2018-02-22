# Integrations

Twits has some types of integrations and you have to carefully pick
your type based on how your integration will be used. Here is a link
for the full explanation of each one with a small summary of what they
can do:

* [oAuth 2 applications](#oauth) - Requires more setup but is more powerful
* [Channel integration](#channel) - Has access to one channel only, has schedule powers
* [Thread integration](#thread) - Has access to one thread or create new threads
* [Slash command integration](#slash-command) - Receives a request when called via slash command

And below we have some information shared among all types.


### HTTPS enforcing

Twist enforces HTTPS everywhere, including our production
integrations. It means that all production URLs that communicate with
Twist somehow have to use HTTPS. If you need a certificate, we highly
recommend [Let's Encrypt](https://letsencrypt.org/). Furthermore, we
also enforce
[certificate chain check](https://support.dnsimple.com/articles/what-is-ssl-certificate-chain/).
