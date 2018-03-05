# WebSphinx Firefox addon

SPHINX: a password **S**tore that **P**erfectly **H**ides from **I**tself
(**N**o **X**aggeration)

SPHINX is a cryptographic password storage as described in
https://eprint.iacr.org/2015/1099

And as presented by the Levchin Prize winner 2018 Hugo Krawczyk on
Real World Crypto https://www.youtube.com/watch?v=px8hiyf81iM

## What is this thing?

It allows you to have only a few (at least one) passwords that you
need to remember, while at the same time provides unique 40 (ASCII)
character long very random passwords (256 bit entropy). Your master
password is encrypted (blinded) and sent to the password storage
server which (without decrypting) combines your encrypted password
with a big random number and sends this (still encrypted) back to you,
where you can decrypt it (it's a kind of end-to-end encryption of
passwords) and use the resulting unique, strong and very random
password to register/login to various services. The resulting strong
passwords make offline password cracking attempts infeasible. If say
you use this with google and their password database is leaked your
password will still be safe.

How is this different from my password storage which stores the
passwords in an encrypted database? Most importantly using an
encrypted database is not "end-to-end" encrypted. Your master password
is used to decrypt the database read out the password and send it back
to you. This means whoever has your database can try to crack your
master password on it, or can capture your master password while you
type or send it over the network. Then all your passwords are
compromised. If some attacker compromises your traditional password
store it's mostly game over for you. Using sphinx the attacker
controlling your password store learns nothing about your master nor
your individual passwords. Also even if your strong password leaks,
it's unique and cannot be used to login to other sites or services.

## Usage

WebSphinx tries to automatically figure out what you want to do: login, create
a new account or change a password. It tries to figure this out by counting the
number of password input fields that are seen on the page. If this fails then
you can manually insert the password by clicking on the field where you want
the password inserted and on the WebSphinx popup click on **Insert Password**.

If there is a text input field with a username already filled in, then it will
try to find a password for that user to login or change, or create a password
for this user if there is no such user yet associated with the current site by
the password storage. If there is no user to be found in a text field, then you
can enter the user in the WebSphinx popup, or you can select it from a list of
users that the password storage knows about.

## Installation

Currently websphinx is not in the Chrome Web Store, if you want to install itt
follow [these steps](https://stackoverflow.com/questions/24577024/install-chrome-extension-not-in-the-store) with the files in the websphinx directory in this repository - there is no crx file and no need to unpack it thus.

The WebSphinx extension requires the installation of a native messaging host. If you are on Linux or MacOS you need [pwdsphinx](https://github.com/stef/pwdsphinx), if you are on Windows you need [winsphinx](https://github.com/stef/winsphinx).

The windows installer should take care of everything. But if you are on Linux/BSD/MacOS you need to change *%PATH%* in *websphinx.json* so it refers to *websphinx.py* which came with pwdsphinx.

Copy *websphinx.json*, depending on your browser to finish the installation:

- Linux/BSD
  - Per-user: `~/.config/{google-chrome,chromium}/NativeMessagingHosts/websphinx.json`
  - System: `/etc/{opt/chrome,chromium}/native-messaging-hosts/websphinx.json`
- MacOS
  - Per-user: `~/Library/Application Support/{Google/Chrome,Chromium}/NativeMessagingHosts/websphinx.json`
  - System-wide: `/Library/{Google/Chrome,Chromium}/NativeMessagingHosts/websphinx.json`

## Credits

Icon made by Freepik from www.flaticon.com
