# Memory Display - Version 6.3 README
## Release Date: February 19, 2026

---

## What's New in Version 6.3

### Major Features Added:
1. **Episcopal/Christian Liturgical Calendar** - Automatic calculation of church holidays
2. **Easter calculation algorithm** - Dates update automatically each year
3. **13 additional liturgical observances** - Ash Wednesday through Trinity Sunday
4. **Visibility-optimized liturgical colors** - Traditional colors adjusted for readability

### Liturgical Holidays Included:

**Lent & Holy Week:**
- Transfiguration Sunday (Last Sunday before Lent)
- Ash Wednesday
- Palm Sunday
- Maundy Thursday
- Good Friday
- Holy Saturday
- Easter Sunday (updated wording: "Christ is Risen! Happy Easter!")

**Easter Season:**
- Ascension Day (40 days after Easter)
- Pentecost Sunday (50 days after Easter)
- Trinity Sunday (Sunday after Pentecost)

**Advent & Christmas:**
- First Sunday of Advent
- Christmas Eve
- Epiphany (January 6)

**Other:**
- All Saints' Day (November 1)

### How It Works:

- **Automatic calculation**: Easter and all related dates recalculate each year
- **Priority display**: Liturgical holidays appear in "For Today" suggestions
- **Appropriate icons**: ✝️ for solemn days, 🌿 for Palm Sunday, 🔥 for Pentecost, etc.
- **Visibility-first colors**: Traditional liturgical colors adjusted to be readable in all modes

---

## Schedule Changes in 6.3 Base (from 6.2.4):

- Morning medication moved to 8:00 AM
- Water reminder ends at 5:00 PM (was 6:00 PM)
- Added: CRA Ultrasound appointment (Feb 20)
- Added: Tapera clan visit (Feb 22)

---

## Current Configuration

### Caregivers:

**Day Shift (7:00 AM - 6:59 PM):**
- **Monday-Friday:** Aster
- **Saturday-Sunday:** Dionne
- Displays as: "[Name] is here today 💜" (purple day, green evening, gray night)

**Night Shift (7:00 PM - 6:59 AM):**
- **Every night:** Marisha
- Displays as: "[Name] is here tonight 💜/💚/🩶"

### Medications (Pop-up alerts only):
- 8:00 AM - Morning medication
- 1:00 PM - Afternoon medication
- 6:00 PM - Evening medication

### Recurring Reminders (Pop-up alerts only):
- **Water:** Every hour from 11:00 AM to 5:00 PM
- **Movement:** Every 90 minutes from 12:45 PM to 5:45 PM

### Weekly Events (Shows in schedule):
- **Sunday 10:30 AM** - Church service

### Daily Suggestions (Shows in "For Today"):
- 🧘🏾‍♀️ Breathe deeply

### Weekly Suggestions (Shows in "For Today"):
- 💬 Call a friend? (Mondays and Thursdays)

---

## Liturgical Calendar Colors

These colors have been optimized for visibility across day, evening, and night modes:

