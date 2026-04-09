# Memory Display v6.5 - README

**A personalized orientation display for people with memory challenges, cognitive change, or extended recovery.**

Built with love for Gloria by Marisha Tapera • March 2026

---

## What's New in v6.5

### 🎉 Dynamic Holiday Calculations

Holidays now calculate automatically based on the current year! No more manual date updates needed.

**Fixed Holidays** (same date every year):
- New Year's Day (Jan 1)
- Valentine's Day (Feb 14)
- St. Patrick's Day (Mar 17)
- Juneteenth (June 19)
- Independence Day (July 4)
- Halloween (Oct 31)
- Veterans Day (Nov 11)
- Christmas (Dec 25)
- New Year's Eve (Dec 31)

**Dynamic Holidays** (calculated automatically):
- MLK Jr. Day (3rd Monday in January)
- Presidents' Day (3rd Monday in February)
- Easter Sunday (Computus algorithm - lunar calendar)
- Mother's Day (2nd Sunday in May)
- Memorial Day (last Monday in May)
- Father's Day (3rd Sunday in June)
- Labor Day (1st Monday in September)
- Indigenous Peoples' Day (2nd Monday in October)
- Thanksgiving (4th Thursday in November)

**How it works:**
- Holidays generate automatically when the page loads
- At midnight on January 1st, holidays regenerate for the new year
- Easter uses the traditional Computus algorithm (same method used since 325 AD!)

---

## Core Features

### **Time & Date Display**
- Large, readable time (200px)
- Full date with day of week (90px)
- Automatic day/evening/night color modes

### **Live Weather**
- Auto-updates from Open-Meteo API every 30 minutes
- Based on ZIP code
- Shows temperature, conditions, and weather icon

### **Caregiver Display**
- Shows current caregiver name with heart emoji
- Day shift: 7:00 AM - 6:59 PM (💜 purple heart 8 AM-6 PM)
- Evening transition: 6:00 PM - 9:00 PM (💚 green heart)
- Night shift: 7:00 PM - 6:59 AM (❤️ gray heart in night mode)
- Updates every minute
- Supports substitute caregivers for specific dates

### **Today's Schedule**
- Shows appointments and events for today only
- Past events stay visible (dimmed at 60% opacity)
- Supports one-time events, weekly recurring events
- Icons and formatted times

### **Daily Reminders**
- Medication reminders (morning, afternoon, evening)
- Recurring reminders (water every 60 min, movement every 90 min)
- Full-screen pop-up alerts with gentle chime
- Optional YouTube video integration for movement exercises

### **For Today Suggestions**
- Shows up to 3 daily prompts/suggestions
- Holidays appear automatically with festive colors
- Daily and weekly suggestions
- Specific date-based suggestions

