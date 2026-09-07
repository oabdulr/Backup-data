# Mosque Prayer App

A browser-based prayer display built for my local mosque, Concord UMCC. It brings the current time, daily prayer times, congregation schedules, and the next prayer into one screen designed for large displays and smaller browser windows.

## Features

- Live clock and date, refreshed every second.
- Daily prayer-time calculations using PrayTimes.js.
- Configurable congregation (iqamah) times and a Friday prayer schedule.
- Highlighting for the next prayer.
- Responsive layout using HTML, CSS, and Tailwind CSS.
- Automatic polling for changes to the page HTML, allowing an open display to reload when that document changes.

## Run locally

The application is a static website with no backend or build step. With Python 3 installed:

```bash
git clone https://github.com/oabdulr/Backup-data.git
cd Backup-data
python -m http.server 8000 --bind 127.0.0.1
```

Open [localhost:8000](http://localhost:8000). On Windows, use `py` instead of `python` if that is how Python is installed.

An internet connection is needed to load the external Tailwind script, fonts, and background texture. Page-update polling requires HTTP or HTTPS.

## Configuration

Edit the configuration block in [index.html](index.html) to change the congregation times:

```javascript
var iqamah_fajr = "6:00";
var iqamah_zuhr = "1:30";
var iqamah_asr = "5:15";
var iqamah_isha = "9:15";
var iqamah_maghrib_added_minutes = "+ 5";
```

The Maghrib setting is displayed as a textual offset alongside the calculated time; it does not currently compute a separate clock time. Friday prayer times are edited directly in the HTML.

Location and calculation settings are in `getNow()` in [main.js](assets/js/main.js). The current configuration uses coordinates `[35.227, -80.843]`, the Makkah calculation method, and a base UTC offset of `-5`. Daylight-saving detection and the displayed clock depend on the browser's local time settings. Both today's and tomorrow's calculations must be updated when changing location.

## Code organization

- [index.html](index.html): display layout and congregation schedule settings.
- [assets/css/main.css](assets/css/main.css): custom presentation styles.
- [assets/js/main.js](assets/js/main.js): prayer calculations, clock updates, highlighting, and page-update polling.

## Current limitations

The next-prayer time selection needs correction: daytime prayers can display tomorrow's calculated time. Date rollover and time-zone behavior also need automated tests. Verify the schedule against the mosque's approved times before relying on the display.

Configuration currently requires editing source files. HTML polling does not detect changes made only to external JavaScript or CSS files. The repository does not yet include automated tests.

## Attribution

Prayer calculations incorporate PrayTimes.js 2.3, credited in the source to PrayTimes.org. The display also uses Tailwind CSS and externally hosted fonts and texture assets. Those components remain subject to their respective terms.
