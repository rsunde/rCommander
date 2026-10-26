# rCommander test guide

This guide walks you through installing rCommander, setting it up, trying every feature,
updating it and removing it again.

Go through it from top to bottom.

Tick each box when the step worked.
When something does not work, write a short note under the step: what you did and what you saw.

&nbsp;

Your name: ______________________

Date: ______________________

Computer: ______________________

rCommander version: ______________________

&nbsp;

---

## Part 1 — Install on Windows

&nbsp;

### Step 1.1 — Remove an old version (skip if rCommander was never installed)

Open **PowerShell as administrator**:
press the Windows key, type `PowerShell`, right-click it, choose **Run as administrator**.

Paste this and press Enter:

```powershell
& "$env:LOCALAPPDATA\Programs\rCommander\current\setup.ps1" uninstall -Purge
```

When it asks, type `DELETE` and press Enter.

- [ ] It finished without red error text.
- [ ] The rCommander icon by the clock is gone.

&nbsp;

### Step 1.2 — Get the files

Download two files from the [Releases page](https://github.com/rsunde/rCommander/releases/latest):

- `rCommander-<version>.zip`
- `SHA256SUMS`

Put both in a new, empty folder, for example `Downloads\rCommander`.

Right-click the zip and choose **Extract All…**, then **Extract**.

- [ ] There is now a folder `rCommander-<version>` next to the zip.

&nbsp;

### Step 1.3 — Install

In the PowerShell window (still as administrator), go to the extracted folder:

```powershell
cd "$HOME\Downloads\rCommander\rCommander-<version>"
```

Then install:

```powershell
powershell -ExecutionPolicy Bypass -File .\setup.ps1 install -Lan
```

`-Lan` lets you use rCommander from your phone and your other computers at home.
Leave it out if you only want it on this computer.

**What `-Lan` changes on your computer, and why**

Without `-Lan`, rCommander only answers this computer itself.
Nothing on your network can reach it.

To be reachable from other devices, three things have to change:

1. **rCommander listens on your network.**
   It starts accepting connections from other devices, not just from this computer.

2. **A shared key is created.**
   This is a long random password that your own rCommander computers use to talk to each other.
   It is stored in rCommander's settings file (`settings.json` in its data folder) and is never shown.
   You copy it to your other computers later (Step 2.3).

3. **Two Windows Firewall rules are added.**
   Windows blocks incoming connections by default, so without these rules nothing gets through.
   You can see them in *Windows Defender Firewall ▸ Advanced settings ▸ Inbound Rules*, group **rCommander**:

   - **rCommander agent (TCP 8223)**: lets browsers and your other computers open rCommander.
   - **rCommander discovery (UDP 9713)**: lets your rCommander computers find each other automatically.

   Both rules apply to **Private** networks only (your home network), never to Public ones
   (a café, a hotel, an airport).
   Uninstalling removes them again.

This is why the install has to run as administrator: only an administrator may add firewall rules.

**It stays safe.** Nothing can be opened from another device without your owner password (Step 2.1),
a guest password, or the shared key.

**If other devices cannot connect:** Windows may have marked your home network as *Public*.
Change it in Windows *Settings ▸ Network & internet ▸ Wi-Fi or Ethernet ▸ (your network) ▸
Network profile type ▸ Private network*.
Settings ▸ Connections in rCommander (Step 2.2) also warns you about this.

If it asks to install the .NET runtime, answer **yes**.

- [ ] The last lines say **rCommander is running** and show an address.
- [ ] An rCommander icon appeared by the clock.

&nbsp;

### Step 1.4 — Open it

Click the rCommander icon by the clock and choose **Open**.

- [ ] rCommander opens in your browser.
- [ ] You can see your drives and folders.
- [ ] **Help ▸ About** shows the version you installed.

&nbsp;

---

## Part 2 — Set it up

Open **Settings**: press `Ctrl+Shift+P`, type `Settings`, press Enter.

&nbsp;

### Step 2.1 — Choose a password

You need this to use rCommander from your phone or another computer.

Go to **Settings ▸ Machine** and set the **owner password** (at least 12 characters).

- [ ] It was saved.

&nbsp;

### Step 2.2 — Check what is missing

Go to **Settings ▸ Connections**.

Every line should be green.
A line that is not green explains what is missing and has a button to fix it.

Press the buttons and follow what they say.

- [ ] Every line is green, or you wrote down which one stayed red.

&nbsp;

### Step 2.3 — Connect a second computer (optional)

With two or more computers, each one shows the others' drives in its panes,
and you can copy files straight from one computer to another.

**What gets copied between the computers: only the shared key.**
All your rCommander computers must have the same key; that is how they recognise each other.
Nothing else is copied: each computer keeps its own owner password, guest password, shared folders
and settings. Your bookmarks and layout follow you anyway.

&nbsp;

#### 2.3.1 — Install on the second computer

On the second computer, do Part 1 with `-Lan`, exactly as on the first
(on Linux: Part 6 with `--lan`).

That install creates a key of its own. You replace it with the first computer's key below.

Also do Step 2.1 there (its own owner password, for signing in from your phone).

- [ ] rCommander runs on the second computer.

&nbsp;

#### 2.3.2 — Copy the key from the first computer

Sit at the **first** computer. This only works in a browser on that computer itself,
not from your phone or another computer.

Go to **Settings ▸ Connections**, find the line **Shared key**, and press **Reveal key…**.
Confirm the warning.

Press **Copy**.

Get the key to the second computer in a way only you can see, for example:

- type or paste it into your password manager, or
- save it in a text file on a USB stick.

Delete that copy once you are done. Anyone with the key can control your rCommander computers.

Press **Hide**.

- [ ] You have the key ready for the second computer.

&nbsp;

#### 2.3.3 — Paste the key on the second computer

On the **second** computer, go to **Settings ▸ Connections**, find **Shared key**,
and press **Use the key from another machine**.

Paste the key and save.

The page now asks for a restart. Press **Restart**. rCommander comes back after a few seconds.

- [ ] The Shared key line is green.

&nbsp;

#### 2.3.4 — Check that they see each other

Wait about 15 seconds.

- [ ] On both computers, **Settings ▸ Connections ▸ Other machines** names the other computer as online.
- [ ] The line **Reachable from other machines** names the other computer with a ✓.
- [ ] In a pane, the machine switcher in the pane header lists the other computer. Open one of its drives.
- [ ] Copy a file from the other computer into a folder here.

**If they do not find each other:**

- Check both networks are *Private* (see "If other devices cannot connect" in Step 1.3).
- Check both keys are the same: paste the key again on the second computer.
- If the computers are on different networks (for example wired and Wi-Fi on separate routers),
  automatic discovery cannot cross. Add the other computer by hand on each side:
  **Settings ▸ Machine ▸ Network ▸ Peers** ▸ add `http://<other computer's name or address>:8223`,
  save, and restart.

**A third computer** works the same way: install with `-Lan`, paste the same key.

&nbsp;

### Step 2.4 — Connect your speakers (optional, needs Music Assistant)

Go to **Settings ▸ Connections ▸ Music Assistant**.

Type the name or address of the computer that runs Music Assistant, and press **Find**.

Open Music Assistant with the link, create a **long-lived token** in your profile there, and copy it.

Paste the token in rCommander and press **Save and test**.

- [ ] It says **connected** and shows your speakers.

&nbsp;

### Step 2.5 — Install the helper programs

Open **Tools ▸ Tools…**.

Press **Install** next to **ffmpeg** (for videos) and **mpv** (for playing music on this computer).

- [ ] Both show as installed.

&nbsp;

---

## Part 3 — Try everything

Use the mouse for everything: menus, buttons and right-click.

Write ✅ when it worked, ❌ when it did not (with a note), ➖ when you skipped it.

&nbsp;

### 3.1 — Moving around

- [ ] Open a drive and some folders, go back and up.
- [ ] Split the window into two panes (right-click a tab).
- [ ] Open several tabs, close one with the middle mouse button.
- [ ] Switch views from the **View** menu: details, thumbnails, folder tree, disk usage.
- [ ] Reload the browser page. You are back where you were.

&nbsp;

### 3.2 — Searching

- [ ] Search for a file name on the whole computer. Results appear right away.
- [ ] Create a file in Windows Explorer. It shows up in rCommander by itself.

&nbsp;

### 3.3 — Working with files

After each of these, press **Ctrl+Z** and check that it was undone.

- [ ] Create a folder and a file.
- [ ] Rename a file.
- [ ] Rename several files at once (**File ▸ Multi-rename**).
- [ ] Copy and move files between the two panes.
- [ ] Copy a file onto one with the same name. It asks what to do.
- [ ] Delete a file. It goes to the recycle bin.
- [ ] Drag files from one pane to the other.
- [ ] Drag a file from Windows Explorer into rCommander.
- [ ] Copy something large. Open the task panel, pause, resume, cancel.

&nbsp;

### 3.4 — Zip files

- [ ] Open a .zip like a folder and open a file inside it.
- [ ] Copy a file into a .zip.
- [ ] Pack a folder into a new zip.
- [ ] Unpack a zip.

&nbsp;

### 3.5 — Looking at files

Select a file and press **Enter**.

- [ ] A text file (with colours).
- [ ] A photo.
- [ ] A PDF.
- [ ] A song.
- [ ] A video (.mp4 and .mkv). Picture and sound play, and jumping ahead works.
- [ ] An e-book (.epub). Close it and open it again: it continues where you stopped.
- [ ] The side panel (inspector) shows details of the selected file.

&nbsp;

### 3.6 — Speakers

- [ ] Right-click a song ▸ **Play on…** ▸ pick a speaker. It plays.
- [ ] Pause, next song and volume work from the bar at the bottom.

&nbsp;

### 3.7 — Extras

- [ ] Convert a video (**File ▸ Convert**).
- [ ] Make a checksum file for a folder, then open it. It says all files are OK.
- [ ] Find duplicate files (disk usage view ▸ **Duplicates**).
- [ ] Compare two folders (**Tools ▸ Synchronize**).

&nbsp;

### 3.8 — From your phone or another computer

Use the address shown at the end of Step 1.3, for example `http://<computer name>:8223`.

- [ ] The sign-in page appears and your owner password works.
- [ ] You can browse folders and play a video.
- [ ] **Settings ▸ User ▸ Devices** on the main computer lists the phone. Press **Revoke**: the phone is signed out.

&nbsp;

### 3.9 — Restart

- [ ] Click the icon by the clock ▸ **Restart**. rCommander comes back by itself.
- [ ] Restart Windows. After signing in, rCommander runs again without you doing anything.

&nbsp;

---

## Part 4 — Update

Download the newer zip and `SHA256SUMS` from the [Releases page](https://github.com/rsunde/rCommander/releases/latest).

&nbsp;

### Step 4.1 — Install the update

Before you start, make a bookmark in rCommander so you can check it survives.

Extract the new zip like in Step 1.2, go to its folder in PowerShell (as administrator), and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\setup.ps1 update
```

- [ ] It finished without red error text.
- [ ] **Help ▸ About** shows the new version.
- [ ] Your bookmark, settings and password are still there.

&nbsp;

### Step 4.2 — Go back to the old version

Run the old version's setup (it is in your install folder; the default one is shown):

```powershell
& "$env:LOCALAPPDATA\Programs\rCommander\<old version>\setup.ps1" update
```

- [ ] **Help ▸ About** shows the old version again, and your things are still there.

Then repeat Step 4.1 to get the new version back.

&nbsp;

---

## Part 5 — Uninstall

&nbsp;

### Step 5.1 — Remove the program, keep your data

```powershell
& "$env:LOCALAPPDATA\Programs\rCommander\current\setup.ps1" uninstall
```

- [ ] The icon by the clock is gone.
- [ ] Opening the rCommander address in the browser no longer works.

&nbsp;

### Step 5.2 — Install again

Repeat Step 1.3.

- [ ] Your settings and bookmarks are back.

&nbsp;

### Step 5.3 — Remove everything

```powershell
& "$env:LOCALAPPDATA\Programs\rCommander\current\setup.ps1" uninstall -Purge
```

Type `DELETE` when asked.

- [ ] Nothing of rCommander is left (no icon, the address does not open).

&nbsp;

---

## Part 6 — Linux

The same zip works on Linux. There is no icon by the clock on Linux; you use rCommander in the browser.

This is the first time rCommander is installed on Linux, so please write down anything odd.

&nbsp;

### Step 6.1 — Install

Put the zip and `SHA256SUMS` in a new folder, open a terminal there, and run:

```bash
unzip rCommander-<version>.zip
bash rCommander-<version>/setup.sh install --lan
```

If it asks to install the .NET runtime, answer **yes**.

On Linux, `--lan` does the same as on Windows (Step 1.3) with two differences:
the shared key is stored in `~/.config/rcommander/agent.env`, readable only by you,
and the firewall is **not** changed for you.
If your computer runs a firewall (ufw or firewalld), the install prints the two commands that open
the same ports (TCP 8223 and UDP 9713). Run them yourself.

- [ ] The last lines say **rCommander is running**.
- [ ] `http://localhost:8223` opens rCommander in the browser.

&nbsp;

### Step 6.2 — Set up and try everything

- [ ] Part 2 (set up).
- [ ] Part 3 (try everything). Deleted files go to the desktop's Trash.
- [ ] Restart the computer and sign in. Write down whether rCommander runs again by itself.

&nbsp;

### Step 6.3 — Update and uninstall

Update with the newer zip:

```bash
bash rCommander-<newer version>/setup.sh update
```

Uninstall, keeping your data:

```bash
bash ~/.local/opt/rCommander/current/setup.sh uninstall
```

Remove everything:

```bash
bash ~/.local/opt/rCommander/current/setup.sh uninstall --purge
```

- [ ] Each of these finished without errors.

&nbsp;

---

## Reporting

For every ❌, write down:

- the step number,
- what you did,
- what you expected,
- what happened (a screenshot helps).

Do not send the file `settings.json`: it contains passwords and keys.

&nbsp;

---

## Good to know

**Installing somewhere else.** To put the program in another folder, add `-InstallDir <folder>` to the install.
Later `update`, `status` and `uninstall` find that install by themselves and reuse its data folder and port; the
first lines they print say where each value came from. Check them before you go on.

**Keeping the data on another disk.** Before installing, run this once, close PowerShell and open it again:

```powershell
[Environment]::SetEnvironmentVariable('RC_DATA_ROOT', 'D:\Data', 'User')
```

**Faster start after a restart (Windows).** Add `-Elevated` to the install command. rCommander then starts
with administrator rights and does not need to re-read your disks after every restart.
