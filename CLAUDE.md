# Saturday Supper Club

A simple web app for planning weekly Saturday dinners with friends, family, and acquaintances. Built to help Alan and his wife build community by hosting regular suppers.

## Project Overview

Single-page HTML app hosted on GitHub Pages at https://amn41.github.io/supperclub

Data persistence via JSONBin.io (free tier). Both users share the same bin so they see the same guest list and calendar.

## Tech Stack

- Single `index.html` file (HTML + CSS + vanilla JS)
- No build step, no dependencies
- JSONBin.io for data storage (API key hardcoded - this is intentional, security not a concern)
- Hosted on GitHub Pages

## Data Model

Guests are stored as an array in JSONBin with this shape:

```javascript
{
  id: string,           // timestamp-based ID
  name: string,
  relation: string,     // how they know them (e.g., "Neighbours", "Work friends")
  notes: string,        // dietary needs, etc.
  scheduledDate: string | null,  // "YYYY-MM-DD" or null if unscheduled
  status: 'proposed' | 'confirmed' | null  // null if unscheduled
}
```

## Guest States

1. **Candidate** - on the list, no date yet (`scheduledDate: null`)
2. **Proposed** - date picked but not confirmed with them yet (`status: 'proposed'`)
3. **Confirmed** - they've said yes (`status: 'confirmed'`)

## Key Files

- `index.html` - the entire app
- `CLAUDE.md` - this file

## JSONBin Config

The bin ID and API key are defined at the top of the `<script>` section in index.html:

```javascript
const JSONBIN_API_KEY = '...';
const JSONBIN_BIN_ID = '...';
```

## Design Notes

- Warm, inviting aesthetic (cream, terracotta, olive colors)
- Fraunces for headings, Inter for body text
- Mobile responsive
- Year defaults to 2026
- Calendar shows all 52 Saturdays for the selected year
- Proposed dates show in amber/yellow, confirmed in green

## Common Tasks

### Adding a new guest field
1. Update the `addGuest()` function to include the new field
2. Update `openEditGuestModal()` to populate the form
3. Update `saveGuest()` to save it
4. Add any necessary UI in the modal HTML

### Changing styles
All CSS is in the `<style>` block at the top of index.html. Key CSS variables are in `:root`.

### Debugging data issues
Open browser console and check:
- `guests` - current in-memory guest array
- `loadData()` - manually reload from JSONBin
- `saveData()` - manually save to JSONBin