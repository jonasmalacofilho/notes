Patches
=======

Useful links
------------

Coding style:
	https://www.kernel.org/doc/html/latest/process/coding-style.html

Linux Kernel patch submission checklist:
	https://www.kernel.org/doc/html/latest/process/submit-checklist.html

Linux HWMON patch submission checklist:
	https://www.kernel.org/doc/html/latest/hwmon/submitting-patches.html


Who to send the patch to
------------------------

To: direct maintainers or principal mailing list
Cc: related maintainers, related mailing lists, **yourself**


Git send-email
--------------

Assuming suitable global and local git configs:

```
$ git config --global sendemail.confirm always
$ git config --global sendemail.annotate true
$ git config --global sendemail.suppressfrom false
$ git config --global --unset sendemail.suppresscc

$ git config sendemail.tocmd \
	"`pwd`/scripts/get_maintainer.pl --norolestats --interactive"
$ git config sendemail.cccmd \
	"`pwd`/scripts/get_maintainer.pl --norolestats --interactive"
```

It is sufficient to execute:

```
$ git send-email <patch>
```
