# SkyEvents
**See the sky before it happens.**  
A Python CLI that fetches upcoming meteor showers, eclipses, and ISS glyovers for your location, with native Windows toast notifications and optional .ics export for your phone's calendar.

## Features (Current)
* Real data sources  
   * Metoer showers & eclispse via In-The-Sky iCal  
   * ISS visible passes via N2YO API (free key)  
* Timezone-aware output(local times)  
* WIndows notrifications (winotify) with --notify  
* Calendar exprt to .ics with --export-ics path  
* Config file support (config.toml) for defaults
* Clean CLI, modular code (ready for weather gate, Starlink, email/SMS, config file, scheduler helper)

## Install  
```powershell
git clone https://github.com/<your-username>/SkyEvents.git
cd SkyEvents

python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**requirements.txt**
```powershell
pip install -r requirements.txt
```  

Create a .env file in the project root folder (this file is ignored by git) a safe template exists called .env.example:
```env
N2YO_API_KEY=YOUR_REAL_KEY_HERE
```

## N2YO API Key
1. Create free account: https://www.n2yo.com/api/
2. Copy your API key
3. Put it in .env as shown above  

# Usage (config.toml) - Open config file and edit vaules according to you prefrences. 
[location]  
lat = 29.6516  
lon = -82.3248  
alt = 50  

[defaults]  
days = 30  
notify = false  
export_ics = ""  
min_elev = 10  

Now you can run with no location flags  
```powershell
python sky_events.py
```
CLI flags always override config:  
```powershell
python sky_events.py --days 10 --notify
pythin sky_events.py --days 60 --export-ics sky_events.ics
```

# Usage (Just CLI Flags)
~~~powershell
# Example (Gainesville, Florida)
python sky_events.py --lat 29.6516 --lon -82.3248 --alt 50 --days 30
~~~
Enable **Windows Notifications**  
~~~powershell
python sky_events.py --lat 29.6516 --lon -82.3248 --alt 50 --days 10 --notify
~~~
Export to .ics for your calendar  
~~~powershell
python sky_events.py --lat 29.6516 --lon -82.3248 --alt 50 --days 10 --export-ics
~~~  

## Windows Notifications (winotify)  
This project uses winotify for native Windows toasts.  
* The script shows up to 2 upcoming events when --notify is used
* We call the WIndows notifications API directly--no flaky threading

## Quick self-test (optional)  
Create and run thif once to confirm your system can toast
~~~python
# notify_test.py
from winotify import Notification
Notification(app_id="SkyEvents", title="SkyEvents Test",
             msg="If you see this, notifications work.", duration="short").show()
print("Sent test toast.")
~~~
~~~powershell
python notify_test.py
~~~
## If you do not see popups  
* Windows Setting -> System -> Notifications On
* **Do Not Distrub/Focus Assist OFF**
* Try running from a regular powershell window (outside vscode)
* You should still see ```[notify] ...``` lines in the terminal when ```--notify``` is active.

## CLI Options (cheat sheet)
* ```--lat```, ```--lon```, ```--alt``` - your location (decimal degrees, meters)
* ```--days N``` - how far ahead to look (default 14)
* ```--notify``` - show Windows toasts for the next 1-2 events
* ```--export-ics PATH``` - write all upcoming events to a single ```ics```
## Data Sources
* **Astronomy events (.ics)** in-The-Sky yearly icalendar feed
* **ISS visible passes: ** N2YO ```visualpasses``` endpoint (ISS NORAD 25544)
* Times converted to your local timezone

# Project Status
## Built  
* iCal meteors/eclipse  
* N2YO ISS passes  
* Windows toasts (```---notify```)  
* Calendar export (```---export-ics```)  
* Config + .env support
## Next  
* Report mode (```--report```,```--save-report```) - "newsletter-style" printable output  
* Heads-up window (```--soon HOURS```)  
* Task Scheduler helper (```--install-task```)  
* Starlink (opt-in)
* Email/SMS delivery (later)

# Contributing  
Ideas and PRs  welcome-especailly for UX polish, weather integrations, and clean config.  
Branch -> PR -> Discuss

# License  
MIT




    






