rdesktop-colemak
================

This is a hopefully thorough Colemak keymap for rdesktop.

[rdesktop][1] is an open source [Remote Desktop Protocol (RDP)][2] client. It is used to connect to remote Windows sessions, but also to other RDP servers such as the one provided by [VirtualBox][3].

[Colemak][4] is an efficient alternative to QWERTY, similar in intent to Dvorak. It aims to reduce finger and wrist strain, improving typing speed and accuracy while keeping the most important shortcut keys (e.g. ``^X``, ``^C``, ``^V``) in their familiar locations. It is included in several major operating systems including OS X, Debian, Ubuntu, NetBSD and FreeBSD. Windows lacks native support, and consequently so does rdesktop.

To rectify this, the keymap needs to be installed where rdesktop can find it. Note that the definition spans multiple files. This can be done locally:

    $ mkdir -p ~/.rdesktop/keymaps
    $ cp keymap/* ~/.rdesktop/keymaps

Or globally, assuming that rdesktop is installed under ``/usr``. Note that there are other possible locations, e.g. if you have built rdesktop yourself it may be under ``/usr/local`` or ``/opt``:

    $ sudo cp keymap/* /usr/share/rdesktop/keymaps

Using it for an rdesktop session is as simple as:

    $ rdesktop -k colemak servername

At the time of writing, a bug in rdesktop causes a few key combinations to generate the wrong character. The characters in question are not used in English, and are: Ø → ţ, ǵ → ő, ǿ → ˙, Ǩ → č, Đ → ǐ, đ → ǰ and Ǫ → ę.

If you are affected and happy to rebuild rdesktop from source, applying the patch ``keysym_collisions.patch`` fixes this problem. If you are unwilling or unable to build your own rdesktop, you will need to comment out the unwanted characters in the keymap to prevent them clashing with the desired ones. Unfortunately you will not be able to keep both of any pair. The fix has been sent upstream and hopefully will be picked up eventually.

Finally, the official Colemak keymaps for Windows and Mac include an extra dead key, which can be used to type various special characters. If you want to send these via rdesktop from a Unix-like system you will need a way to enter them. One solution is to use [xmodmap][5]. A sample ``xmodmaprc`` is included which shows how to achieve this.

Except where stated otherwise, this work may be used under the same permissive terms as FreeBSD. You will find the necessary legalese in the file ``LICENSE``. Happy hacking!

[1]: http://www.rdesktop.org/
[2]: https://en.wikipedia.org/wiki/Remote_Desktop_Protocol
[3]: https://www.virtualbox.org/
[4]: http://colemak.com/
[5]: https://www.freebsd.org/cgi/man.cgi?query=xmodmap&apropos=0&sektion=0&manpath=X11R7.4&arch=default&format=html
