# What's new in rCommander

Newest first. Each release on the [Releases page](https://github.com/rsunde/rCommander/releases) shows its own part.

<!-- For maintainers: add a line under "Unreleased" with every user-visible fix or feature, in plain words, written
     for someone who uses rCommander, not for a developer. At release time rename "Unreleased" to the version.
     The release workflow publishes the "## <version>" section as the release notes; a release without one fails. -->

## Unreleased

## 0.1.5

*The story of 0.1.5, or how a short wish list became the biggest release yet.* The list really was short: open a file in its own app, stop calling a machine "online" when it is not answering, keep a log. Then the file manager did what file managers do and started organising. Opening a file meant knowing which machine you sit at. Telling the truth meant every chip, banner and tray icon had to stop saying "online" out of politeness. A log needs somewhere to live, which means knowing how much room everything else takes, which means a Storage page, which means a budget, which means... you can see where this went. Each idea was small. Together they were not.

*Why so many fixes?* Every piece was checked by a reviewer whose only job was to be unimpressed, and it earned its keep. Before any of this reached you it caught a report that could have kept a machine name it was meant to mask (an apostrophe was enough to hide it from the masker), a storage clean-up that could have made running copies trip over a locked database, and move-your-data-folder commands that were ready to start copying before the agent had finished putting its pen down. All fixed, each with a test that fails if it comes back. The list below is long because it is honest, which is rather the theme of this release. 0.1.6 promises to be smaller. It said that last time too.

- A task's console and failure details now survive an agent restart. A failed task keeps them for 90 days (finished ones for 30), shows the error that stopped it, and its log export includes the console, the error and a timeline.
- rCommander keeps a log of what it does, in the data folder, with old files removed automatically (Settings > Machine > Logs for the size and age limits). The tray menu and Help have Open logs folder.
- Help > Report a problem... (and Report this... on a failed task) builds a diagnostics zip you read in full first, with paths, machine names and addresses masked and passwords and keys always removed. Nothing is sent: you save the zip and post it yourself in a prefilled GitHub issue.
- If rCommander stopped unexpectedly last time, it now says so and offers to report it.
- Settings > Storage (also Tools > Storage...) shows every byte rCommander uses, what each part is for, and what clearing it does before you click. Caches can be cleared safely, history can be trimmed by age, your own data is never touched. An optional size budget clears the least useful parts by itself and lists what it did. A guided Move... shows the commands for putting the data on another disk.
- A machine that only shows up on the network but does not answer now says "unreachable" with the reason (refuses connections, does not answer, rejects this machine's key) instead of "online", and offline machines say when they were last seen.
- A banner at the top says when the rCommander agent on this computer stops answering, since when, and every other machine shows as "unknown" (amber, its mark dimmed) until it answers again.
- A folder says "live" only while changes really show up; otherwise it says when it was read and why it is not watched. Drives without live updates are no longer green and say when they were last re-checked.
- Searching a drive without live updates says the answer comes from the index and when it was last re-checked, and offers to search the disk instead.
- A job whose machine stops answering says "no contact with the machine since ..." and leaves the combined speed and time left, instead of looking stuck at its last numbers. The tray menu opens a job in the web page.
- Settings > Connections shows when the reach check ran and runs it again by itself after ten minutes.
- Music Assistant is noticed as gone within about 40 seconds when its server disappears, instead of staying "connected".
- The tray's Restart agent is now offered whenever the agent can restart itself, also when it was started by the setup scripts; it is greyed out with the reason otherwise.
- The tray icon, tooltip and menu show the real state: machines, jobs, drives without live updates and updates, each with its age, a red icon when the agent does not answer, amber for an unreachable machine or a drive without live updates, and "Status details unavailable" when an older agent cannot tell.
- Open any file in the app your computer uses for it: Shift+Enter, File ▸ Open with default app, or Open with… on Windows. Files from your other machines open as a copy you can copy back.
- Enter on a file the viewer cannot show now opens it in its app when you sit at that machine, instead of downloading it. On any other device, Enter, o and a double-click still download it; F3 and v still open the viewer.
- The index status popup is calmer: drives that lost live updates for the same reason share one short line with a "How to fix" button (the fix, a copyable command and the numbers appear only when you open it), and the popup scrolls instead of growing past the window. Container storage mounts on Linux are no longer listed as drives, and system mounts such as /boot/efi are no longer indexed by default (list them under Index:Volumes to keep them); a skipped drive shows under "Not connected" until you forget it.
- Every panel can now go anywhere: drag the inspector, tasks, undo history, script console, playback or any side view by its header or tab to the left, right, top or bottom, into another panel as a tab, out as a floating window, or into a pane as a tab. A highlight shows where it will land.
- Each side holds several panels as tabs or stacked one above the other, and every side, every split between panels and every floating window can be resized by dragging, with the arrow keys, or reset with a double-click.
- Panels and whole sides collapse to labelled strips, tall at the left and right, wide at the top and bottom; the task strip shows running jobs and their progress, and a click on a collapsed task strip opens it again.
- View ▸ Panels shows or hides each panel and moves the focused one; Move panel to… does it from the keyboard, and F6 steps through the open panels.
- Right-click a panel's tab (also when it sits as a pane tab) for its placement menu: move, float, collapse, hide.
- Personalities remember where the panels sit, so a saved personality brings its layout back (floating windows are not saved).
- Applying a personality replaces the whole panel layout: the built-in ones that do not place panels hide the side bar, the bottom panel and the task panel; View ▸ Panels brings any of them back.
- Your current side bar, bottom panel, inspector and task panel placements carry over on the first start.
- The inspector no longer shows a file's owner as an attribute; the owner has its own row.
- A setup update dry run now names the same old version folder that the real update removes.
- Column headers in the disk usage view, the duplicates list and the sync view look and work like the file list's: click anywhere on a header to sort, click again to reverse (the sync view's headers are for looks only, and the duplicates list's Machine column is not sortable).
- Settings: each section has its own icon and colour, bigger headings, and the list on the left follows as you scroll.
- The disk usage view and the folder tree now drag, drop, mark ranges and open files like the details list; Miller's side columns drag, take drops and open files too (their right-click menu acts on that row).
- Each pane group has buttons for the list modes (details, thumbnails, grid, Miller, tree, disk usage) next to the split buttons; in a narrow tab bar they fold into one button with a menu.
- Maximising a pane keeps the other panes as tall bars showing their machine, folder, free space, items, whether they are the copy target and any copy running into them; drop files on a bar, expand it to bring the layout back.
- In Miller columns the preview column is the inspector itself; text previews use all the height left, with the file's properties below. A Miller pane you are not working in shows the file's name, size and date.
- The inspector and the task panel share one header with the same buttons in the same order (folded into a Placement menu when narrow); the inspector can dock at the top too.
- Importing a VS Code theme now explains in plain words what it gave, and a Colours tab lets you pick any colour from the theme's palette or your own; your choices stay when the theme is updated from the gallery. Exporting a theme writes your choices into the file.
- Folders show their size from the index in the file list, when sorting by size, in the status line and in copy, move and delete confirmations (sizes are estimates, shown with a tilde; nothing is shown when the index is off or for network and archive folders).
- Every machine now has its own colour, and it is the same colour on every machine you use: a small mark beside the machine's name in pane headers, the machine picker, tabs, the folder tree, tasks and Help > About, plus a thin stripe along the top of each pane. Settings > Appearance (or View > Machine colours) chooses marks and stripe, marks only, or off. The name is always shown beside the mark.
- Change colours... (right-click a machine) lets you pick another colour for any machine; if another machine already has it you can swap the two.
- One machine can be the flagship (Help > About > Machines, or Settings > Machine): the others follow its lead when they must agree, and carry on without it when it is offline. Hand the flag to another machine or clear it at any time. If two machines were apart and each got a flag, the newer choice keeps it and the other one is told once.
- Forget machine (Help > About > Machines) removes a machine that is offline and no longer wanted; if it is still running it simply takes a colour again.
- Machines still on 0.1.4 or older keep working and are given a colour by the fleet; they show it themselves once updated.
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