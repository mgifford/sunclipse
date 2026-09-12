Sunset & Sunrise Quality Predictor
==================================

This is a single, self-contained static web page. There is nothing to
build, compile, or install.

TO DEPLOY
---------
Upload index.html to any web server or static host. Open it in a browser.
That's it.

  - Serve it over HTTPS. The precise-GPS button requires a secure origin
    (https:// or http://localhost); it will not work over plain http://.
  - It can live at the site root (yoursite.com/) or in any subfolder
    (yoursite.com/sunset/). No server-side code, database, or config needed.

WHAT IT NEEDS AT RUNTIME (in the visitor's browser, not on your server)
----------------------------------------------------------------------
Three outbound calls the visitor's browser makes:
  1. cdn.jsdelivr.net  - loads the SunCalc library (solar times)
  2. ipapi.co          - approximate location from the visitor's IP
  3. api.open-meteo.com - cloud/weather forecast
All are free and need no API key. Your server just serves the HTML file.

OPTIONAL: remove the CDN dependency
-----------------------------------
To avoid the jsdelivr CDN, download suncalc.js next to index.html and
change the <script src="..."> tag to src="suncalc.js".

Licence follows the repository it came from.
