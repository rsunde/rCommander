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

**Honest note:** rCommander has so far been tested with two computers (a Windows PC and a Linux server).
More should work the same way but has not been tried; if you connect three or more, please report how it went.

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

### Step 4.1b — Update from inside rCommander

You need an install that is at least one release behind the newest one. These steps start from the older version; install it first with Part 1 if needed. Do each case that fits your machine.

**Windows, logon tasks not elevated (the default install).**

- [ ] The top bar shows an **Update** chip within a day, or right away after **Help ▸ Check for updates…**.
- [ ] The dialog lists every release newer than yours, newest first, with what changed.
- [ ] Click **Update**. The task panel shows the download, the check and then "restarting". No window stays open.
- [ ] After less than a minute the page reloads on its own and **Help ▸ About** shows the new version.
- [ ] Your bookmarks, settings and password are still there, and the tray icon is back (once, not twice).

**Windows, installed with `--elevated`.** Repeat the cases above.

- [ ] The update works without a UAC prompt, and the agent and tray come back elevated.
- [ ] Sign in to Windows as a user who is not an administrator, if you have one, and open rCommander. If it refuses and shows a command to run in an administrator PowerShell, run that command and check the version.

**Windows, installed with `-NoAutostart`.**

- [ ] The update works, and afterwards the agent is running but no logon task exists (check with `setup.ps1 status`).

**Linux, user install (`bash setup.sh`).**

- [ ] The update works the same way, and `setup.sh status` shows the new version.
- [ ] After the update the agent still runs when you close the terminal you started it from.

**Linux, `--system` install.**

- [ ] The dialog shows no Update button, only a `sudo` command. Copying it and running it in a terminal updates the install.

**Folders with spaces in their names.** The update hands over to a one-shot task on Windows (`conhost.exe --headless powershell.exe`) and to `systemd-run --user` on Linux; whether they pass paths with spaces through intact has not been tried yet. Use a fresh test install for this case and uninstall it after (`uninstall` with the same folder options).

- [ ] Windows: install the older version with both folders containing a space:
  `powershell -ExecutionPolicy Bypass -File .\setup.ps1 -InstallDir 'C:\rc test\program files' -DataDir 'C:\rc test\data folder'`.
  Update from inside rCommander. The page reloads on the new version, `setup.ps1 status` shows it,
  `C:\rc test\data folder\updates\<new version>.log.exit` holds `0`, and the scheduled task `rCommander Update` is gone.
- [ ] Linux: `RC_DATA_ROOT="$HOME/rc test/data root" bash setup.sh install --install-dir "$HOME/rc test/program files"` (there is no data folder option; keep `RC_DATA_ROOT` exported in that shell for later `status`/`uninstall` runs).
  Update from inside rCommander. The page reloads on the new version, `setup.sh status` shows it, and
  `$HOME/rc test/data root/rCommander/updates/<new version>.log.exit` holds `0`.

**Skip this version.**

- [ ] Click **Skip this version** in the dialog: the chip goes away. A newer release than the skipped one shows the chip again.

**What's new after the update.**

- [ ] The first time you open rCommander after an update, a notice shows what changed since the version you had before. It does not show again.
- [ ] **Help ▸ What's new** shows the notes of the running version at any time.

**Refusals.**

- [ ] Start two updates quickly (two browser tabs): the second says one is already running.
- [ ] Turn the network off before clicking Update: the task fails with a clear message and the old version keeps running.

**Update all, with a second machine.** Both machines must be on the older version and see each other (Part 2.3).

- [ ] **Help ▸ About ▸ System** lists both machines with their versions, and marks an older one.
- [ ] Click **Update all**: the other machine updates first, then this one. The task panel follows each, and the page reloads when this machine is on the new version.

&nbsp;

### Step 4.1c — A failed task is still readable after the update

Do this on the update from Step 4.1b, or on any restart of the agent.

- [ ] Before updating, make a task fail (copy a file into a folder you have no permission to write to, or to a full disk). Note its name.
- [ ] After the update or restart, open the task panel. The failed task is still listed with its error, and its console shows what it printed.
- [ ] **Export log** on it contains the console, the error and a timeline.
### Step 4.2 — Go back to the old version

Run the old version's setup (it is in your install folder; the default one is shown):

```powershell
& "$env:LOCALAPPDATA\Programs\rCommander\<old version>\setup.ps1" update
```

- [ ] **Help ▸ About** shows the old version again, and your things are still there.

Then repeat Step 4.1 to get the new version back.

You can also go back from inside rCommander:

- [ ] **Help ▸ Check for updates…** offers **Go back to <old version>**. After you click it, the old version is running again and your things are still there. If the old version is 0.1.3 or older, rCommander refuses and shows the command to run by hand (as above).

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

## Part 7 — Machine colours and the flagship

Needs two machines with rCommander 0.1.5 on the same network, LAN mode on with the same shared key (call them machine A and machine B), and ideally a third machine still on 0.1.4 (machine C).

