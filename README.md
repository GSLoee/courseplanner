# CoursePlanner: high-fidelity prototype (ITEC 3230)

A clickable prototype of the Course Planning & Registration Assistant. It is one file
(`index.html`) with no installation and no server. All courses, instructors and ratings
are sample data.

---

## How to run it

**Option 1: double-click (easiest, works offline)**
1. Unzip the folder.
2. Double-click `index.html`. It opens in your default browser.
   Chrome or Edge is recommended. Firefox and Safari also work.
3. With internet the page uses its Rubik and Nunito Sans fonts. Offline it falls back to
   system fonts. Everything else works the same.

**Option 2: the hosted link from Claude**
Open the artifact link in Chrome. It is private to the account that made it. Teammates who
need it must be added through the page's **Share** menu, or they can use Option 1 instead.

**Option 3: local web server (only if your browser blocks Option 1)**
```
cd path/to/this/folder
python3 -m http.server 8000      # on Windows: py -m http.server 8000
```
Then open http://localhost:8000 in your browser.

---

## Before each session (2 minutes)

1. Open the prototype and press **Shift + M** to open **Study tools**
   (or click **Study tools** at the bottom right of the page).
2. Click **Reset prototype**, then **Yes, reset**. This restores the starting scenario:
   - Plan A has a clash and a Friday class
   - Plan B overlaps an evening course
   - The cart is empty
   - No blocked time is set
3. Click **Clear study data** if earlier test data is still there. Type the participant ID,
   for example `P1-Instructor`.
4. Press **Shift + M** again to hide the panel.
5. Set browser zoom to 100% (Ctrl/Cmd + 0). Use full screen (F11) to hide your bookmarks bar.
6. In Zoom, share **only this browser window**. Then go to **Remote Control → Give mouse/keyboard
   control** to the instructor.

The prototype saves its state in the browser. Reloading the page keeps the participant's
progress. Only **Reset prototype** returns it to the start.

---

## Study tools (for the note-taker)

| Control | What it does |
|---|---|
| **Start T1…T4** | Starts the timer for that task |
| **Success / Partial / Fail** | Stops the timer and records the outcome |
| **Assist +1** | Records that you gave a hint |
| **Error +1** | Records an error that wasn't counted automatically |
| **Copy results (CSV)** | Copies time, result, clicks, errors and assists for each task. Paste into Excel or Google Sheets |
| **Copy event log (CSV)** | Copies every click, navigation and error with a timestamp |

The panel counts some things automatically while a task is running:
- **Clicks:** every click on the page
- **Errors:**
  - clicking a disabled button
  - picking a greyed-out section
  - an invalid "Block time" form
  - creating a new clash
  - choosing a conflicting AI alternative

The panel appears on the shared screen. Start and stop tasks between tasks, not while the
participant is working.

---

## The scenario

The participant plays **Bob Mitchell**, a 2nd-year IT student who:
- works Tuesday and Thursday evenings, 18:00–22:00
- wants no Friday classes and 15 credits in Winter 2027
- is interested in UX design and data

### Starting state
- **Plan A (main plan, 9 credits)**
  - ITEC 3220 LEC A
  - ITEC 3010 LEC M, which **clashes** with ITEC 3220 on Mon/Wed at 10:00
  - ITEC 3210 LEC Q, which is on **Friday**
- **Plan B (15 credits, "shared by a classmate")**
  - Has no clashes
  - ITEC 3020 LEC B is **Thursday 19:00–22:00**, which overlaps Bob's work once he blocks it
  - Has a 7.5-hour gap on Thursday

### Expected solution paths (for the team, not the participant)

| Task | A successful path |
|---|---|
| **T1: Find a course** | Search → filter *Core ITEC 3000-level* (+ *Fits Plan A*) → open ITEC 3330 or ITEC 3020 → choose a section with a well-rated instructor that fits → add to Plan A. The participant should notice that ITEC 4020 is greyed out because a prerequisite is missing. |
| **T2: Fix the timetable** | Timetable → **Block time** Tue + Thu 18:00–22:00 "Work" → fix the clash: change ITEC 3010 from LEC M to **LEC N** → move ITEC 3210 from Friday LEC Q to **LEC A** (Tue/Thu 10:00). |
| **T3: Compare** | Compare → Plan A vs Plan B → notice that Plan B overlaps the blocked work time (its *Send to cart* is disabled and says why) → keep Plan A as the main plan. Plan B has more credits, which makes this a trade-off. |
| **T4: AI and register** | Assistant → check the goals (15 credits, no Friday, interests) → **Suggest changes** → read the *Why* and *Check* columns → accept one good option (e.g. ITEC 3020 LEC A or ITEC 3330 LEC A) → **reject or swap** MATH 2560 LEC B (2.9-rated instructor, makes Monday a 9-hour day) → Timetable → **Send to cart** → read the readiness checklist → turn on the reminder. |

If the participant skips T2, the assistant also suggests the clash and Friday fixes as
switch suggestions. Every path still works.

---

## What works and what is only shown

**Working**
- Navigation between all 7 screens
- Search with all main filters and sorting
- Course detail with eligibility, requirement impact and sections
- Rate My Professors score and rating count for each section
- Adding, changing and removing sections
- Clash detection, with orange banners and blocks
- Blocked personal time
- Greyed-out sections with the reason shown
- Duplicating, deleting and setting the main plan
- Side-by-side compare with mini timetables
- AI suggestions with Why and Check columns: Accept, Reject, Swap and Undo
- Pending AI blocks shown dashed on the timetable
- Cart with readiness checklist and reminder
- Undo on every change
- Degree progress that updates from the main plan

**Present but not functional**
These are designed but show "not part of this prototype":
- Profile, Settings, Advisor messages, Sign out
- Summer 2027 term
- Online, campus and instructor filters
- The RMP links, which explain they would open the instructor's page
- **Register now**, which stays disabled and explains that enrolment opens Mon, Dec 7 at 9:00 AM

---

## Files
- `index.html`: the whole prototype (HTML, CSS and JavaScript in one file)
- `README.md`: this file
