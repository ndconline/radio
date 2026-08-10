


<img width="3823" height="2016" alt="main" src="https://github.com/user-attachments/assets/f2306f36-45b9-4c52-aa5c-4a9831d34dfc" />
<img width="1059" height="1329" alt="settings" src="https://github.com/user-attachments/assets/259b27c4-6c94-4556-a050-516aa633156b" />
<img width="2341" height="1987" alt="show" src="https://github.com/user-attachments/assets/23f3a3dc-6397-4da9-b0ea-efe73a6a59f4" />


Airwave Console

Airwave Console is a self-contained browser application for local radio automation, presenter practice, and show-planning exercises. It provides a media library, live playback deck, running order, playlists, hot keys, scheduled events, show run sheets, audio device routing, played-item logs, and local backups in a single HTML file.

The application runs locally in the browser. It does not require a package manager, build step, account, database server, or media upload service.

Important: Test the application, browser, codecs, media folders, and audio hardware before using it in a live environment. Airwave Console does not claim regulatory compliance, uninterrupted playout, or certified broadcast logging.

Contents

•Features

•Requirements

•Quick start

•Publish with GitHub Pages

•Supported media

•Filename timing convention

•Interface guide

•Basic operating workflow

•Playlists

•Hot cart

•Show planning and run sheets

•Scheduled events

•Audio input and output

•Session logs

•Backup and restore

•Settings

•Keyboard shortcuts

•Storage and privacy

•Limitations

•Troubleshooting

•Repository structure

•Contributing

•License

Features

| Area | Capabilities |
| --- | --- |
| **Local media sources** | Add separately named folders for music, advertisements, video, shows, jingles, playlists, or other media. Refresh, reconnect, replace, or remove a folder reference without modifying files on disk. |
| **Searchable media library** | Search by title, filename, folder path, or artist. Filter by source, artist, audio, video, or disconnected files. Preview a connected item for 10 seconds. |
| **Live playback deck** | View the previous, current, and next items. See elapsed progress, remaining time, expected finish, filename duration, and intro or outro talkover cues. |
| **Running order** | Add media next or at the end, drag to reorder, play a waiting item immediately, remove items, clear the queue, or shuffle it. The console calculates known queue time and an estimated finish. |
| **Automation modes** | Use Normal, Manual, Repeat, or Random playback behavior. |
| **Presenter segments** | Add open or timed announcer breaks, timed pauses, stop points, hold-next markers, and a Break after current command. |
| **Silence protection** | A prominent warning appears whenever nothing is queued next, with a direct path to emergency search. |
| **Emergency controls** | Search every connected folder, play a result now, queue it next, add it to the end, or use the always-visible Fade stop control. |
| **Playlists** | Build named playlists from selected media or the complete library. Reorder tracks, edit saved lists, append them, or replace the running order. |
| **Nine-slot hot cart** | Assign media to slots 1 through 9. Click a pad or press the matching number key to queue the item next. |
| **Show Centre** | Plan dated programmes with announcers, training notes, media, advertisements, intros, outros, talk segments, breaks, pauses, and stop points. |
| **Planned and actual run sheets** | Calculate planned start times, record actual local times, identify unplanned items, and export planned or actual run sheets as PDF. |
| **Scheduling** | Schedule media, playlists, breaks, pauses, stop points, and enhanced shows. Choose one-time or daily events, soft or hard timing, lateness tolerance, and optional hold-next behavior. |
| **Audio routing** | Select a program output when supported, enable a microphone or mixer input, monitor input level, and optionally route input monitoring to the selected output. |
| **Logs and data tools** | Download the current session's played-media log as CSV. Export or import station setup as JSON. Reset browser data without touching source media. |
| **Responsive operation** | The interface adapts from wide desktop layouts to smaller screens, provides visible keyboard focus, and respects reduced-motion preferences. |


Requirements

Airwave Console is designed for a modern desktop browser. A current Chromium-based browser is recommended for the broadest folder and audio-device support.

| Requirement | Guidance |
| --- | --- |
| **Browser** | Use a current desktop browser. Chrome or Edge is recommended for remembered folder access and optional audio routing. |
| **Media location** | Media remains on the operator's computer or attached storage. The browser receives read-only access to folders selected by the user. |
| **Page state** | Keep the page open while playing media or waiting for scheduled events. |
| **Audio permissions** | Microphone or mixer input requires browser permission. Some browser features require localhost or HTTPS. |
| **Screen size** | A wide desktop display provides the best four-panel layout, although narrower layouts are supported. |

