# Mutt + Gmail on OSX Yosemite

As a terminal enthusiast and all around hacker my daily work flow includes a bunch of old school software that isn't always super up to date (especially in the OSX world). After upgrading to Yosemite, I ran into some issues with my email setup.

My Mutt setup consists of several Gmail accounts linking up via smtp so naturally this broke after the newest update. From my debugging efforts, I narrowed it down to an error on the ssl side of things, it seems that Gmail's servers were rejecting the ssl handshake from Mutt when sending off emails. After about 6 hours of digging into Mutt and attempting to play with other command line email systems (Sup, Alpine) I ended up switching to msmpt. Quick side note: both Alpine and Sup are not easy to get up and running on OSX, Mutt is far and away the best choice as an OSX hacker for mail.

[Msmtp](http://msmtp.sourceforge.net/) is a terminal based email sending system thats been around for a while, its well supported and maintained. Fortunately, Mutt was designed with a lot of built in support for piping commands to outside programs. By default, Mutt uses sendmail for sending emails through smtp. In your muttrc, you can change the sendmail path to use msmtp. 

## Setting up msmtp

Msmtp is a terminal based mail sending system. You can configure it with a ```$HOME/.msmtprc```

<script src="https://gist.github.com/anonymous/7e3cdd19299932ac41ec.js"></script>

### CA-Certificate Installation

If you have already built and installed a ca-certificate file on your machine, you can skip this step. 

<script src="https://gist.github.com/anonymous/2d16c16f012126b8f066.js"></script>


### Configuring msmtp

You can then add settings for your various smtp accounts by changing ```$HOME/.msmtprc```

<script src="https://gist.github.com/anonymous/1c4c0b83cd18f9641861.js"></script>

You can also use ```password``` if you are comfortable storing your password in in plain text. I recommend using some sort of encryption software (I like [pass](http://www.passwordstore.org/)). 

You can find other msmtp settings [here](http://msmtp.sourceforge.net/doc/msmtp.html#A-user-configuration-file)

### Testing it out

Finally, to test that everything works, you can run the following command to send an email directly through msmtp.

<script src="https://gist.github.com/anonymous/e5ee43604a3ec77d6ce2.js"></script>

## Configuring Mutt to use Msmtp

Mutt pipes email commands to sendmail by default. Simply changing the msmtp path can let you use msmtp for email sending.

<script src="https://gist.github.com/anonymous/a5cb359dd96c42ee1689.js"></script>

### Multiple account configurations

If you are using hooks to switch between accounts (this is another post in and of itself) you can use ```/usr/local/bin/msmtp -a account_name``` to specify the exact msmtp account to be used.

Here's a pretty solid post on setting up [multiple accounts](https://www.df7cb.de/blog/2010/Using_multiple_IMAP_accounts_with_Mutt.html) (their ssl certificate looks to be expired, but it works safely for me)