### **Display Modes**
- **Day Mode** (8 AM - 6 PM): Sage green background (#d4dbc1)
- **Evening Mode** (6 PM - 9 PM): Dark gray background (#2a2a2a)
- **Night Mode** (9 PM - 8 AM): Black background (#0a0a0a) with dim gray text

### **Auto-Refresh**
- Refreshes every 15 minutes during waking hours (8 AM - 10 PM)
- Refreshes at midnight daily
- Skips refresh if a featured reminder is active

---

## File Structure

```
memory_display_v6.5.html
├── CSS Styles (~300 lines)
│   ├── Day/Night mode colors
│   ├── Responsive layout
│   └── Featured reminder overlay
│
├── Configuration Section (Lines 418-670)
│   ├── Location (ZIP code)
│   ├── Caregivers (day/night shifts)
│   ├── Substitute caregivers
│   ├── Events and appointments
│   ├── Medication times
│   ├── Daily suggestions
│   └── Display timing settings
│
├── Dynamic Holiday Functions (Lines 672-761)
│   ├── calculateEaster()
│   ├── getNthWeekday()
│   ├── getLastWeekday()
│   └── getDynamicHolidays()
│
└── Core Functions (~500 lines)
    ├── Time & weather updates
    ├── Reminder generation
    ├── Display rendering
    └── Featured reminder system
```

---

## How to Use

### **First Time Setup**

1. **Download** the `index.html` file from the zip
2. **Edit** the CONFIGURATION SECTION (starts around line 418)
3. **Upload** to your web hosting or open locally
4. **Full screen:** Press F11 (PC) or ⌘ Ctrl F (Mac)
5. **Display:** Open in Chrome or Edge on any device

### **Updating Caregivers**

```javascript
// DAY SHIFT (7 AM - 7 PM)
const WEEKLY_CAREGIVERS = [
    { dayOfWeek: 1, name: "Aster" },     // Monday
    { dayOfWeek: 2, name: "Aster" },     // Tuesday
    // ... etc
];

// SUBSTITUTE DAY SHIFT
const SUBSTITUTE_CAREGIVERS = [
    { date: "2026-04-15", name: "Mariama" },
];

// NIGHT SHIFT (7 PM - 7 AM)
const NIGHT_CAREGIVERS = [
    { dayOfWeek: 0, name: "Marisha" },   // Sunday night
    // ... etc
];
```

### **Adding Appointments**

```javascript
const SPECIFIC_DATE_EVENTS = [
    { 
        date: "2026-04-15", 
        time: "10:30", 
        text: "Doctor appointment", 
        featured: true, 
        icon: "🏥" 
    },
];
```

**Important formatting rules:**
- Dates: `"YYYY-MM-DD"` with leading zeros (e.g., `"2026-04-05"` not `"2026-4-5"`)
- Times: `"HH:MM"` in 24-hour format (e.g., `"14:30"` not `"2:30 PM"`)
- **Always put a comma at the end** (except the very last item)

### **Common Time Conversions**

| 12-hour | 24-hour |
|---------|---------|
| 12:00 AM | 00:00 |
| 8:00 AM | 08:00 |
| 12:00 PM | 12:00 |
| 1:00 PM | 13:00 |
| 2:30 PM | 14:30 |
| 6:00 PM | 18:00 |
| 9:00 PM | 21:00 |

### **Adding Weekly Events**

```javascript
const WEEKLY_EVENTS = [
    { 
        dayOfWeek: 0,      // 0=Sunday, 1=Monday, etc.
        time: "10:30", 
        text: "Church service", 
        featured: false, 
        icon: "⛪" 
    },
];
```

### **Customizing Medication Times**

```javascript
const DAILY_REMINDERS = [
    { time: "08:00", text: "Morning medication", featured: true, icon: "💊" },
    { time: "13:00", text: "Afternoon medication", featured: true, icon: "💊" },
    { time: "18:00", text: "Evening medication", featured: true, icon: "💊" },
];
```

### **Adding Movement Reminders with Video**

```javascript
const RECURRING_REMINDERS = [
    { 
        interval: 135,              // Every 135 minutes
        startTime: "12:45", 
        endTime: "17:45", 
        text: "Move your arms and legs", 
        featured: true, 
        icon: "🤸",
        videoId: "YOUR_YOUTUBE_ID"  // Optional: 11-character YouTube video ID
    },
];
```

**Note:** YouTube video embedding only works if the video allows embedding. For guaranteed functionality, use unlisted/private YouTube videos or local video files in MemoryLUV Pro.

---

## Troubleshooting

### **Appointments not showing up**

Check:
- Date format has leading zeros: `"2026-04-05"` ✓ not `"2026-4-5"` ✗
- Time is in 24-hour format: `"14:30"` ✓ not `"2:30 PM"` ✗
- Comma at end of line (except last item)
- Date matches today's date

### **Display shows blank/error**

- Check browser console (F12) for error messages
- Look for missing commas in your configuration
- Verify all quote marks match (`"` not `'` mixed with `"`)

### **Wrong caregiver showing**

- Check that substitute caregiver date is correct
- Verify day of week numbers (0=Sunday, 1=Monday, etc.)
- Remember night shift date is when the shift STARTS at 7 PM

### **Holiday showing on wrong day**

- This should no longer happen with v6.5! Holidays calculate dynamically.
- If a holiday seems wrong, check that your device's date/time is correct
- Holidays regenerate automatically on January 1st of each year

### **Changes not appearing**

- Wait 15 minutes for auto-refresh OR manually refresh (F5 or Ctrl+R)
- Make sure you saved your changes before uploading
- Clear browser cache if needed

---

## Technical Details

### **Font Sizes**
- Time: 200px
- Date: 90px
- Weather: 96px (temperature), 100px (icon)
- Caregiver: 65px
- Section titles: 42px
- Schedule items: 36px

**Note:** For better readability, you can increase schedule text sizes:
- Line 181: Change `font-size: 42px` to `45px` (section titles)
- Line 188: Change `font-size: 36px` to `55px` (schedule items)

### **Color Palette**

**Day Mode:**
- Background: #d4dbc1 (sage green)
- Text: #1a1a1a (almost black)
- Borders: #b5bd9a
- Schedule items: #c5cdb0

**Evening Mode:**
- Background: #2a2a2a (dark gray)
- Text: #e8e8e8 (light gray)
- Schedule items: #363636

**Night Mode:**
- Background: #0a0a0a (black)
- Text: #666666 (dim gray)
- Borders: #2a2a2a
- Schedule items: #1a1a1a

### **Browser Compatibility**
- Chrome/Edge: Full support ✓
- Safari: Full support ✓
- Firefox: Full support ✓
- Works on Windows, Mac, iOS, Android

### **Requirements**
- Internet connection (for weather API)
- Modern browser (Chrome, Edge, Safari, Firefox)
- Any device with a screen (computer, tablet, TV)

---

## Emoji Reference

### **Medical & Health**
🏥 Hospital | 💊 Medication | 🩺 Stethoscope | 💉 Injection | 🧑‍⚕️ Doctor

### **Therapy & Exercise**
🏋️ PT | ✍🏾 OT | 🤸 Movement | 🧘🏾‍♀️ Meditation | 🚶🏾‍♀️ Walking

### **Communication**
🖥️ Telehealth | 💻 Computer | 📞 Phone | 💬 Chat

### **Personal Care**
💇🏾‍♀️ Hair | 💆🏾‍♀️ Massage | 🛁 Bath

### **Social & Activities**
🧑‍🧑‍🧒‍🧒 Family | 👥 People | ☕ Coffee | ⛪ Church | 📺 TV | 🎵 Music

### **Daily Life**
💧 Water | 🤸 Movement | 🚙 Car | 📋 Planning

---

## Version History

### v6.5 (April 2026)
- ✨ NEW: Dynamic holiday calculations (Easter, MLK Day, Memorial Day, etc.)
- ✨ Holidays now accurate for any year
- ✨ Auto-regenerate holidays on January 1st
- 🎉 Easter now uses proper Computus algorithm

### v6.4.2 (March 2026)
- ✨ YouTube video integration for movement reminders
- ✨ Styled countdown before video playback
- ✨ Muted autoplay for videos

### v6.3.2 (March 2026)
- 🐛 Fixed timezone bug (appointments showed a day early after 8 PM)
- ✨ Font size increases (42px→45px titles, 36px→55px items)
- ✨ Gray heart in night mode (CSS-styled for Windows 10 compatibility)

### v6.3.1 (March 2026)
- ✨ Caregiver shift timing fixes
- ✨ Past events stay visible all day (dimmed)

### v6.3 (March 2026)
- ✨ Liturgical calendar support (removed in base, moved to Pro)

### v6.2 and earlier
- Initial development and testing

---

## Credits

**Built with love by:** Marisha Tapera  
**For:** Gloria (Mom)  
**Date:** March-April 2026  
**Technology:** HTML, CSS, JavaScript  
**Weather API:** Open-Meteo (free, no API key required)  

**Special thanks to:** Claude (Anthropic) for development partnership

---

## License & Usage

This display is **personal use only**. It was built as a caregiving tool for a specific individual.

**You may:**
- Use it for your own family member
- Modify it for your personal needs
- Share the concept with other caregivers

**You may not:**
- Sell this code
- Use it commercially
- Redistribute it as a product

If this display has helped you and you'd like to support more tools like it, consider:
- Sharing your experience with other caregivers
- Providing feedback on what works/doesn't work
- Contributing to open-source caregiving tools

---

## Support & Contact

For questions about this display or MemoryLUV products:
- Website: (coming soon)
- Email: (coming soon)

---

**Made with 💜 for caregivers everywhere**

*"For the person you love"*