Quick start

Option 1: Open the file directly

1.Download airwave-console-training.html.

2.Open it in your browser.

3.Select Add folder.

4.Choose Compatible folder import if remembered folder access is unavailable.

5.Select a folder containing supported audio or video files.

6.Add an item to the running order with Next or End.

7.Select Play or Start next.

Direct file mode is the fastest way to test the console. Folder access may need to be repeated after the browser is restarted.

Option 2: Run from a local web server

Serving the file from localhost can improve access to browser features such as microphone input.

Bash
python3 -m http.server 8000

Open http://localhost:8000/airwave-console-training.html in the browser.

If you rename the file to index.html, open http://localhost:8000/ instead.

Publish with GitHub Pages

Airwave Console can be hosted as a static site because all application code is contained in the HTML file.

1.Rename airwave-console-training.html to index.html, or keep the original name and link to it directly.

2.Add README.md, the HTML file, and the optional docs/assets screenshot directory to the repository.

3.Push the files to GitHub.

4.Open the repository's Settings, then open Pages.

5.Choose deployment from a branch and select the repository's main branch and root directory.

6.Open the published Pages URL after deployment finishes.

Hosting the page does not upload a user's media library. Each operator still chooses local folders through the browser, and the media remains on that device.

Supported media

The application recognizes the following filename extensions.

| Type | Extensions |
| --- | --- |
| **Audio** | `.mp3`, `.wav`, `.ogg`, `.m4a`, `.aac`, `.flac`, `.opus`, `.webm` |
| **Video** | `.mp4`, `.webm`, `.mov`, `.m4v`, `.ogv`, `.avi` |

An extension being recognized does not guarantee that every browser can decode its codec. Test production media in the exact browser and operating system that will be used.

Filename timing convention

Airwave Console can read a planned duration, intro talkover, and outro talkover directly from a filename. The preferred pattern is:

Plain Text


Artist - Title DURATION - INTRO~OUTRO.ext



For example:

3 Days Grace - Just Like You 3m06s - 12sec~4.mp3

This filename produces the following metadata.

| Parsed value | Result |
| --- | --- |
| **Artist** | `3 Days Grace` |
| **Title** | `3 Days Grace - Just Like You` |
| **Planned duration** | 3 minutes 6 seconds |
| **Intro talkover** | 12 seconds |
| **Outro talkover** | 4 seconds |

Time values can use forms such as 3m06s, 03:06, 1h2m3s, 12sec, or a plain number of seconds.

The legacy tilde-separated pattern is also accepted:


Artist - Title~3m06s~12s~4s.mp3


If no artist can be read from an Artist - Title name, the application may use the parent folder name. Generic folder names such as Music, Audio, or Media are ignored for artist detection.

The browser-reported duration is stored after media metadata loads. This actual duration can replace or supplement filename timing in later queue calculations.

Interface guide

| Interface area | Purpose |
| --- | --- |
| **Top bar** | Shows the station name, console state, local clock, Shows, Session Log, Station Data, Settings, and End Session. |
| **Silence warning** | Appears when no next item is ready. **Find next item** focuses the emergency search field. |
| **Emergency add** | Searches all connected folders and provides Play now, Add next, and Add end actions. |
| **Artists** | Filters the media library by parsed artist. |
| **Media library** | Manages folder sources, searches and filters media, previews files, creates playlists, and assigns hot keys. |
| **Live deck** | Displays the current playback state, timing, talkover cues, transport controls, player mode, volume, and audio routing status. |
| **Running order** | Holds all waiting media and presenter segments. The first item is the next item to play. |
| **Scheduled events** | Displays upcoming one-time or daily events and scheduled shows. |
| **Hot cart** | Provides nine reusable next-item shortcuts. |

Basic operating workflow

1. Connect media folders

Select Add folder, enter a source name and category, then choose one of the two access methods.

| Method | Behavior |
| --- | --- |
| **Remembered folder** | Uses the browser's enhanced folder picker. The folder handle can be stored and permission can be requested again later. |
| **Compatible folder import** | Works when the HTML file is opened directly. The folder will usually need to be selected again after reopening the browser. |


