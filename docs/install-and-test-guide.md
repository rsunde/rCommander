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

Needs rCommander 0.1.5 signed in as the owner in a browser on the same computer as the agent. Steps 1-4 use a Windows computer with an install made with the elevated option; steps 5-7 also need a second machine running rCommander (machine B) and a phone or another computer; steps 8-9 need a Linux computer. Report problems as described under Reporting.

1. Select a `.txt` file and press Shift+Enter, then do the same with a `.docx` file. - [ ] Each opens in the app Windows has registered for it, on your screen. - [ ] In Task Manager > Details, add the "Elevated" column: the app shows **No**.
2. Select a file and choose File > Open with... - [ ] A chooser for the app appears (write down what Windows 11 shows). - [ ] Picking an app opens the file in it, and its Elevated column says **No**.
3. Select a `.ps1` file and press Shift+Enter. - [ ] A dialog says the file is a script and that opening it runs it. - [ ] Cancel opens nothing. - [ ] Run opens it.
4. Select an image and press Enter. - [ ] It opens in the built-in viewer. Select a file the viewer cannot show (for example a `.docx`) and press Enter. - [ ] It opens in its app, not as a download. Set Settings > Files and lists > Enter on a file to "Always the system app" and press Enter on the image. - [ ] It opens in its app. Set the choice back.
5. On a phone or another computer, open rCommander from this machine's address and sign in as the owner; select a file and choose Open with default app from the context menu. - [ ] The message says the app would open on the machine's screen, not on this device, and offers Download. - [ ] Download saves the file. - [ ] Nothing opens on the machine's own screen. Press Enter on a file the viewer cannot show. - [ ] It downloads.
6. On the machine from step 1, browse to a file on machine B and open it with Shift+Enter. - [ ] It opens in the app, and a toast says it opened a copy and that changes stay in the copy. Edit the file in the app and save. - [ ] The toast's Copy back starts a copy to machine B, and the normal overwrite question appears.
7. Open Tools > Opened copies... - [ ] The copy is listed with its source machine, when it was opened and "changed". - [ ] Open again, Show folder and Copy back work. - [ ] Remove fails with a message while the app still has the file open, and works after you close it.
8. On a Linux desktop with the user-service install, open a `.txt` file with Shift+Enter. - [ ] It opens in the registered app. - [ ] Open with... is not offered. - [ ] A file with the executable bit asks first, like step 3.
9. On a Linux machine without a desktop (a server, or a system-wide install), press Shift+Enter on a file. - [ ] The toast says "No desktop on this machine". Now reach that machine's rCommander through an SSH tunnel to its loopback port and press Shift+Enter again. - [ ] The browser counts as local (the tunnel arrives on loopback), so it gets the same "No desktop" answer; on a machine with a desktop the app would start on that machine's own screen, not on yours.
10. Open the agent's log after the steps above. - [ ] There is one `Open` line for every attempt, refused ones included, naming the result, the path and where the request came from.

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
