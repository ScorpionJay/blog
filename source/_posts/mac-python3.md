---
title: mac python3
date: 2019-04-07 00:07:52
tags:
---

```
Error: The following directories are not writable by your user:
/usr/local/share/man/man5
/usr/local/share/man/man7

You should change the ownership of these directories to your user.
  sudo chown -R $(whoami) /usr/local/share/man/man5 /usr/local/share/man/man7

And make sure that your user has write permission.
  chmod u+w /usr/local/share/man/man5 /usr/local/share/man/man7
jay:~ jaywang$ sudo chown -R $(whoami) /usr/local/share/man/man5 /usr/local/share/man/man7
```
