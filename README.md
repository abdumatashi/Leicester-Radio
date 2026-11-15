# London Radio - Android Studio project

Built from the Hausa Radio app: same design and features, with London stations and a new Podcasts section.

Wraps the web app (app/src/main/assets/www) in a native Android app with:
- AdMob **banner** at the bottom of the home page (hidden while the player page is open)
- AdMob **interstitial** each time the player page opens
- A foreground service so the sound keeps playing when you leave the app
- Splash screen with the radio icon (2.5 seconds, change SPLASH_MS in AppConfig.kt; icon file: app/src/main/res/drawable-nodpi/splash_icon.png)
- Back button: closes player / sub-page / tab first; on the home page it asks "Exit London Radio?"

## Open and run
1. Install Android Studio (current stable) with JDK 17 and Android SDK Platform 36.
2. File > Open > choose this folder. Wait for Gradle sync (needs internet the first time).
3. Run on a phone or emulator (debug builds always use Google TEST ads).

## Before publishing
1. `app/build.gradle.kts`: change `applicationId`, paste your real AdMob ids (liveAppId, liveBanner, liveInterstitial).
2. `AppConfig.kt`: set DEVELOPER_URL, and INTERSTITIAL_COOLDOWN_MS (0 = every time, 60000 = once a minute).
3. Build > Generate Signed Bundle / APK > Android App Bundle (.aab), upload to Google Play Console.
4. Never tap your own live ads. Test only with the debug build.

## Updating stations
Edit `app/src/main/assets/www/stations.json` and the images in `.../www/logos/`, then rebuild.

## Menu items (drawer)
- Rate us / Share / More apps use the native Android actions. The Play Store link is built from your applicationId automatically.
  Set DEVELOPER_URL in AppConfig.kt for "More apps".
- Help & Support and Privacy Policy pages live in app/src/main/assets/www/index.html.
  Edit these constants near the top of that file: SUPPORT_EMAIL, DEVELOPER_NAME, PRIVACY_URL, POLICY_DATE.
- extras/privacy-policy.html: upload it to your GitHub Pages repo (root) so Google Play has a public Privacy Policy link,
  then paste that link into PRIVACY_URL. Replace "Your name" and "your-email@example.com" inside it first.

## Ads
AppConfig.kt: ADS_ENABLED = false turns banner and interstitial off completely.

## Stations and podcasts
- Stations: `app/src/main/assets/www/stations.json` (58 stations). Fields: n = name, s = subtitle, c = tab (top, local, music, world), img = logo (full https address or a file in www/logos/), url = stream.
- Podcasts: `app/src/main/assets/www/podcasts.json` (22 podcasts). Fields: n = name, s = author, c = category, img = cover, feed = RSS feed.
- Podcast episodes are downloaded when a podcast is opened (FeedLoader.kt, newest 100), so they stay up to date without an app update.

## Still to do before publishing London Radio
- Upload extras/privacy-policy.html to a GitHub Pages repo and put that link in PRIVACY_URL (index.html).
- applicationId: com.ansar.londonradio (permanent after the first upload).
