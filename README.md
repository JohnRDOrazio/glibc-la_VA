# Latin locale as used in the geographical region of the Vatican

Proposed ecclesiastical Latin locale, to enable localization in Latin on Unix systems.

As I started creating localized applications in PHP that had Latin as one of the languages,
I found that I was not able to use either `gettext` or any kind of localization function
(`strftime`, `IntlDateTimeFormat`, etc.) for Latin, since there wasn't an available locale
that could be installed in the system. So even if I created translation strings,
they wouldn't be picked up by `gettext` for the simple fact that `la_VA` was missing from
the system locales.

For the time being, I have generated the locale myself on my server where I host such applications.
My hope is that this locale will be accepted by glibc so as to allow installation in the system.
If anyone has any further contributions, go ahead and open an issue here or better yet,
discuss directly on the [glibc bug report](https://sourceware.org/bugzilla/show_bug.cgi?id=24366).

# How to generate the locale on your system
```bash
$ cd /usr/share/i18n/locales
$ wget https://raw.githubusercontent.com/JohnRDOrazio/glibc-la_VA/main/la_VA
$ localedef -i la_VA -c -f UTF-8 la_VA
```

# Test
Check if the locale is working correctly by outputting the date on the command line:
```bash
$ echo $(LANG=la_VA date '+%A %d %B %Y %H:%M:%S')
```
This should give an output similar to this:
```
Feria II 20 December 2021 05:03:35
```