You can create separate sources for music, ads, videos, shows, jingles, and other content. Select a source card to filter the library. Use Refresh or Reconnect when access is lost, Change to choose a different folder, and Remove to remove only the application reference.

2. Find and preview media

Use the artist panel, library search, source cards, and media-type filter to narrow the library. Search matches the title, original filename, folder path, and artist.

Select Preview 10s to audition a connected file. Select the same control again, press Escape, or wait for the preview timer to stop it.

3. Build the running order

Use Next to put a media item at position one or End to append it. You can also drag a media row into the queue.

Within the queue, drag items to reorder them or use the arrow controls. The play icon starts a waiting item immediately. The remove icon deletes only that queue entry.

The queue summary shows the number of items, total known time, and estimated finish. A plus sign after the known time indicates that at least one duration is unknown.

4. Start and control playback

The main transport controls behave as follows.

| Control | Behavior |
| --- | --- |
| **Play** | Starts the first queued item. While media is active, it becomes Pause or Resume. During a presenter segment, it starts the next item. |
| **Previous** | Replays the most recent connected media item from browser history. |
| **Fade stop** | Reduces the current player's volume over the configured fade duration, then stops. Non-media items stop immediately. |
| **Start next** | Completes or skips the current item and starts the next queued item. |
| **Break after current** | Arms an open announcer break after the current media item finishes. |

The deck displays the expected finish time and activates INTRO TALK or OUTRO TALK cues when filename metadata provides those values.

5. Choose an automation mode

| Mode | Behavior |
| --- | --- |
| **Normal** | Completed media advances automatically to the next item. |
| **Manual** | Completed media does not start another item until the operator acts. |
| **Repeat** | When the queue empties, previously played media from the repeat buffer is queued again. |
| **Random** | The next item is selected randomly from the waiting queue. |

6. Add presenter segments

Use the quick controls above the queue to add operational markers.

| Segment | Behavior |
| --- | --- |
| **Announcer** | Can be open ended or timed. A timed break can continue automatically, depending on the item and station settings. |
| **Pause** | Holds silence for a fixed duration, then continues automatically. |
| **Stop point** | Stops automation and waits for the operator. |


A show or scheduled event can also set Hold Next. When that item finishes, the console enters Announcer Mode and waits for Play or Start next.

Playlists

To create a playlist:

1.Optionally select one or more media items in the library.

2.Select New playlist.

3.Enter a playlist name.

4.Select Add current selection to include selected media.

5.Search the complete library and select Add beside other items.

6.Reorder or remove tracks in the playlist pane.

7.Select Save playlist.

Open the Playlists tab to append a playlist, replace the running order, edit it, or delete it. Deleting a playlist does not change media files.

Hot cart

The hot cart provides nine one-key shortcuts for frequently used jingles, identifiers, beds, or emergency items.

1.Select a media item in the library.

2.Select Assign hot key.

3.Choose a slot from 1 through 9.

4.Click the hot-cart pad or press its number key when the cursor is not inside an input field.

Firing a hot slot queues the assigned item next. It does not interrupt the item currently playing.

Show planning and run sheets

The Show Centre extends playlists with dates, presenters, planned times, training notes, typed sections, and actual operation records.

Create a show

1.Open Shows and select New show.

2.Enter a show name, date, planned start, planned end, and at least one announcer.

3.Add optional announcers and training notes.

4.Add music or video from the complete media library.

5.Add sections such as a show intro, announcer talk, advertisement, show outro, announcer break, timed pause, or stop point.

6.Reorder the planned items.

7.Review the timing summary for an exact, early, late, or estimated finish.

8.Select Save show.

Airwave Console calculates the planned start time of each item from the show start and known durations. An open or unknown-duration item makes later start times estimates.

Load or start a show

| Action | Behavior |
| --- | --- |
| **Append** | Adds the show items to the end of the current running order. |
| **Replace queue** | Replaces all waiting items with the show. |
| **Start show** | Stops the current item after confirmation, replaces the queue, marks the show active, and starts its first item. |
| **Delay** | Places one connected song before the show and records it as an unplanned delay item. |
| **Review** | Opens the planned or actual run-sheet comparison. |
| **Planned PDF** | Downloads the calculated planned run sheet. |
| **Duplicate** | Creates an editable copy of the show. |


While a show is active, media added through normal queue or emergency controls can be recorded as unplanned show content. Select End show to finish the active item, archive the actual run, and open the actual review.

