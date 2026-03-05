# TimeBox

A mobile-first time tracking web app that syncs to Google Calendar. Log your day in 15-minute blocks across predefined categories, then review a daily summary with a donut chart.

## Features

- **15-minute time blocks** — long-press and drag on the schedule to select a time range, then pick a category
- **Google Calendar sync** — all entries are stored as events in a dedicated Google Calendar
- **Day navigation** — browse past days; future dates are locked
- **Daily summary** — donut chart showing time breakdown by category, with per-slice labels and a legend
- **Untracked time** — optionally show the remaining unlogged hours in the chart
- **Percentages** — recalculate automatically based on whether untracked time is included

## Categories

| Emoji | Name | | Emoji | Name |
|-------|------|-|-------|------|
| 💼 | Work | | 📚 | Learning |
| 🏢 | Business | | ☕ | Break |
| 🤝 | Meetings | | 🏃 | Exercise |
| 🧠 | Deep Work | | 😴 | Sleep |
| 📧 | Email/Admin | | 🍽️ | Meal |
| 🌱 | Garden | | 📺 | Entertainment |
| 🎨 | Creating | | 📌 | Custom |

## Setup

### 1. Google Cloud project

1. Go to [Google Cloud Console](https://console.cloud.google.com) and create a project
2. Enable the **Google Calendar API**
3. Under **APIs & Services > Credentials**, create an OAuth 2.0 Client ID for a Web Application
4. Add your domain (or `http://localhost` for local dev) to the authorised JavaScript origins

### 2. Google Calendar

Create a new Google Calendar dedicated to TimeBox entries and copy its Calendar ID from **Settings > Integrate calendar**.

### 3. Configuration

Open `index.html` and update the two constants near the top of the `<script>`:

```js
const CLIENT_ID   = 'YOUR_OAUTH_CLIENT_ID.apps.googleusercontent.com';
const CALENDAR_ID = 'YOUR_CALENDAR_ID@group.calendar.google.com';
```

### 4. Serve

The app is a single `index.html` file with no build step. Serve it with any static file server, for example:

```bash
npx serve .
# or
python3 -m http.server
```

Then open `http://localhost:3000` (or whichever port) in your browser.

## Usage

| Action | How |
|--------|-----|
| Log a block | Long-press and drag on the timeline, then select a category |
| Log custom activity | Long-press, drag, then type a name in the text field and tap LOG |
| Delete a block | Tap the x button on any entry block |
| Navigate days | Use the left/right arrows in the header (future dates are disabled) |
| Jump to today | Tap the TODAY button |
| View summary | Tap the half-circle (◑) button in the header |
| Toggle untracked | Use the "Show untracked" checkbox in the summary view |

## Data format

Each time block is stored as a Google Calendar event with the summary prefix `[TB]` followed by the category emoji and name, e.g. `[TB] ☕ Break`. This makes entries identifiable in Google Calendar without cluttering other events.
