# ⏱️ Work Time Calculator

A web application for calculating work time based on entry/exit access logs.

## 📋 Description

Work Time Calculator is a web application that automatically calculates your work time based on access control system logs. The application works in real-time - as soon as you paste your data, results are displayed and updated every second.

## 🚀 How to Use

### 1. Open the Application

Open the `WorkTimeCalculator.html` file in a web browser (Chrome, Firefox, Edge, etc.).

### 2. Paste Your Log Data

Copy the data from your access control system and paste it into the text field.

**Expected format:**
```
<Entry/Exit>	<Location>	<date and time>	<Processed/Pending>	<Status(OK,Yes,No,Invalid)>
```
**Example:**
```
Entry 	BL Cajavec GLAVNI ULAZ 	2026-01-29 06:59:59 	Processed 	OK
Exit 	BL Cajavec GLAVNI ULAZ 	2026-01-29 07:18:02 	Processed 	OK
Entry 	BL Cajavec GLAVNI ULAZ 	2026-01-29 07:48:20 	Pending 	OK
```

### 3. View the Results

Results are automatically displayed and include:

- **Total Work Time** - Total time spent working
- **Total Break Time** - Total break duration
- **Break Penalty** - Penalty for insufficient break time
- **Final Work Time** - Final calculated work time
- **Expected Leave Time** - Expected time to leave (if you're still at work)

## 📊 How the Application Calculates

### Work Time

The application recognizes `Entry` and `Exit` records and calculates the time between them as work time.

### Breaks

Time between an `Exit` and the next `Entry` record is calculated as break time.

### Break Penalty

- Minimum required break is **30 minutes (0.5 hours)**
- If total break time is less than 30 minutes, the difference is deducted from work time
- Example: If you have 20 minutes of break, the penalty is 10 minutes

### Currently at Work

If the last record is an `Entry` (without a corresponding `Exit`), the application assumes you're still at work and:
- Uses the current time for calculations
- Shows expected leave time for a 7.5h work day considering the break time
- Updates every second

## ⚠️ Notes

### Invalid Records

Records marked as `Invalid` are automatically ignored. This includes duplicate entries/exits that may occur due to system errors.

**Example:**
```
Entry	BL Cajavec GLAVNI ULAZ	2025-11-06 07:08:51	Processed	OK
Exit	BL Cajavec GLAVNI ULAZ	2025-11-06 12:22:19	Processed	OK
Exit	BL Cajavec GLAVNI ULAZ	2025-11-06 12:22:22	Processed	Invalid  ← Ignored
Entry	BL Cajavec GLAVNI ULAZ	2025-11-06 12:58:45	Processed	OK
```

### Clear Button

Use the **Clear** button to erase all data and start fresh.

## 📱 Compatibility

The application works in all modern web browsers:
- Google Chrome
- Mozilla Firefox
- Microsoft Edge
- Safari

No installation or internet connection required - everything runs locally in your browser.

## 📐 Calculation Example

**Input data:**
```
Entry	2026-01-12 07:00:00	OK
Exit	2026-01-12 12:00:00	OK
Entry	2026-01-12 12:35:00	OK
Exit	2026-01-12 15:30:00	OK
```

**Result:**
- Work session 1: 07:00 - 12:00 = 5.00h
- Break: 12:00 - 12:35 = 0.58h (35 min) ✓
- Work session 2: 12:35 - 15:30 = 2.92h
- **Total work time: 7.92h**
- **Break: 0.58h** (greater than 0.5h, no penalty)
- **Final time: 7.92h**

## 🔧 Technical Details

- Pure HTML, CSS, and JavaScript
- No external dependencies
- Local data processing (nothing is sent to a server)
- Real-time updates every second

## 📄 License

MIT License