Export run sheets

The planned PDF includes station, show, announcer, date, planned time, notes, calculated item starts, durations, filenames, talkover values, and operator-control behavior.

The actual PDF includes exact local start times, elapsed durations, results, filenames, planned comparisons, and unplanned markers. An actual PDF becomes available after the show has recorded entries.

Scheduled events

Select Add event under Scheduled events to create a trigger.

| Option | Choices and behavior |
| --- | --- |
| **Event type** | Media file, playlist, announcer break, timed pause, or stop point. |
| **Repeat** | Once or every day. Enhanced shows use their own scheduled date and time. |
| **Soft timing** | Places the scheduled content at the front of the waiting queue. If the console is idle, playback starts. |
| **Hard timing** | Interrupts the current item and starts the scheduled content immediately. |
| **Maximum lateness** | Prevents an event from running after its allowed late window. |
| **Hold Next** | Enters Announcer Mode after the scheduled item or playlist and waits for the operator. |

Scheduled times use the computer's local clock. The page must remain open for the scheduler to check events.

A scheduled show can either become ready at its planned time or auto-start when the output is idle. If another item is active, the show is prepared for the operator rather than interrupting automatically.

Audio input and output

Open Settings or select Audio I/O on the live deck.

Program output

Choose a listed output device when browser and operating-system support is available. This can be a sound card, USB interface, mixer, headphones, or another exposed output. If routing is unavailable, the application continues with the system default.

Audio input

Choose an input and select Enable input. The browser will request permission. The application displays an input-level meter and can monitor that input through the selected program output.


Feedback warning: Input monitoring can create loud feedback when an open microphone and speakers share the same room. Start with monitoring disabled or at a low level, and prefer headphones or a properly routed mixer.

The selected input is released when it is disabled or when the page is hidden or closed.

Session logs

Airwave Console maintains two related records.

| Record | Scope |
| --- | --- |
| **Browser history** | Persists in application storage and is limited to the number of entries selected in Settings. It supports the Previous control and deck history. |
| **Session played-media log** | Covers media played since the current page load. It can be reviewed and downloaded as CSV. |


The CSV includes sequence, local play date and time, ISO start and end timestamps, title, filename, result, source, path, filename duration, and browser-reported duration.

Select End Session to review recent entries. If the session contains played media, the console asks for a CSV download before enabling its close action. A manually opened browser tab may still need to be closed with the browser's tab control.

Backup and restore

Open Station Data to manage application records.

| Action | Result |
| --- | --- |
| **Download JSON** | Exports station name, folder labels, indexed media metadata, playlists, queue, schedules, shows, run sheets, hot-cart assignments, history, and settings. |
| **Choose JSON file** | Replaces the current setup with a compatible backup after confirmation. |
| **Reconnect available folders** | Requests access again for remembered folders where supported. |
| **Reset local data** | Clears application data from the current browser context after two confirmations. Source files are not changed. |

Backups do not contain media files or browser folder permissions. After importing a backup, reconnect each listed media folder before playback.

Settings

| Setting | Purpose |
| --- | --- |
| **Station name** | Changes the application header, browser title, and PDF report footer. |
| **Fade stop duration** | Selects an immediate stop or a fade from 0.5 to 5 seconds. |
| **History limit** | Keeps 50, 100, 250, or 500 browser-history entries. |
| **Confirm before Play Now** | Requests confirmation before an immediate action interrupts the current item. |
| **Continue after timed breaks** | Allows timed announcer breaks to advance automatically when not held. |
| **Skip missing files** | Skips disconnected or unavailable media while automation is running instead of stopping on a fault. |
| **Program output** | Selects the browser audio output where supported. |
| **Audio input** | Selects and enables a microphone, USB interface, or mixer input. |
| **Input monitoring** | Sends the selected input to the chosen output at the configured monitor level. |


The deck also stores the selected player mode and output volume.

Keyboard shortcuts

Keyboard shortcuts are ignored while the cursor is inside an input, text area, or selection control.

| Key | Action |
| --- | --- |
| `Space` or `P` | Play, pause, resume, or leave the current presenter segment |
| `S` | Fade stop |
| `N` | Start next |
| `B` | Toggle Break after current |
| `E` | Focus emergency search |
| `/` | Focus media-library search |
| `1` through `9` | Fire the matching hot-cart slot |
| `Escape` | Stop the active 10-second preview |
| `Ctrl+W` or `Command+W` | Open the End Session dialog instead of immediately closing |




