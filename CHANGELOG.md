# What's new in rCommander

Newest first. Each release on the [Releases page](https://github.com/rsunde/rCommander/releases) shows its own part.

<!-- For maintainers: add a line under "Unreleased" with every user-visible fix or feature, in plain words, written
     for someone who uses rCommander, not for a developer. At release time rename "Unreleased" to the version.
     The release workflow publishes the "## <version>" section as the release notes; a release without one fails. -->

## Unreleased

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