1. Open rCommander on machine A and look at Help > About > Machines (one card per machine). - [ ] Both machines are listed, each with a coloured mark beside its name.
2. Open rCommander on machine B. - [ ] Both machines show the same two colours as on machine A, within about 10 seconds. - [ ] The two colours differ.
3. Open a pane on each machine in turn. - [ ] A thin stripe in the machine's colour runs along the top of the pane. - [ ] Hovering a mark shows the machine's name and its colour name.
4. Settings > Appearance > Machine colours: choose "Marks only", then "Off", then back to the default. - [ ] The stripe goes first, then the marks; the names stay.
5. On machine A, right-click machine B in the machine picker, choose Change colours... and pick a free colour. - [ ] Within about 10 seconds machine B has the new colour on both machines.
6. Change colours again and pick the colour machine A has. - [ ] The dialog offers Swap or Pick another. Choose Swap. - [ ] The two machines have traded colours on both screens.
7. Make machine A the flagship (Help > About > Machines > Make this the flagship; on a machine that is not the flagship the button may read "Take the flag from ..." once another machine holds it). - [ ] A flag appears before machine A's name on both machines.
8. On machine B choose Take the flag from machine A and confirm. - [ ] The flag moves to machine B on both machines.
9. Split: disconnect machine B from the network (unplug or turn off Wi-Fi). On machine A make A the flagship; on machine B make B the flagship. Reconnect machine B. - [ ] Within about a minute both machines agree on one flagship, the one set last. - [ ] The machine that lost the flag shows one notice saying the other took the flag while you were apart.
10. If machine C (0.1.4) is available, start it on the same network. - [ ] Machines A and B list machine C and give it a colour within about a minute. - [ ] Machine C keeps working normally (browse, copy). - [ ] After updating machine C to 0.1.5 it shows the same colour.
11. Shut machine B down. On machine A open Help > About > Machines. - [ ] Machine B is shown as offline with Forget machine.
12. Choose Forget machine for machine B. - [ ] Its card is gone and its colour is free.
13. Start machine B again. - [ ] It comes back with a colour of its own within about 20 seconds.
14. While machine B is running, forget it from machine A (right-click its mark > Forget machine). - [ ] Machine B takes a colour again within about 20 seconds and is never left without one.

&nbsp;

---

## Part 8 — The dock: moving and resizing panels

Needs rCommander 0.1.5 open in a desktop browser, signed in as the owner. A second browser (or a private window) signed in as the owner is used in step 9, and a guest sign-in in step 10.

1. Open View > Panels and show the Inspector, Tasks and Playback panels. - [ ] Each one appears and its entry is checked.
2. Drag the Inspector by its header to the left edge of the window. - [ ] A highlight shows a left-edge target while you drag. - [ ] After you drop, the Inspector sits on the left. Repeat for the right, top and bottom edges; it follows each time.
3. Drag the Tasks panel onto the Inspector's header. - [ ] The highlight shows a tab insert marker. - [ ] Both panels share the zone as tabs; dragging a tab out again splits them apart.
4. Drag the Playback panel onto the lower half of the zone. - [ ] It stacks beneath the others. - [ ] The boundary between stacks moves when dragged, with the arrow keys, and resets on double-click.
5. Drag a panel to the middle of the window away from every edge. - [ ] It becomes a floating window. - [ ] Move it by its header and resize it by its edges and corners; it cannot be dragged fully off-screen.
6. Drag a panel by its header onto a pane's tab bar. - [ ] It becomes a tab beside the file tabs. - [ ] Drag that tab back to a side; it returns to the dock. - [ ] Right-click the panel's tab: the menu offers move, float, collapse and hide.
7. Resize a side by dragging its inner edge, then double-click the edge. - [ ] The size changes while you drag. - [ ] Double-click returns it to the default size. - [ ] A side cannot be made wider than about 70 % of the window.
8. Collapse a side and a single stack (the collapse button on the header). - [ ] Each becomes a labelled strip, tall at the left and right, wide at the top and bottom. - [ ] Clicking a strip opens it again. - [ ] With a job running, the collapsed task strip shows its progress.
9. Start dragging a panel, then switch to another window with Alt+Tab and back. - [ ] The drag has ended, the panel stayed where it was and nothing is stuck. Press Esc during another drag. - [ ] The drag is cancelled and nothing moves.
10. Reload the page. - [ ] Every panel is where you left it, with the same sizes. Open the same session in the second browser. - [ ] It shows the same layout, and a move in one browser shows up in the other within a couple of seconds.
11. Use View > Panels > Move panel to… with the keyboard only. - [ ] The dialog lists the places and moves the focused panel. - [ ] F6 moves the focus from one open panel to the next.
12. Open Personalities, arrange the panels, save a personality, change the layout, then apply the saved personality. - [ ] The saved arrangement comes back (floating windows excepted).
13. Sign in as a guest in another window. - [ ] The owner-only panels (Tasks, Undo history, Script console, Playback, Scripts and Tools) are not offered, in View > Panels or the activity bar. - [ ] The guest can still move and resize the panels it has, and its layout stays in that browser only.

&nbsp;

---

## Part 9 — Open files in their apps

Needs rCommander 0.1.5 signed in as the owner in a browser on the same computer as the agent. Steps 1-4 use a Windows computer with an install made with the elevated option; steps 5-8 also need a second machine running rCommander (machine B) and a phone or another computer (step 7 also an SMB share on machine B); steps 9-10 need a Linux computer. Report problems as described under Reporting.