Storage and privacy

Airwave Console works locally and does not upload selected media through its application code.

| Data | Storage behavior |
| --- | --- |
| **Media files** | Remain in the folders selected by the user. The application reads them for indexing and playback. |
| **Station configuration** | Stored in browser `localStorage` and IndexedDB for the current origin and browser profile. |
| **Remembered folder handles** | Stored in IndexedDB when the browser supports the enhanced folder picker. Permission may still need to be granted again. |
| **Audio input** | Used as a live browser media stream. It is not recorded or included in backups. |
| **Backups and reports** | Created in the browser and downloaded to the user's device. |




The application never renames, moves, edits, or deletes source media files. Removing a source from Airwave Console removes its reference and indexed records only.

Browser storage is specific to the page's origin. Opening the application from a different URL, port, browser profile, or hosting domain can create a separate station state.

Limitations

Airwave Console is intentionally a local, single-browser application. Consider these boundaries before deployment.

| Limitation | Impact |
| --- | --- |
| **No background service** | Playback and schedules stop when the page is closed or the computer sleeps. |
| **No shared server state** | Data does not automatically synchronize across computers, browsers, or operators. Use JSON backups to move a setup. |
| **No bundled media** | Every operator must have access to the required local folders and reconnect them when permission is lost. |
| **Browser codec dependence** | Some recognized file extensions may not play on every operating system or browser. |
| **Browser permission dependence** | Folder memory, microphone input, and output-device selection vary by browser and security context. |
| **Session CSV resets on reload** | The downloadable session log covers the current page session only. Download it before reloading or closing. |
| **Local-time scheduling** | Clock changes, sleep, tab closure, or an inactive device can cause an event to be late or missed. |
| **No automatic media backup** | JSON backups contain records and settings, not the underlying audio or video. |




Troubleshooting

| Problem | Resolution |
| --- | --- |
| **A source shows Reconnect** | Select **Reconnect** or **Change**, then choose the original folder again. |
| **A file is visible but cannot be queued** | Reconnect its source. Queue controls are disabled for disconnected runtime files. |
| **Playback reports an unsupported format** | Convert the file to a codec supported by the target browser, or test another supported browser. |
| **The title or timing is wrong** | Rename the source file using the documented timing convention, then refresh or reconnect the folder. Source files are never renamed by the application. |
| **No artist appears** | Use `Artist - Title` in the filename or place the file in a clearly named artist folder. |
| **Scheduled content did not run** | Confirm that the page was open, the computer was awake, the local date and time were correct, and the maximum lateness window was not exceeded. |
| **A scheduled show did not auto-start** | Auto-start occurs only when the output is idle. If another item is active, the show is prepared for manual start. |
| **Microphone or mixer input is unavailable** | Use localhost or HTTPS, confirm browser permission, connect the device before opening Settings, then refresh the device list. |
| **The chosen output is ignored** | The browser or operating system may not expose output routing. Use the system default or configure routing at operating-system or mixer level. |
| **Monitoring causes feedback** | Disable input monitoring, reduce the monitor level, use headphones, or correct the external mixer routing. |
| **A backup loads but files do not play** | Reconnect every media folder. Backups do not include file permissions or media content. |
| **Close Browser does not close the tab** | Download the log, then close the tab with the browser control. Browsers may block scripts from closing manually opened tabs. |
| **The console has a different setup at another URL** | Return to the original URL and port, or export JSON from one context and import it into the other. |




Repository structure

A simple public repository can use this layout:

Plain Text


.
├── README.md
├── index.html
└── docs/
    └── assets/
        └── airwave-console-overview.webp



If you keep the original filename, replace index.html with airwave-console-training.html in the structure and links.

Contributing

Contributions should preserve the application's single-file deployment model unless a change clearly requires a different architecture.

1.Fork the repository and create a focused branch.

2.Make changes in the HTML file.

3.Test direct-file mode and localhost mode.

4.Test folder import, playback, queue behavior, keyboard controls, scheduling, exports, backup import, and responsive layout where relevant.

5.Confirm that changes do not rename, move, edit, or delete source media.

6.Open a pull request that explains the problem, approach, testing, and any browser-specific behavior.

When changing stored data structures, maintain backward compatibility through state normalization or document the migration clearly.