- **Ash Wednesday:** Medium Purple (#9370DB)
- **Transfiguration:** Light Gold/Khaki (#F0E68C)
- **Palm Sunday:** Lime Green (#32CD32)
- **Maundy Thursday:** Peru/Tan (#CD853F)
- **Good Friday:** Firebrick Red (#B22222)
- **Holy Saturday:** Dark Gray (#A9A9A9)
- **Easter:** Gold (#FFD700) with ✝️
- **Ascension:** Sky Blue (#87CEEB)
- **Pentecost:** Crimson Red (#DC143C)
- **Trinity Sunday:** Gold (#FFD700)
- **First Advent:** Medium Purple (#9370DB)
- **Christmas Eve:** Gold (#FFD700)
- **Epiphany:** Gold (#FFD700)
- **All Saints:** Gold (#FFD700)

All colors automatically dim to gray (#666666) in night mode (9 PM - 8 AM).

---

## How Easter Calculation Works

The system uses the **Computus algorithm** to calculate Easter Sunday for any year, then calculates all related observances:

- **Fixed offset dates:** Ash Wednesday (-46 days), Palm Sunday (-7 days), etc.
- **Automatic yearly update:** Calculations run for current and next year
- **No manual updates needed:** Liturgical calendar updates itself annually

### Easter-Based Dates:
- Transfiguration: Last Sunday before Ash Wednesday
- Ash Wednesday: 46 days before Easter
- Palm Sunday: 7 days before Easter
- Maundy Thursday: 3 days before Easter
- Good Friday: 2 days before Easter
- Holy Saturday: 1 day before Easter
- Easter Sunday: Calculated via Computus
- Ascension: 39 days after Easter (always Thursday)
- Pentecost: 49 days after Easter (Sunday)
- Trinity Sunday: 56 days after Easter (Sunday)

### Fixed Dates:
- First Sunday of Advent: 4 Sundays before Christmas
- Christmas Eve: December 24
- All Saints' Day: November 1
- Epiphany: January 6

---

## Editing Liturgical Holidays

The liturgical calendar is **automatically generated** and doesn't need editing. However, if you want to:

**Change the wording:**
Find the `generateLiturgicalHolidays` function and edit the `text` field for any observance.

**Change colors or icons:**
Edit the `emoji` or `color` fields in the same function.

**Disable specific observances:**
Comment out or remove the section that adds that observance to the `liturgical` array.

**Add new observances:**
Follow the pattern in the function, calculating the date relative to Easter or as a fixed date.

---

## Combining Secular and Liturgical Holidays

The system now tracks:
- **16 secular holidays** (Federal holidays + Valentine's, Halloween, etc.)
- **13 liturgical holidays** (Automatically calculated)
- **Total: 29 recognized observances**

When multiple observances fall on the same day, the first one found displays (liturgical are checked after secular in the combined list).

---

## Version History

### Version 6.3 (Feb 19, 2026)
- Added Episcopal/Christian liturgical calendar (13 observances)
- Automatic Easter calculation with Computus algorithm
- Auto-updating dates for all Easter-related observances
- Easter changed from 🐣 to ✝️ with "Christ is Risen!" text
- Visibility-optimized liturgical colors
- Schedule updates: Morning med 8AM, water ends 5PM

### Version 6.2 (Feb 11, 2026)
- Added automatic holiday recognition (16 secular holidays)
- Festive color-coded holidays in "For Today"
- Holiday colors dim to gray in night mode
- Day/night shift caregivers with different wording
- Color-coded caregiver hearts (purple day, green evening, gray night)

### Version 6.1 (Feb 10, 2026)
- Optimized layout: top 40%, bottom 60%
- Reduced caregiver name to 65px
- Vertically centered caregiver line
- Eliminated scrolling

### Version 6.0 (Feb 9, 2026)
- Two-column layout (Schedule 2/3, Suggestions 1/3)
- Caregiver name display
- "For Today" suggestions widget

---

## Technical Notes

### Easter Algorithm:
The Computus algorithm is the standard method used by Western Christianity to calculate Easter. It accounts for:
- The lunar calendar
- The spring equinox
- Ensuring Easter falls on a Sunday
- The 19-year Metonic cycle

### Performance:
- Liturgical dates are calculated once on page load
- Calculations are lightweight (< 1ms)
- Two years calculated (current + next) to handle year transitions

### Maintenance:
- No manual updates needed for moving dates
- Page automatically recalculates on midnight refresh
- Works correctly across year boundaries

---

## For Your Records

**Church:** Episcopal/Anglican tradition
**Service time:** Sundays 10:30 AM (local church via Zoom)
**Additional viewing:** Washington National Cathedral (YouTube)
**Liturgical season awareness:** Now automatically maintained

---

## Support

The liturgical calendar follows the Western Christian/Episcopal calendar. Dates are calculated using the Gregorian calendar and standard Computus algorithm used by most Western churches.

If observances seem incorrect, verify against your church's published liturgical calendar for the year.

---

## File Naming

Save as:
- `memory_display_v6.3.html`
- `README_v6.3.md`