1. Select a `.txt` file and press Shift+Enter, then do the same with a `.docx` file. - [ ] Each opens in the app Windows has registered for it, on your screen. - [ ] In Task Manager > Details, add the "Elevated" column: the app shows **No**.
2. Open a `.jpg`, a `.json` and a `.txt` with Shift+Enter, with the agent started by `just run` and by the logon task. - [ ] Each app appears in front of the browser, not behind it (if it is behind, say so and send the agent log line starting `Open:`). - [ ] It appears at once (no 10-second wait, no "Explorer did not answer" error). - [ ] The File menu and the item context menu offer no "Open with..." (taken out 2026-11-10: Windows does not show its app chooser for the background agent). Press Shift+Enter on a file whose type has no app (for example a `.nfo` on a fresh Windows). - [ ] A message says "No app is registered for .nfo files on <this machine>.", nothing opens, and no Windows error or dialog appears. - [ ] The agent log line reads `Open NoApp ...`.
3. Select a `.ps1` file and press Shift+Enter. - [ ] A dialog says the file is a script and that opening it runs it. - [ ] Cancel opens nothing. - [ ] Run opens it.
4. Select an image and press Enter. - [ ] It opens in the built-in viewer. Select a file the viewer cannot show (for example a `.docx`) and press Enter. - [ ] It opens in its app, not as a download. Set Settings > Files and lists > Enter on a file to "Always the system app" and press Enter on the image. - [ ] It opens in its app. Set the choice back.
5. On a phone or another computer, open rCommander from this machine's address and sign in as the owner; select a file and choose Open with default app from the context menu. - [ ] The message says the app would open on the machine's screen, not on this device, and offers Download. - [ ] Download saves the file. - [ ] Nothing opens on the machine's own screen. Press Enter on a file the viewer cannot show. - [ ] It downloads.
6. On the machine from step 1, browse to a file on machine B in a folder that no SMB share of machine B covers, and open it with Shift+Enter. - [ ] It opens in the app, and a toast says it opened a copy, says why (no network share on machine B reaches the file), that changes stay in the copy, and that sharing the folder over SMB avoids copies. Edit the file in the app and save. - [ ] The toast's Copy back starts a copy to machine B, and the normal overwrite question appears.
7. Network shares first. Pick a folder on machine B that its file server shares over SMB under the folder's own name although machine B's rCommander does not list it under Settings ▸ Machine ▸ Sharing (for example Samba running in a container), so that `\\<machine B>\<share>` opens in Explorer. In rCommander, open `\\<machine B>` in a pane. - [ ] The shares Explorer shows are listed (a note says machine B's agent announces none). Browse to a file inside that folder by machine B's own path (not the `\\` one) and press Shift+Enter. - [ ] It opens in the app directly, no copy is made, and a toast says "Opened over SMB: \\<machine B>\<share>\…". - [ ] **Copy full path** on that file gives the same `\\` path. If Windows refuses to list machine B's shares, map the share to a drive letter instead (`net use Z: \\<machine B>\<share>`) and repeat: - [ ] it opens through the mapped drive (toast "Opened through the network mount: Z:\…"). - [ ] A file whose copy on the share differs in size or time from machine B's own is never opened from the share: it opens as a copy whose toast says the share's file differs.
8. Open Tools > Opened copies... - [ ] The copy is listed with its source machine, when it was opened and "changed". - [ ] Open again, Show folder and Copy back work. - [ ] Remove fails with a message while the app still has the file open, and works after you close it.
9. On a Linux desktop with the user-service install, open a `.txt` file with Shift+Enter. - [ ] It opens in the registered app. - [ ] Open with... is not offered. - [ ] A file with the executable bit asks first, like step 3. If machine B's share is mounted here (`mount -t cifs` or an NFS mount of the same folder), open a file of machine B inside it with Shift+Enter: - [ ] it opens from the mount, without a copy.
10. On a Linux machine without a desktop (a server, or a system-wide install), press Shift+Enter on a file. - [ ] The toast says "No desktop on this machine". Now reach that machine's rCommander through an SSH tunnel to its loopback port and press Shift+Enter again. - [ ] The browser counts as local (the tunnel arrives on loopback), so it gets the same "No desktop" answer; on a machine with a desktop the app would start on that machine's own screen, not on yours.
11. Open the agent's log after the steps above. - [ ] There is one `Open` line for every attempt, refused ones included, naming the result, the path, the route (`route=announced`, `discovered`, `mounted`, or `none` for a local file or a copy) and where the request came from.

&nbsp;

---

## Part 10 — Honest status

Needs rCommander 0.1.5 on two machines in LAN mode (machine A on Windows, machine B on Linux, called the peer below), signed in as the owner in a browser on A, and the tray running on A. Step 9 needs a Windows install whose agent the setup script's logon task started. Report problems as described under Reporting.

1. Open the machine picker on A. - [ ] Both machines are online (green). - [ ] The pane header and Help > About > Machines agree.
2. On the peer, block the agent's TCP port: on Windows disable the firewall rule `rCommander agent (TCP 8223)`, on Linux run `sudo ufw deny 8223/tcp`. - [ ] Within 10 seconds the peer shows "unreachable: does not answer (timeout)" or "refuses connections on port ...", not online. - [ ] The tray icon turns amber and its Machines submenu names the peer and the reason. - [ ] A pane showing a folder on the peer shows the error. Remove the block. - [ ] The peer is online again within 10 seconds and the tray icon is back to normal.
3. Start a copy to the peer, then unplug the peer's network cable or turn off its Wi-Fi. - [ ] Within 20 seconds the peer reads "offline - last seen ...". - [ ] The task panel shows "no contact with <peer> since ..." and the job's speed leaves the combined rate. Plug the network back in. - [ ] The job carries on and the message goes away.
4. On the peer set a different `Agent:SharedKey` and restart it. - [ ] A's list shows "rejects this machine's key (the shared keys differ)". Put the original key back. - [ ] It is online again.
5. With the web page open on A, choose Stop agent in the tray menu. - [ ] A banner says "agent not answering since ...", every other machine reads "unknown" in amber with a dimmed mark, the tray icon is red and its tooltip says "agent not answering since ...". - [ ] The tray menu shows the last known machines, jobs and drives marked "as of ...". Start the agent. - [ ] The banner says the agent is back, then goes away.
6. On Linux run `sudo sysctl fs.inotify.max_user_watches=1024` and restart the agent. - [ ] The index dot is not green and its popup says "No live updates on ... - re-checked ...". - [ ] A pane on `/home` says "live" (own watcher) or "read hh:mm - not watched" with the reason, never plain "live" without changes arriving. - [ ] Search below `/` says "from index (re-checked ...)"; Search the disk finds a file you created a moment ago. Restore the limit and restart the agent. - [ ] The dot turns green again.
7. Open Settings > Connections. - [ ] "Reachable" shows "checked ... ago". Leave the page open for 11 minutes and reopen it. - [ ] The check has run again.
8. With Music Assistant connected, cut the network of the machine that runs it. - [ ] Within 40 seconds the speaker picker and Connections show it as unreachable, not connected. Reconnect it. - [ ] Players come back.
9. Start the tray on Windows after the setup script's logon task started the agent. - [ ] "Restart agent" is enabled. - [ ] Choosing it restarts the agent and the web page reconnects. - [ ] Open the tray menu and leave it open while you stop and start the agent from another window. Does the open menu repaint with the new text, or only on the next open? This is not verified in code: write down what you see.
10. Start a copy job, close the web page, and open the tray menu. - [ ] The Jobs submenu lists the job with its progress. - [ ] Clicking it opens the web page on that job in the task panel.

## Part 11 — Logs, problem reports and storage

Needs rCommander 0.1.5 signed in as the owner in a browser on the same computer. None of this has been tried on a real computer before, so be exact and write down what you see. Steps 7 to 9 need a spare folder on another disk or partition. Report problems as described under Reporting.

1. Open **Settings ▸ Machine ▸ Logs**. - [ ] The log level, how long to keep files, the total size limit and the console size per task are there. - [ ] **Open logs folder** moves the focused pane to the `logs` folder inside your data folder, and it holds a file named `agent-` and today's date.
2. Choose **Help ▸ Open logs folder**. - [ ] The focused pane goes to the same folder. Stop the agent (tray ▸ Stop agent) and choose **Open logs folder** in the tray menu. - [ ] The tray opens the folder in the system file manager, with the agent stopped. Start the agent again.
3. Choose **Help ▸ Report a problem...**. Type "test" in the box. - [ ] The window shows "Nothing is sent by rCommander" before any button. - [ ] After Build, a list of files with sizes appears (`summary.txt`, `setup.txt`, `agent.log`, `config.txt`, at least). - [ ] Click each file: its text shows, and your folder names, computer names and addresses appear as things like `d1`, `machine-1`, `ip-1`. - [ ] Look for your user name, a computer name and a password or key anywhere in the files. Write down any you find, even a single word.
4. Untick **Mask paths, names and addresses** and look again. - [ ] The real names show, but passwords and keys still read `***`. Tick it again.
5. Click **Save bundle...**. - [ ] A zip named `rcommander-report-` with the date and time downloads. - [ ] Open it: the files are the ones you previewed. Click **Open GitHub issue**: - [ ] A new GitHub page opens with the form filled in, and "Diagnostics bundle" says to drag the zip into the box. Close it without sending.
6. Make a task fail, right-click it. - [ ] **Report this...** is there, and the window offers "This job". Build it. - [ ] `job.log` holds the console and the error. Then stop the agent from Task Manager or with `kill -9` (not the tray), start it again and reload the page. - [ ] A message says rCommander stopped unexpectedly last time and offers **Report...**. - [ ] **Report...** builds a bundle that covers the minutes before the stop. - [ ] The message does not come back after you dismissed it and reloaded.
7. Open **Settings ▸ Storage**. - [ ] The data folder, where that choice comes from and the free space are shown. - [ ] Every row says whether it can be rebuilt, is history or is yours, and the sizes add up to about the folder size in your file manager. - [ ] Click Clean on the thumbnail row: the text before the click says what goes and what stays, and afterwards "Freed ..." appears. - [ ] The Yours rows have no Clean button.
8. **Move the data, Windows.** Click **Move...**, enter an empty folder on another drive. - [ ] It refuses a folder that is not empty or has too little free space. - [ ] The commands stop the agent, wait for it, copy with robocopy, check the result and run `setup.ps1 update -DataDir`. Run them in PowerShell. - [ ] The agent comes back, **Settings ▸ Storage** shows the new folder, and your bookmarks, settings and the failed task from step 6 are still there. - [ ] Make the copy fail (fill the target or unplug it) and run again: the commands stop before the setup step and the old folder is untouched. Move the data back the same way.
9. **Move the data, Linux user install.** Same as step 8. - [ ] The commands stop the agent, wait until its port is free, copy with `cp -a` and run `setup.sh update` with `Agent__DataDirectory` set. - [ ] Afterwards the agent runs on the new folder and the old one is unchanged. On a `--system` install: - [ ] **Move...** shows no commands and explains that the folder is fixed and how to move it by hand.
10. In **Settings ▸ Storage** set a budget a little below the total of the History and Rebuildable rows. - [ ] Within about 10 minutes the page lists "Recent cleans" saying what was cleared and how much, and the total comes down. - [ ] Today's log file and your recent tasks are still there. Set the budget back to 0.

&nbsp;

---

## Part 12 — New in 0.1.6

Needs rCommander 0.1.6 signed in as the owner. Steps 1 to 4 and 8 need two machines in LAN mode with the same shared key (machine A, where your browser runs, and machine B); step 1 is best done while machine B still runs 0.1.5. Report problems as described under Reporting.

1. **Update every machine.** Open **Help ▸ About ▸ Machines**. - [ ] Each machine shows its version and when it last checked for a new release. - [ ] **Check now** on a machine changes that time. - [ ] A machine that was never checked or cannot be reached reads as unknown, never as up to date. Click **Update all**. - [ ] Every machine checks first, then the other machines update before this one, and the page comes back on the new version.
2. **Roll back one machine.** On machine B's card click **Roll back**. - [ ] It asks first. - [ ] Machine B comes back on its previous version and the card says so. Update it again from its own card. - [ ] A machine that cannot be updated with one click (for example a Linux system install) shows why and the command to run by hand, instead of a button.
3. **Machine properties.** Right-click machine B in a pane header, in the machine picker and in the folder tree, and choose **Properties...**. - [ ] Each time **Help ▸ About ▸ Machines** opens on machine B's card. - [ ] With machine B stopped, the card says why it is not online.
4. **Jobs on other machines in the tray.** Start a large copy on machine B (from the browser, with machine B as the target). Open the tray menu on machine A ▸ **Jobs**. - [ ] The job is listed under a line with machine B's name. - [ ] Clicking it opens rCommander with the task panel on that job. - [ ] With machine B stopped, the tray says machine B's jobs could not be read, instead of showing nothing.
5. **Opened copies.** Open a file from machine B with **Shift+Enter**, close the app, and open the same file again. - [ ] The second open is quick: the copy on this computer is reused, not downloaded again. Edit and save the copy, then open the file again. - [ ] A fresh copy opens and your edited one is kept. Open **Tools ▸ Opened copies...**. - [ ] It shows how many copies there are and how much space they take. - [ ] **Remove all unchanged** removes only the copies you did not edit. - [ ] **Remove all, losing changes** asks once, names how many edited copies go, and then removes them. In **Settings ▸ Storage**: - [ ] the "Opened copies" row's Clean removes unchanged copies only.
6. **Open in the default app on Windows.** Repeat Part 9 step 2. - [ ] Each app comes to the front. - [ ] A file type with no app says so, with no Windows error. - [ ] No "Open with..." entry is offered anywhere.
7. **Folder sizes and the index dot.** Hover a folder's size in a file list, then in the thumbnail grid. - [ ] The tooltip says where the number comes from and how old it is, for example "From the index, as of 14:03 (3 min ago)". - [ ] It mentions the index still building only while it really is. On Windows, look at the index status dot after the first check of `C:\`. - [ ] It does not stay blue because of folders such as `C:\Windows\CSC` or System Volume Information. Click the dot, untick that drive and tick it again. - [ ] A real "partial" warning (folders you yourself cannot open), if there was one, is still shown afterwards.
8. **SMB shares and network paths.** On machine B open **Settings ▸ Machine ▸ Sharing** and add a share that its file server really serves (name, folder, read-only). On machine A, in a pane on machine B inside that folder, choose **Copy full path** on a file. - [ ] The clipboard holds a path starting with two backslashes and machine B's name. - [ ] **Shift+Enter** on a file there opens it in place, without copying the whole file first. - [ ] Outside a shared folder, Copy full path gives machine B's own path.
9. **Dialogs.** Open **Help ▸ About**, then a copy dialog (**F5** in the Total Commander layout). - [ ] They are bigger than in 0.1.5 and never larger than the window. - [ ] Dragging the grip in the bottom-right corner resizes them, and Alt+arrow keys do too (Shift+Alt for bigger steps). - [ ] Close and reopen: the size is kept for that dialog. - [ ] In the Columns dialog (**View ▸ Columns**), Alt+↑/↓ moves a column and does not resize the dialog. - [ ] The copy dialog shows each machine's colour mark beside the source and the target, dimmed for a machine that is not online.
10. **Multi-rename.** Mark a few files and open multi-rename. - [ ] The preview's Old name and New name columns can be dragged wider or narrower, and double-click fits them. - [ ] Names stay on one line, with the full name on hover. - [ ] "Changed only" hides the rows that do not change.
11. **Speakers (needs Music Assistant).** In **Settings ▸ Connections**, give Music Assistant a wrong token and save. - [ ] The speaker picker and Settings keep saying the token was refused, with the time it was first refused, for a few minutes; they never switch to "not reachable" in between. Put the right token back.

&nbsp;

---

## Part 13 — New in 0.1.7

Needs rCommander 0.1.7 signed in as the owner, in Chrome or Edge. Steps 3 to 6, 10, 15 to 18, 26 and 31 need two machines in LAN mode with the same shared key (machine A, where your browser runs, and machine B). rCommander across several machines has only ever been tested with two, so these steps use two; with more machines, write down what you see. Step 32 needs Music Assistant. Report problems as described under Reporting.

1. **Install it as an app.** On machine A open rCommander at `http://localhost:8223` (the default port; use yours if you changed it). Choose **Help ▸ Install rCommander as an app...**. - [ ] The dialog says "Install rCommander as an app" with an **Install** button, or "Install from the browser" if the browser keeps its own offer in the address bar. Install it (the button, or the install icon at the right of the address bar). - [ ] rCommander opens in its own window, without the browser's tabs and address bar. - [ ] The Start menu (Windows) or the app launcher (Linux) lists "rCommander" with the rCommander icon. - [ ] In the app window, **Help ▸ Install rCommander as an app...** says "rCommander is running as an app." Close the window and start it from the Start menu. - [ ] It opens where you left off.
2. **Only localhost installs.** On machine A open rCommander at machine B's LAN address (for example `http://192.168.1.20:8223`). Choose **Help ▸ Install rCommander as an app...**. - [ ] The dialog says "This address cannot install apps", names that address, and tells you to open `http://localhost:<port>` on that computer instead. In Firefox: - [ ] the dialog says "This browser cannot install apps" and suggests Chrome or Edge.
3. **A request for a machine that is switched off.** Open a pane on machine B and show a folder with a test file in it. Stop the agent on machine B (or switch the machine off) and wait until its mark in the pane header is dimmed. Rename the test file in that pane. - [ ] A toast says machine B "is offline. Held: it will be sent when ... is back." with a **Cancel** button. - [ ] The task panel shows the rename as "waiting for machine B". - [ ] The row of the file is not dimmed or locked. Start machine B's agent again. - [ ] Within a few seconds the row reads "checking…", then "sent, running on machine B", then the job ends Completed. - [ ] The file is renamed once on machine B (refresh the pane), not twice.
4. **The order is kept.** With machine B stopped again, create a new folder there, then copy a file from machine A into that new folder (two requests). - [ ] The second one reads "waiting for machine B (1 ahead)". Start machine B. - [ ] The folder is made first, then the copy lands in it.
5. **The files changed meanwhile.** With machine B stopped, rename another test file there. On machine B itself, while its agent is stopped, edit and save that file (or replace it). Start machine B's agent. - [ ] Before sending, rCommander asks: "Since you asked, on machine B: ... changed (...). Send it anyway?". Answer **No**. - [ ] The job ends Cancelled with "Not sent: the files on machine B changed." - [ ] The file on machine B is not renamed. Repeat and answer **Yes**: - [ ] the rename runs once.
6. **Cancel and restart.** Hold one more request for stopped machine B, then cancel it from the toast or the task panel. - [ ] It ends Cancelled and nothing happens on machine B when it comes back. Hold another one, restart the agent on machine A (tray ▸ Restart agent), then start machine B. - [ ] The held request is still in the task panel after the restart and is sent once when machine B is back. - [ ] **Settings ▸ Storage** lists "Held requests for machines that are off" with no Clean button.
7. **Updates with the app window open.** Repeat Part 4 with the app window from step 1 open. - [ ] After the update the app window shows the new version (Help ▸ About) without reinstalling the app.
8. **Favourites: the star.** Open a folder, for example `D:\Photos`. - [ ] The pane header shows an empty star after the drive button. Right-click the star and choose **Add this folder**. - [ ] The star fills, and it stays filled in every pane that shows this folder. If you used bookmarks in 0.1.6: - [ ] they are all there as favourites, and m or ' with a letter still jumps to them. Right-click the star again and choose **Remove this folder**. - [ ] The star is empty again.
9. **Favourites: menu, groups and keys.** Add three or four folders as favourites. Click the star (or press **Ctrl+D** with the Total Commander keys). - [ ] The favourites menu lists them, each with a key (1-9, then a-z); pressing that key opens the folder. Open **Configure...** (in the menu, or **Go ▸ Favourites**). Add a group, move two favourites into it (drag, or **Move to**), add a separator, rename one to `&Holiday`, and use **Alt+↑/↓** to reorder. - [ ] The menu shows the group as a submenu, a line where the separator is, and H as the key of Holiday. - [ ] A group inside a group inside a group works; a fourth level is not offered. Give one favourite a second folder (and machine) for the other pane, then choose it from the menu. - [ ] Both panes go to their folders, and the entry shows ⇄. - [ ] The favourites panel (**View ▸ Panels ▸ Favourites**) shows the same tree.
10. **A favourite on a machine that is switched off (two machines).** Add a folder on machine B as a favourite, then stop the tray agent on machine B. Open the favourites menu. - [ ] That favourite is dimmed and its tooltip says why. - [ ] Choosing it shows a message at once instead of waiting. Start machine B again. - [ ] The favourite works again.
11. **Recent folders.** Visit a few folders, then open the favourites menu ▸ **Recent folders**, and **Go ▸ Recent folders**. - [ ] The folder the pane is in now is not listed in either. - [ ] **History** in the favourites menu lists this pane's back list, newest first, with the current folder marked.
12. **Settings, one section at a time.** Open Settings and click a section on the left (for example Files and lists). - [ ] Only that section is shown. Click **All** at the top. - [ ] Every section is shown, and the left side follows as you scroll. Pick a section, close Settings and open it again. - [ ] It opens on that section. Type a word in the search box. - [ ] Matches from every section show, grouped by section; clearing the search goes back to the section you picked.
13. **Simple and Advanced settings.** In **Settings ▸ Machine**, look at the list with **Show advanced settings** off. - [ ] Everyday options only: on/off switches, drives, LAN mode, passwords and the like. Turn **Show advanced settings** on. - [ ] Limits, intervals, caches and tool overrides appear, each with an "Advanced" tag, a faint tint behind the row and the same colour on the switch, readable in a light and a dark theme. Change one advanced value and turn the switch off. - [ ] That row stays in sight, tagged "Advanced · changed". - [ ] A search for an advanced setting finds it with the switch off.
14. **Storage words.** Open **Settings ▸ Storage**. - [ ] The rows read in plain words, such as "Search index", "Files unpacked from archives", "Copies between machines", "Task output", "Tray agent log" and "Sessions and signed-in browsers". - [ ] Your own data names favourites and folder looks.
15. **Search every machine (two machines).** Click **Search** in the toolbar (or press **Ctrl+Alt+F**; **Alt+F7** in the Total Commander keys). Type part of a file name that exists on both machines. - [ ] Results appear while you type, newest first, each with its machine's colour mark. - [ ] The chips (Photos, Videos, Music, Documents, Archives, This week, This year, Over 100 MB, Over 1 GB, Files only) narrow the list and change the text in the box to match; clicking a machine chip leaves that machine out. Open **Syntax** and click a few examples. - [ ] They are put into the box: try `"a phrase"`, `holiday or summer`, `-draft`, `/^IMG_\d+/`, `size:>10mb`, `modified:2024`, `ext:jpg,heic`, `path:photos`. - [ ] An unknown word such as `colour:red` shows an error and searches nothing. This has not been tried on real machines before: be exact about what you see.
16. **Search results as a file list (two machines).** Press **Enter** (or **Open in pane**). - [ ] The pane shows the results with a Machine column after Folder, and the header says "Fleet search: ..." with the count. - [ ] Sort, mark, rename and trash work as in any folder. Press **Enter** on a photo. - [ ] It opens in the viewer, and the arrow keys step through the other results, also those on the other machine. Press **Enter** on a folder hit. - [ ] That folder opens on its machine. Right-click a file hit and choose **Show in its folder** (also **Go ▸ Show in its folder**). - [ ] The pane goes to the folder that holds it. - [ ] **Edit search** brings the box back with your text. Leave the results. - [ ] The pane has its own sort back.
17. **Machines that were not searched (two machines).** Stop the tray agent on machine B and search again. - [ ] The top of the box and the pane header name machine B and say it is offline (with since when), never just showing fewer results. With machine B running 0.1.6, if you still have it: - [ ] it says machine B "needs an update to search". With the index switched off on machine B: - [ ] it says so.
18. **Copy results from two machines into one folder (two machines).** Make two files with the same name, one on each machine (for example `notes.txt`), and one more file that is only on machine B. Search for them, mark the results from both machines, open an empty folder on machine A in the other pane and press **F5** (Copy). - [ ] A dialog lists each clashing name with both sides (machine, size, date) and says nothing is asked later. - [ ] **The same for all** sets every row; each row can also be set on its own. - [ ] With two files of the same size and time, "Skip identical ones" sends one of them only. Start it. - [ ] One job in the task panel copies from both machines, and every file lands directly in the folder, by the choices you made. - [ ] Undo removes them again.
19. **The Sort button.** Switch a pane to the thumbnail grid, then to Miller columns. - [ ] The status bar shows how the list is sorted, for example "Sort: Modified ↓". Click it. - [ ] It offers the same choices as the column headers in Details, including a secondary sort, and the list follows.
20. **Thumbnail zoom.** In the thumbnail grid drag the slider in the status bar. - [ ] The thumbnails grow and shrink from 64 to 512 px; S, M, L and XL are marks on the slider. Hold **Ctrl** and turn the mouse wheel over the grid. - [ ] It zooms too, and the page itself does not zoom.
21. **Folder looks: save one.** Open a folder of photos, for example `D:\Photos`, and set it up: thumbnail grid, a large zoom, sorted by Modified newest first. Choose **View ▸ Folder look ▸ Save this folder's look...**. Name it "Photos", choose this folder with its subfolders, mark the list mode Locked and the sort Initial, and save. - [ ] A chip in the pane header says "Photos". Go to a folder outside `D:\Photos`. - [ ] The pane is back to how it was before, with its own list mode and sort. Go back into `D:\Photos` and into one of its subfolders. - [ ] The look is applied in both.
22. **Folder looks: Initial and Locked.** In `D:\Photos` change the sort. - [ ] It changes at once (Initial) and lasts until you leave the folder. Switch to the Details view. - [ ] Because the list mode is Locked, a question appears at the chip: **Change for this folder**, **Just for now**, **Cancel**. **Cancel** keeps the grid; **Just for now** switches until you leave; **Change for this folder** switches and keeps it for the folder from now on. - [ ] A locked sort shows a lock beside the sort arrow in the column header.
23. **Folder looks: the chip, the icon and editing.** Go to a folder without a look. - [ ] A faint palette icon sits in the pane header. Click it. - [ ] It offers your saved looks (pick "Photos" to give it to this folder) and **Save this folder's look...**. Back in `D:\Photos`, change the zoom, then click the chip ▸ **Edit...**. - [ ] The dialog starts from what the pane shows now, with "saved: ..." beside each value that differs (click it to keep the saved one). - [ ] The button says **Update**, and **Save as new** keeps "Photos" and makes a new look. Click the chip ▸ **Back to the pane's own settings for now**. - [ ] The pane shows its own settings, and the chip offers **Apply the look again**. The chip ▸ **Use another look** switches to another saved look. The chip ▸ **Remove from this folder**. - [ ] The chip is gone and the pane keeps its own settings. **Settings ▸ Files and lists ▸ Folder looks** lists the looks with the folders that use them, and deletes a look after a second click.
24. **The index badge.** Look at a pane's header while the index is healthy. - [ ] Next to the machine button there is no badge, and the free space in the status bar never moves. Turn a drive's index off in the index popover, or pause the index (**View ▸ Indexing**). - [ ] A small badge appears next to the machine button; its tooltip says what is wrong, and a click opens the per-drive popover. Turn it on again. - [ ] The badge goes away once the index is ready. On Windows, with an elevated install, create and remove a temporary folder from PowerShell (`mkdir C:\rc-temp-test; rmdir C:\rc-temp-test`). - [ ] The index does not start re-reading the whole drive (no checking badge for minutes).
25. **Folders the index cannot read (Windows).** Make a test folder, for example `D:\rc-locked`, and in its Properties ▸ Security deny your own account "List folder contents". Restart the tray agent (tray ▸ Restart agent) and wait for the index check to finish. - [ ] The index popover names `D:\rc-locked` and says access is denied. - [ ] **Skip this folder** asks first, then leaves it out of the index and search, and the warning goes away. Before you skip it, turn the drive off and on in the popover: - [ ] the warning stays until the folder can be read or is skipped. If a drive has a damaged folder: - [ ] the popover says it is damaged and shows `chkdsk X: /f` (with that drive's letter) and a **Copy** button that copies the command. Remove the deny rule and the test folder afterwards, and take its entry out of the index excludes in **Settings ▸ Machine** (search for "exclude").
26. **Update checks shared between machines (two machines).** Open rCommander on machine A, or open the tray menu there. Then open **Help ▸ Check for updates** and **Help ▸ About ▸ Machines** on machine A and on machine B. - [ ] Both say "latest x.y.z (checked by <machine> N min ago)", naming the machine that checked, and the tray's Updates submenu says the same. - [ ] Opening the tray menu again within 15 minutes does not check again (the time stays). - [ ] When a machine's own check shows something else than another machine reported, it shows its own result plus "<machine> reported x.y.z, not confirmed here". - [ ] A machine still installs only a release it checked itself. Only tested with two computers so far.
27. **What's new.** Choose **Help ▸ What's new**. - [ ] Every version is listed, newest first, all the way back to 0.1.0, not only the version you run.
28. **Help ▸ About.** Open **Help ▸ About**. - [ ] It is taller than in 0.1.6 and never larger than the window. - [ ] Its first page links to the releases, the changelog, the wiki (quick tour, script cookbook), this install and test guide, bug reports, known issues and Discussions; each link opens the right page. - [ ] The buttons **What's new**, **Keyboard shortcuts** and **Report a problem** open those.
29. **The top bar and toolbars stay one line.** Make the browser window narrower step by step. - [ ] The top bar and every toolbar stay on one line: labels turn into icons first, then parts move into a **»** button at the end of the bar. - [ ] The **»** menu lists them, works with ↑ ↓ and Enter, and Esc closes it. Widen the window again. - [ ] The parts and their labels come back. Right-click a part and choose **Always show**. - [ ] It stays on the bar when narrowing (until even the pinned parts do not fit). Right-click another and choose to keep it always in the » menu. - [ ] It is only in the menu. **View ▸ Toolbars ▸ Show all items by room again** undoes both.
30. **Default app in front, and a type with no app.** Repeat Part 9 step 2. - [ ] Each app comes to the front of the browser. - [ ] A file type with no app says "No app is registered for ...", with no Windows error or dialog. - [ ] No "Open with..." is offered.
31. **Another machine's file through its shares (two machines).** Repeat Part 9 steps 6 and 7. - [ ] A file in a folder machine B's file server shares (also a share its rCommander does not list, such as Samba in a container, or a drive you mapped to it) opens in place, and the toast says which way it went. - [ ] **Copy full path** gives the same `\\` path. - [ ] A copy is made only when no share reaches the file or the file on the share differs, and the message says why.
32. **Now playing on a Music Assistant speaker.** Play a folder of music on a Music Assistant speaker from rCommander. - [ ] The now-playing bar and **Playback** panel show the song that plays. In Music Assistant itself, add another song to that speaker's queue and play it (or start a radio there). - [ ] Within a few seconds rCommander shows that song, marked "added in Music Assistant", and no song in rCommander's own queue is shown as current. - [ ] The title never stays on an old song while the progress bar keeps moving. Skip back to one of rCommander's songs in Music Assistant. - [ ] rCommander marks that song as current again.
33. **Free space per drive.** Click a pane's drive button (or press Alt+F1). - [ ] Every drive shows a bar and "N free of M" under its name, and the same numbers as the status bar for the drive you are on. - [ ] A drive with less than a tenth free has a red bar. - [ ] Hovering a drive shows how much of it is used.
34. **Drives and machines apart.** - [ ] The drive button lists only drives, never machines. Click the machine button (in a narrow pane, or when the machines do not fit). - [ ] It lists only machines. With more than nine machines (only if you have them) the list starts short (this machine, the one shown, the ones online) with **Show all N machines** below it, and typing part of any name finds that machine.
35. **A pane header with many machines.** Make a pane narrow, or split until panes are small. - [ ] The row of machines folds into one machine button before it pushes anything away: the drive button, the star, the path and the filter stay in view. Make the pane wide again. - [ ] The row comes back.
36. **Settings ▸ Connections and Storage.** Open each with this machine chosen. - [ ] The machine list names this machine; it is never an empty box.

&nbsp;

---
&nbsp;

---

## Part 14 — Wallpapers

Needs a build with wallpapers, signed in as the owner. Step 5 needs a laptop on battery; step 6 needs a second browser signed in as a guest. This part has never been run in a real browser, so look closely at steps 2 and 3. Report problems as described under Reporting.

1. **Pick one.** Open **Help ▸ About** and click **Choose a wallpaper...** (or **View ▸ Wallpaper ▸ Wallpaper settings...**). - [ ] The list starts with None and **Built-in**: The Long Walk, Slow Drift, Fireflies, Aurora and the rest, each with a preview. - [ ] Clicking one turns the wallpaper on behind the window and the panes turn see-through. - [ ] Press **Ctrl+Alt+B**: everything is solid again and nothing animates. Press it again: it comes back.
2. **Live scenes.** Pick The Long Walk. - [ ] The sky matches your local time of day and the clouds drift very slowly. Pick Fireflies and Slow Drift. - [ ] They move gently and take their colours from your theme. In the browser's developer tools, Performance tab, the page is idle between frames.
3. **Your own picture and video.** Click **Upload picture or video...** (or drop a file on the list) with a photo. - [ ] A wallpaper with its name appears and is selected. - [ ] A text file or SVG is refused with a message naming the allowed types. Upload a short MP4. - [ ] It plays muted and loops; with the tab in the background it pauses.
4. **Depth and readability.** Press **Ctrl+Alt+Shift+B** repeatedly. - [ ] A toast names Flat, Glass, Focus in turn. - [ ] In Focus the pane you click stays clearer than the others. Pick a very bright photo with a light-on-dark theme. - [ ] Text stays easy to read; a surface that had to be made more solid says "Raised to ... % so text stays readable" in the dialog.
5. **Battery and reduced motion (laptop).** Unplug the laptop with a live wallpaper on. - [ ] It stops moving (one frame) and the blur turns off. Turn on "reduce motion" in the operating system. - [ ] A live wallpaper shows one still frame.
6. **A guest.** Sign in as a guest in another browser. - [ ] The wallpaper dialog lists None and the built-ins only: no upload, no scripts, no import. - [ ] Ctrl+Alt+B works there too.
7. **Share one.** In the dialog click **Export to a file...** and import the file again. - [ ] A `.rcwall.json` is saved, and importing it adds the wallpaper with its picture.

&nbsp;

---

## Reporting

For every ❌, write down:

- the step number,
- what you did,
- what you expected,
- what happened (a screenshot helps).

Use **Help ▸ Report a problem...** to build a diagnostics bundle: read every file in it first, save the zip, and drag it into the GitHub issue yourself. It masks paths, names and addresses, but check the files anyway.

Still never send the file `settings.json`: it contains passwords and keys.

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
