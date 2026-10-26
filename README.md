# rCommander

A keyboard- and mouse-friendly file manager that runs in your browser.

Install it on each of your computers, and every one of them shows the drives of the others:
browse, search, view and copy files across all your machines from one window,
also from your phone.

This repository holds the **downloads, help and bug reports**. The source code is not public.

&nbsp;

## Download

Go to [**Releases**](../../releases/latest) and download two files into one folder:

- `rCommander-<version>.zip`
- `SHA256SUMS`

The same zip works on Windows and Linux.

&nbsp;

## Install

**Windows 10 / 11:** unzip, open PowerShell **as administrator** in the unzipped folder, and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\setup.ps1 install -Lan
```

**Linux:** unzip, open a terminal in that folder, and run:

```bash
bash setup.sh install --lan
```

Then open <http://localhost:8223> in your browser.

Leave out `-Lan` / `--lan` if you only want to use rCommander on this one computer.
What it changes, and everything else step by step, is in the
[**install and test guide**](docs/install-and-test-guide.md).

The installer needs the .NET 10 runtime and offers to install it when it is missing.

&nbsp;

## Update and uninstall

Update: download the newer zip, unzip it, and run its `setup.ps1 update` (Linux: `setup.sh update`).
Your settings, bookmarks and index are kept.

Uninstall: run `setup.ps1 uninstall` from the installed program folder (Linux: `setup.sh uninstall`).
Add `-Purge` / `--purge` to delete your rCommander data as well.

Details: [install and test guide](docs/install-and-test-guide.md), Parts 4 and 5.

&nbsp;

## Found a bug? Have an idea?

Open an [**issue**](../../issues/new/choose) and pick *Bug report* or *Idea*.

&nbsp;

## Privacy

rCommander runs on your own computers. It contacts the internet only to:

- check GitHub once a day for updates of the helper programs it manages (ffmpeg, mpv, 7-Zip…),
  and download them when you press Install;
- search and download themes from Open VSX when you open the theme gallery.

Nothing about your files is ever sent anywhere.
