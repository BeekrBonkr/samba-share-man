# samba-share-man

<div align="center">

<a href="https://ko-fi.com/bkrbnkr"><img alt="Support me on Ko-fi" src="https://img.shields.io/badge/Ko--fi-buy_me_a_coffee-FF5E5B?style=for-the-badge&logo=kofi&logoColor=white"></a>

</div>

A tiny Windows login window for a Samba share. Double-click it, type the
server, your username and password, and it maps the share to a drive letter
and opens it in Explorer. No terminal, no `net use` to remember. I made it
for people on my network who should not have to learn any of that.

It is a single HTML Application file, `CNALX Ninja Login.hta`, with a short
VBScript inside. There is nothing to install.

## Requirements

- Windows. HTAs run through `mshta.exe`, which ships with Windows 10 and 11.
- A Samba or SMB share on the server that is named after the user. The
  script connects to `\\<server>\<username>`.

## Usage

1. Download `CNALX Ninja Login.hta` and double-click it.
2. Fill in the three fields:
   - Server address: hostname or IP of the Samba server. The field comes
     prefilled with a default you can change.
   - Username: your Samba user. It is also used as the share name.
   - Password: your Samba password. It is only passed to Windows for this
     connection and is not saved anywhere.
3. Click Login. Explorer opens on drive `Z:` and the window closes.

If something fails you get a message box with the Windows error text. Check
the server address, username and password first.

## What it does under the hood

When you click Login the script runs, in order:

```
net use Z: /delete /y
net use \\<server> /delete /y
```

to drop any old connection to the same drive letter or server, then maps the
share with `WScript.Network.MapNetworkDrive` using the username and password
you typed (not persistent, so the mapping is gone after a reboot), and finally
starts `explorer.exe Z:`.

To change the drive letter, the default server address or the share path,
open the `.hta` in a text editor. The drive letter is `strDriveLetter`, the
default server is the `value` of the `serverAddress` input, and the share path
is built in the `MapNetworkDrive` line.

---

## Support

<div align="center">

This project is free and open source, and I work on it in my spare time.<br>
If it saved you some time, you can buy me a coffee. No pressure - the code stays free either way.

<a href="https://ko-fi.com/bkrbnkr"><img alt="Support me on Ko-fi" src="https://img.shields.io/badge/Ko--fi-bkrbnkr-FF5E5B?style=for-the-badge&logo=kofi&logoColor=white"></a>

</div>

<!-- more ways to support go here -->
<!-- - [PayPal](...) -->
<!-- - [GitHub Sponsors](...) -->

## License

GPL-3.0, see [LICENSE](LICENSE).
