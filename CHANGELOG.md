# What's new in rCommander

Newest first. Each release on the [Releases page](https://github.com/rsunde/rCommander/releases) shows its own part.

<!-- For maintainers: add a line under "Unreleased" with every user-visible fix or feature, in plain words, written
     for someone who uses rCommander, not for a developer. At release time rename "Unreleased" to the version.
     The release workflow publishes the "## <version>" section as the release notes; a release without one fails. -->

## Unreleased

## 0.1.7

*Sjutton också!* This one was going to be small. So was the one before it, and the one before that, and by now "this release will be small" is less a plan than a family tradition. When a Swede fails, they say *sjutton också!*, roughly "seventeen as well!", a curse so mild it is printed on children's books. It is also, by pure coincidence and no planning whatsoever, this version's name: 0.1.7, seventeen. So when this list grows longer than promised (it will, it already has), you know what to say. We said it first.

*Zoom out.* See? It grew. For seven releases we stared so hard at files that we forgot to look up. Files live on drives, drives live in machines, and machines, it turns out, come in fleets. rCommander could tell you a file's size to the byte, but not whether the universe around it had room for one more. Now it can. We also pretended you own forty machines, just to see what would break. Quite a lot did. You probably don't own forty, but if you ever do, the header is ready.

- Favourites, like Total Commander's directory hotlist: every pane has a star after its drive button, filled when the folder is a favourite. Click it (or press Ctrl+D in the Total Commander keys) for the favourites menu; right-click it to add or remove this folder. Bookmarks are now called favourites and nothing is lost: your letters (m and ' with a letter) still work.
- Recent folders (in the favourites menu and Go ▸ Recent folders) no longer lists the folder you are in.
- Favourites can sit in groups (shown as submenus, up to three levels deep) with separator lines between them. Every entry has a key to press: put & before a letter in its name to choose it, otherwise the menu numbers them 1-9, then a-z. The menu also has Recent folders and History (this pane's back list).
- Favourites > Configure... arranges them: rename, give or take a letter, drag or Alt+Up/Down to reorder, move into a group, add groups and separators, change the folder or machine. A favourite can also open a second folder in the other pane at the same time.
- A favourite on a machine that is switched off shows dimmed with the reason, and choosing it says why instead of waiting.
- If you roll back to 0.1.6, its next save of your favourites drops groups, separators and second folders, but keeps every favourite, in order.
- Settings: each section now shows on its own. Pick one on the left and only that section is shown; All at the top shows them all as before. Settings opens on the section you chose last, and a search still looks through every section.
- Search every machine at once: the toolbar's Search button (or Ctrl+Alt+F; Alt+F7 in the Total Commander keys) opens one box over the index of every machine, with results while you type, newest first, each with its machine's colour. Plain words find names; chips add Photos, Videos, Music, Documents, Archives, This week, This year, Over 100 MB, Over 1 GB, Files only, and turn machines on or off. For more: "a phrase", `a or b` (or `a | b`), `-word`, `/regular expressions/`, `size:>10mb`, `modified:2024`, `ext:jpg,heic`, `path:photos`, `machine:name`. A machine that is off, unreachable, without an index or too old to search is named at the top with why, never silently left out. Enter opens the results in a pane, where you sort, mark, view (stepping across machines), open, rename, trash or copy them like any folder. Only file names and details are searched, not what is inside files. Not yet tried on real machines; the fleet as a whole has only ever been tested on two.
- Copy or move search results from several machines into one folder in one go: one job pulls from every machine, every file lands directly in the folder, and name clashes are asked once before anything moves, showing both sides, with "the same for all" and "skip identical ones". Not yet tried on real machines.
- Search results now work like any file list: Enter on a file opens it where it is (the viewer steps through the results, so you can look at the photos one after another), and Enter on a folder opens that folder. To go to the folder a result is in, right-click it and choose Show in its folder (also in the Go menu). This applies to every search, not only searches across machines.
- Views without column headers (the thumbnail grid and Miller columns) show how the list is sorted in the status bar, for example "Sort: Modified ↓". Click it to choose another order or a secondary sort: the same choices as the column headers in the Details view.
- On Windows, the index no longer re-reads a whole drive after a program creates and removes a temporary folder.
- When the index cannot read a folder, the status popover now names it and says why (damaged on disk, or access denied). For a damaged folder it shows the full Windows disk check that repairs it (`chkdsk X: /f`) with a Copy button, and every such folder has a Skip this folder button that leaves it out of the index and search. Turning the index or the drive off and on no longer hides the problem: it stays shown until the folder can be read or is skipped. A drive marked this way by an earlier version is re-checked once to name its folders, and stays marked meanwhile.
- Settings has a Simple / Advanced switch: everyday options show by default, and limits, intervals, caches and tool overrides appear with "Show advanced settings" (a search still finds them, and one you changed always stays in sight).
- Advanced settings stand out: a colour of their own (taken from your theme), a faint tint behind each one, and the same colour on the Show advanced settings switch.
- Settings > Storage speaks plainer: "Search index", "Files unpacked from archives", "Copies between machines", "Task output", "Tray agent log", "Sessions and signed-in browsers", and your own data now names favourites and folder looks.
- Your machines now share what they learn about new releases: opening rCommander or the tray menu makes that machine look for an update (at most every 15 minutes), the others hear about it, and the Updates window, Help > About > Machines and the tray say "latest x.y.z (checked by <machine> N min ago)", or that no machine has checked for two days. Each machine still checks and verifies a release itself before it installs it. Only tested with two computers so far.
- Help > What's new now shows every version's changes, newest first, all the way back to the first release, not only the version you run.
- Playing on a Music Assistant speaker: the now-playing bar and the Playback panel show the song Music Assistant really plays, also when it was added in Music Assistant itself or by its radio (then marked "added in Music Assistant"), instead of an old title while the progress bar kept moving. Not yet checked with a real Music Assistant speaker.
- Help > About is half as tall again, and its first page now links to the releases, the changelog, the wiki (with the quick tour and the script cookbook), the install and test guide, bug reports, known issues and Discussions, plus buttons for What's new, Keyboard shortcuts and Report a problem.
- Wallpapers: put a picture, a video or a live scene behind the whole window (View > Wallpaper). Panes and bars turn to glass, and a readability guard keeps the text easy to read. Ctrl+Alt+B shows or hides it, Ctrl+Alt+Shift+B steps through Flat, Glass and Focus.
- A pack of 12 built-in wallpapers, all drawn in code, including The Long Walk, which follows your local time of day, and two quiet live scenes that take your theme's colours (and hold still when your system asks for less motion). Help > About shows them off, with a button to choose one, and links the free 4K wallpaper pack The Long Walk (24 pictures) on GitHub.
- You can install rCommander as an app in Chrome or Edge (Help > Install rCommander as an app...): it gets its own window and a Start menu or launcher icon. Browsers allow this only on http://localhost, so install it on each computer from that computer. Whether Chrome and Edge offer it is still to be confirmed.
- When a machine is switched off, renaming, deleting or copying to it no longer just fails: rCommander holds the request, shows it in the task panel as waiting, checks the files when the machine is back and then does it, in the order you asked. You can cancel it while it waits. Not yet tried with two real machines.
- Opening a file in its default app now brings the app to the front; Open with... is removed for now (Windows does not show its app chooser for rCommander's background agent). A file type with no app now says so instead of showing a Windows error.
- The top bar and the toolbars no longer wrap onto extra lines when the window gets narrow. They stay one line: labels turn into icons first, then the least important parts move into a » button at the end of the bar, whose menu lists them. Right-click any part to keep it always visible or always in the » menu (View > Toolbars > Show all items by room again undoes that).
- The index status no longer pushes the free-space text around: it now shows as a small badge next to the pane's machine button (nothing when all is well), with the details in its tooltip and the per-drive popover one click away.
- Opening a file of another machine in its app, or copying its path, now uses that machine's network shares first, also ones its rCommander does not list (such as Samba in a container) and drives you mapped to them, but only when the file there is the same; a copy is made only when no share reaches the file, and the message says which way it went and why.
- Folder looks: a folder can keep its own way of being shown (list mode, thumbnail size, sort, filter and column set). Open the folder, set it up the way you like, then View > Folder look > Save this folder's look... Name the look ("Photos") to give it to other folders too, choose this folder, its subfolders or a pattern such as `**/DCIM/**`, and mark each setting Initial (set when you arrive, your changes last until you leave) or Locked (always shown; changing it asks whether to change it for the folder or just for now). A chip in the pane header names the look; leaving the folder puts your own settings back. Settings > Files and lists > Folder looks lists them all.
- A folder without a look of its own shows a faint palette icon in the pane header, where the look's name appears once it has one. Click it to pick one of your saved looks for this folder, or to save how the folder is shown now. The chip of a folder that has a look offers the other looks too (Use another look).
- Editing a folder's look now starts from what the pane shows, so changes you made there are what gets saved; a value that differs from the saved one shows "saved: …" beside it (click it to keep the saved one). The button says Update when you change a saved look, and Save as new keeps the saved look and makes a new one from what you see.
- Thumbnail zoom: in the thumbnail grid a slider in the status bar sets the size from 64 to 512 px, and Ctrl+mouse wheel over the grid zooms too. S, M, L and XL are marks on the slider.
- The drive picker shows how full each drive is: a bar and "120 GB free of 1 TB" under every drive, red when less than a tenth is free.
- The drive button lists only drives now, and the machine button only machines. A long list of machines no longer has to be scrolled past to reach the disks. Many machines also start as a short list (this machine, the one shown and the ones online) with "Show all" below; typing a name finds any of them.
- A pane header with more machines than fit folds them into the machine button, so the drive button, favourites star, path and filter stay in view. Only ever tried with made-up machines in the browser: the fleet has been tested on two real machines.
- Settings ▸ Connections and Settings ▸ Storage name this machine in their machine list again; it showed as a blank box.

- [x] mjölk
- [ ] pepparkakor (2 packs, the THIN ones)
- [ ] snow?? check forecast. a lot
- [x] glögg
- [ ] tree, small, lights in every colour. one light per room
- [ ] ribbon red + green + gold
- [ ] say god jul to the neighbour (say it twice if he doesnt hear)
- [ ] sjutton... something. forgot what
- [ ] batteries for the star
- [ ] tomte??

## 0.1.6

*The small one, as promised.* 0.1.5 swore the next release would be smaller, and for once it kept its word. Most of this is what you found while living with 0.1.5: an update button that trusted week-old news, a status dot that sulked about folders Windows locks for everyone, a Copy path that forgot other machines speak SMB. Each fix came with a test that fails if it comes back, and a night of chasing tests that only failed when the computer was busy turned up one real bug as a bonus (the Music Assistant one, last line).

### Machines and updates

- Update all in Help > About > Machines now asks every machine to check for a new release first, so a machine with an old cached check is no longer skipped. Each machine shows when it was last checked and has a "Check now" button, and a machine that was not checked or could not be reached is listed as unknown, never as up to date.
- Help > About > Machines now has a Roll back button on each machine that can return to its previous version (it asks first), and a machine that cannot be updated with one click shows why and the command to run by hand.
- Right-click a machine > Properties now opens Help > About > Machines on that machine's card (version, channel, update, colour, reachability and why it is not online), instead of a short pop-up note.
- The tray's Jobs menu now also lists the jobs running on your other machines, under each machine's name; one that needs an answer turns the tray icon to "needs you", and a machine whose jobs could not be read says so instead of showing nothing. Clicking a job opens it on that machine.

### Files, folders and opening

- Opening the same unchanged file from another machine (or from inside an archive) again now reuses the copy already on this computer instead of downloading it every time; a copy you edited is never reused or overwritten.
- Open with... now asks Windows Explorer for its own "Open with" chooser instead of the old rundll32 call, which showed nothing on Windows 11 build 26100; this is changed in code and still waits for a check on a real machine. The agent log now says "Requested" for it, not "Opened".
- Tools > Opened copies now shows how many copies there are and how much space they take, and has "Remove all unchanged" to clear every copy you have not edited (copies you edited, or that an app still has open, stay). "Remove all, losing changes" removes edited copies too, after one confirmation. Settings > Storage has an "Opened copies" row whose Clean does the same unchanged-only clear.
- Settings > Machine > Sharing now has "SMB shares of this machine": list the shares your file server really serves (name, the folder it serves, read-only) when rCommander cannot find them itself, for example Samba running in Docker. rCommander does not create the share; it must already exist in Samba. Other machines then open a file from here in place instead of copying the whole file first.
- Copy full path and Copy folder path on a file that lives on another machine now give its network (UNC) path, such as a path starting with two backslashes and the machine name, when that machine shares the folder over SMB and answers; otherwise you still get the machine's own path.
- Hover a folder's size in a file list (or its tile) and it now says where the number comes from and how old it is, for example "From the index, as of 14:03 (3 min ago)"; it says so plainly when the index is still building, and warns when the drive has no live updates and was last re-checked a while ago.
- The index status dot no longer stays blue because of folders Windows keeps closed to everyone (such as CSC or System Volume Information), and turning the index off and on no longer hides a real "partial" warning.

### Dialogs

- Dialogs (About and the other pop-up windows) are about 50 % bigger, never larger than the window, and you can resize them: drag the grip in the bottom-right corner or press Alt+arrow keys (Shift = bigger steps). The size is remembered per dialog. Windows that were already large (Settings, theme gallery, report) keep their size; narrow screens still use the full width.
- The copy and move dialog (and Add to transfer) show each machine's colour mark beside the source and the target, dimmed when that machine is not online.
- Multi-rename: the preview columns can be dragged wider or narrower (double-click fits), names stay on one line with the full text on hover, Old name shows the name only, there is a "changed only" filter, and the dialog is wider.

### Speakers

- When Music Assistant refuses the token (or needs a newer rCommander), the speaker picker and Settings now keep saying so, with the time it was first refused, while rCommander retries; before, the reason flipped to "not reachable" between retries.

## 0.1.5

*The story of 0.1.5, or how a short wish list became the biggest release yet.* The list really was short: open a file in its own app, stop calling a machine "online" when it is not answering, keep a log. Then the file manager did what file managers do and started organising. Opening a file meant knowing which machine you sit at. Telling the truth meant every chip, banner and tray icon had to stop saying "online" out of politeness. A log needs somewhere to live, which means knowing how much room everything else takes, which means a Storage page, which means a budget, which means... you can see where this went. Each idea was small. Together they were not.

*Why so many fixes?* Every piece was checked by a reviewer whose only job was to be unimpressed, and it earned its keep. Before any of this reached you it caught a report that could have kept a machine name it was meant to mask (an apostrophe was enough to hide it from the masker), a storage clean-up that could have made running copies trip over a locked database, and move-your-data-folder commands that were ready to start copying before the agent had finished putting its pen down. All fixed, each with a test that fails if it comes back. The list below is long because it is honest, which is rather the theme of this release. 0.1.6 promises to be smaller. It said that last time too.

### New

- A task's console and failure details now survive an agent restart. A failed task keeps them for 90 days (finished ones for 30), shows the error that stopped it, and its log export includes the console, the error and a timeline.
- rCommander keeps a log of what it does, in the data folder, with old files removed automatically (Settings > Machine > Logs for the size and age limits). The tray menu and Help have Open logs folder.
- Help > Report a problem... (and Report this... on a failed task) builds a diagnostics zip you read in full first, with paths, machine names and addresses masked as far as it can (masking is best effort, so check the preview) and passwords and keys always removed. Nothing is sent: you save the zip and post it yourself in a prefilled GitHub issue.
- If rCommander stopped unexpectedly last time, it now says so and offers to report it.
- Settings > Storage (also Tools > Storage...) shows every byte rCommander uses, what each part is for, and what clearing it does before you click. Caches can be cleared safely, history can be trimmed by age, your own data is never touched. An optional size budget clears the least useful parts by itself and lists what it did. A guided Move... shows the commands for putting the data on another disk.
- Open any file in the app your computer uses for it: Shift+Enter, File ▸ Open with default app, or Open with… on Windows (on Windows 11 build 26100 Open with… currently shows no chooser). Files from your other machines open as a copy you can copy back.
- Enter on a file the viewer cannot show now opens it in its app when you sit at that machine, instead of downloading it. On any other device, Enter, o and a double-click still download it; F3 and v still open the viewer.
- Every panel can now go anywhere: drag the inspector, tasks, undo history, script console, playback or any side view by its header or tab to the left, right, top or bottom, into another panel as a tab, out as a floating window, or into a pane as a tab. A highlight shows where it will land.
- Each side holds several panels as tabs or stacked one above the other, and every side, every split between panels and every floating window can be resized by dragging, with the arrow keys, or reset with a double-click.
- Panels and whole sides collapse to labelled strips, tall at the left and right, wide at the top and bottom; the task strip shows running jobs and their progress, and a click on a collapsed task strip opens it again.
- View ▸ Panels shows or hides each panel and moves the focused one; Move panel to… does it from the keyboard, and F6 steps through the open panels (not in the Total Commander, Far, Midnight Commander and Explorer key layouts, where F6 keeps its own job).
- Right-click a panel's tab (also when it sits as a pane tab) for its placement menu: move, float, collapse, hide.
- Personalities remember where the panels sit, so a saved personality brings its layout back (floating windows are not saved).
- Applying a personality replaces the whole panel layout: the built-in ones that do not place panels hide the side bar, the bottom panel and the task panel; View ▸ Panels brings any of them back.
- Your current side bar, bottom panel, inspector and task panel placements carry over on the first start.
- Each pane group has buttons for the list modes (details, thumbnails, grid, Miller, tree, disk usage) next to the split buttons; in a narrow tab bar they fold into one button with a menu.
- Maximising a pane keeps the other panes as tall bars showing their machine, folder, free space, items, whether they are the copy target and any copy running into them; drop files on a bar, expand it to bring the layout back.
- Folders show their size from the index in the file list, when sorting by size, in the status line and in copy, move and delete confirmations (sizes are estimates, shown with a tilde; nothing is shown when the index is off or for network and archive folders).
- Importing a VS Code theme now explains in plain words what it gave, and a Colours tab lets you pick any colour from the theme's palette or your own; your choices stay when the theme is updated from the gallery. Exporting a theme writes your choices into the file.
- Every machine now has its own colour, and it is the same colour on every machine you use: a small mark beside the machine's name in pane headers, the machine picker, tabs, the folder tree, tasks and Help > About, plus a thin stripe along the top of each pane. Settings > Appearance (or View > Machine colours) chooses marks and stripe, marks only, or off. The name is always shown beside the mark.
- Change colours... (right-click a machine) lets you pick another colour for any machine; if another machine already has it you can swap the two.
- One machine can be the flagship (Help > About > Machines, or Settings > Machine): the others follow its lead when they must agree, and carry on without it when it is offline. Hand the flag to another machine or clear it at any time. If two machines were apart and each got a flag, the newer choice keeps it and the other one is told once.
- Forget machine (Help > About > Machines) removes a machine that is offline and no longer wanted; if it is still running it simply takes a colour again.
- Machines still on 0.1.4 or older keep working and are given a colour by the fleet; they show it themselves once updated.

### Honest status fixes

- A machine that only shows up on the network but does not answer now says "unreachable" with the reason (refuses connections, does not answer, rejects this machine's key) instead of "online", and offline machines say when they were last seen.
- A banner at the top says when the rCommander agent on this computer stops answering, since when, and every other machine shows as "unknown" (amber, its mark dimmed) until it answers again.
- A folder says "live" only while changes really show up; otherwise it says when it was read and why it is not watched. Drives without live updates are no longer green and say when they were last re-checked.
- Searching a drive without live updates says the answer comes from the index and when it was last re-checked, and offers to search the disk instead.
- A job whose machine stops answering says "no contact with the machine since ..." and leaves the combined speed and time left, instead of looking stuck at its last numbers. The tray menu opens a job in the web page.
- Settings > Connections shows when the reach check ran and runs it again by itself after ten minutes.
- Music Assistant is noticed as gone within about 40 seconds when its server disappears, instead of staying "connected".
- The tray's Restart agent is now offered whenever the agent can restart itself, also when it was started by the setup scripts; it is greyed out with the reason otherwise.
- The tray icon, tooltip and menu show the real state: machines, jobs, drives without live updates and updates, each with its age, a red icon when the agent does not answer, amber for an unreachable machine or a drive without live updates, and "Status details unavailable" when an older agent cannot tell.

### UX fixes

- The inspector no longer shows a file's owner as an attribute; the owner has its own row.
- Column headers in the disk usage view, the duplicates list and the sync view look and work like the file list's: click anywhere on a header to sort, click again to reverse (the sync view's headers are for looks only, and the duplicates list's Machine column is not sortable).
- Settings: each section has its own icon and colour, bigger headings, and the list on the left follows as you scroll.
- The disk usage view and the folder tree now drag, drop, mark ranges and open files like the details list; Miller's side columns drag, take drops and open files too (their right-click menu acts on that row).
- In Miller columns the preview column is the inspector itself; text previews use all the height left, with the file's properties below. A Miller pane you are not working in shows the file's name, size and date.
- The inspector and the task panel share one header with the same buttons in the same order (folded into a Placement menu when narrow); the inspector can dock at the top too.

### Index and setup fixes

- The index status popup is calmer: drives that lost live updates for the same reason share one short line with a "How to fix" button (the fix, a copyable command and the numbers appear only when you open it), and the popup scrolls instead of growing past the window. Container storage mounts on Linux are no longer listed as drives, and system mounts such as /boot/efi are no longer indexed by default (list them under Index:Volumes to keep them); a skipped drive shows under "Not connected" until you forget it.
- A setup update dry run now names the same old version folder that the real update removes.

### Security

- The agents exchange the list of colours (and the flagship) with each other, using the shared key, on your home network only; nothing goes to the internet. The key is sent to every agent that announces itself on your home network, so keep LAN mode to networks you trust.

## 0.1.4

- The VS Code look's left side bar is wider by default and you can drag its right edge to resize it (arrow keys when the edge is focused, double-click to reset); the width is remembered.
- Built-in toolbar templates such as the Total Commander button bar now follow the look (personality) you switch to: they hide unless the look asks for them. Your own toolbars keep whatever state you gave them.
- The folder tree now shows a drive's free space (hover a drive) and keeps it current: read again after copy, move or delete, on Refresh, and with the 30-second drive check.
- A drive the index cannot follow live (on Linux usually because the inotify watch limit is too low for a big disk) now gets a clear notice in the index status popover and in Settings ▸ Connections: why, what it costs, and the exact command that fixes it, with a Copy button.
- Such a drive is no longer walked almost nonstop: the next re-check waits at least 15 minutes, or four times as long as the last walk took (at most once a day by default). Restarting rCommander no longer starts such a walk at once when the drive was walked recently.
- Free space on a drive now follows the disk: it is read again after every copy, move or delete, on Refresh, and every 30 seconds or so. Before, it stayed as it was when the page loaded.
- Updates: when a newer release is out, a chip in the top bar shows it; click it to read what is new and update with one click (Help > Check for updates...). Help > What's new shows the notes of the version you run, and after an update you see its notes once.
- Help > About > System lists every machine's version and channel, marks machines that run an older or newer version than this one, and offers Update all: the other machines one at a time, each until it is back on the new version, then this one. The task panel follows each update through its restart, and the page reloads itself once this machine runs the new version.
- Tray: shows "Update to x.y.z..." in its menu and pops up one notification per new release; a tray started by an update waits up to 5 seconds for the old one to exit instead of quitting.
- Linux setup: `setup.sh install` and `update` no longer end with an error after a successful start when LAN mode is off.

## 0.1.3

- Setup's `update`, `status` and `uninstall` now find your existing install and reuse its folder, data folder and port, so you no longer repeat `-InstallDir` or `-DataDir`; they first print where each value came from.

## 0.1.2

- An agent started from the tray now listens on the network in LAN mode; before, the tray pinned it to this machine, so copies from other machines could not connect. Settings ▸ Connections now says so when that happens.
- A narrow folder tree now keeps names readable and the expand arrows clickable: it hides folder sizes first, then tightens the indent of deep folders instead of pushing the names out.
- While the index reads a drive, the status shows how far it is and about how long is left.
- The machine and drive list in a narrow pane opens again; before, clicking its button seemed to do nothing.
- The pane header shows one drive button for the current drive instead of a row of drives that was cut off with many drives.
- The machine and drive list can be filtered by typing, groups drives by kind (fixed, removable, network, optical, shares) and marks the current one.
- On Linux, system mounts (bind mounts, /boot, container and desktop helper mounts) are folded behind "Show N system mounts"; View ▸ Show system mounts in drive lists shows them, also in the folder tree.
- Linux drives show their volume label, and every drive its file system (ntfs, ext4, btrfs …) in the drive list.

## 0.1.1

- MKV, AVI, WMV, FLV, MPG, M2TS and other video files open in the video player instead of as text.
- VS Code themes such as Tokyo Night and Nord install again from the theme gallery.

## 0.1.0

The first release. Everything in it:

**All your computers**
- One agent per computer (Windows and Linux); each one shows the others' drives in its panes.
- LAN mode with one shared key for all your computers; computers find each other on the home network.
- Direct copies between computers, verified, resumed after a network drop or a restart of either side.
- Network shares (`\\server\share`): served by the rCommander on that server when it runs one, else opened directly.
- Browser sign-in for you (owner) and guests; guests see only the folders you share, read-only.
- Devices list: see every signed-in browser and revoke one at once.
- Sessions: every browser tab shows the same panes; named sessions, view-only, take over, kick a client.
- Tray icon (Windows): open, restart, stop, sessions and job progress.

**Browsing**
- Panes you split and tab freely, splitter snapping, maximise, tab overflow, layout templates and workspaces.
- Views: details with designable columns and column sets, thumbnails, folder tree, Miller columns, disk usage.
- Sorting by any column with a second sort key; media columns (duration, artist, album, taken).
- Bookmarks, back/forward from memory, instant re-open of recent folders.
- Git status of repositories: branch, ahead/behind, changed files marked.
- Inspector panel: details, previews, photo, music, video and e-book information, folder sizes.
- Context menus, drag and drop, uploads from the desktop, mouse-only use of everything.

**Search and index**
- Instant search across every drive from an index that follows changes as they happen.
- Lists shown from the index at once, then checked against the disk.
- Indexing can be paused, limited per drive, kept low priority, paused on battery.

**Working with files**
- Copy, move, rename, delete to the recycle bin, new folder and file, multi-rename with tokens and presets.
- Undo and redo with history for nearly everything.
- Conflict questions (skip, overwrite, rename, newer), copy filters, retries for files in use, saved copy jobs.
- Task panel: per-disk queues, pause, resume, reorder, add files to a running copy, speed graph, log export.
- Synchronise two folders, also on two computers, with filters and undo.
- Checksum files: verify and create (MD5, SHA, CRC32, XXH128).
- Folder watches that run a script when files arrive.

**Archives**
- Zip, 7z, tar and rar open like folders; nested archives too.
- Copy, rename and delete inside zip, tar and 7z archives (rewritten safely, undoable).
- Compress and extract, with protection against harmful archives.

**Viewing**
- Viewer with Rendered, Text and Hex modes; code highlighted like on GitHub.
- Markdown and HTML rendered safely; images, PDF, audio.
- Video: formats browsers cannot play are converted on the fly, on the graphics card when possible.
- E-book reader (EPUB, MOBI, AZW3, FB2) that remembers your page.

**Disk usage**
- Size tree, treemap, sunburst, icicle, pie and bar charts; top files, file types, ages, empty folders.
- Exact scans, snapshots over time, comparisons, duplicate finder with safe clean-up.

**Media and tools**
- Play music to this computer's speakers or to Music Assistant speakers.
- Convert video, audio and images.
- Tools view: finds ffmpeg, 7-Zip, mpv and others; installs and updates them from GitHub, verified.

**Make it yours**
- 13 personalities: Total Commander, Midnight Commander, Far, yazi, ranger, nnn, lf, vifm, Explorer, Directory Opus, VS Code and more.
- Every key can be changed; F-key bar, command line, own toolbars and the Total Commander button bar.
- Themes, including VS Code themes from the Open VSX gallery; three densities.
- JavaScript scripts with a built-in library (dated backups, photos by date, flatten, dedupe and more).

**Setup**
- Settings view for you and per computer, and a Connections page that finds and fixes missing setup.
- Install, update, roll back and uninstall scripts for Windows and Linux.
