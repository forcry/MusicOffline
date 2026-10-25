# Offline: a family music player (installable Android app)

Offline is a Progressive Web App. Once installed from Chrome it runs full-screen like a native app,
works with no internet, keeps your music on the device, and shows lock-screen controls.

## Files
- index.html: the whole app (library, playlists, Now Playing, importer, storage)
- sw.js: service worker that caches the app so it opens offline
- manifest.webmanifest + icons/: install info and app icon

## Run it on your computer (to test)
    cd offline
    python3 -m http.server 8080
Open http://localhost:8080 in Chrome.

## Install on your Android phone
A PWA must be served over HTTPS, so put the folder on any free static host
(GitHub Pages, Netlify Drop, Cloudflare Pages), then:
1. Open the HTTPS address in Chrome on the phone (internet needed this one time).
2. Menu (three dots) > Install app (or Add to Home screen).
3. Launch "Offline" from the home screen. Airplane mode works from here on.

## Add your music
1. Put MP3s you own or are licensed to use in Google Drive (or on the phone).
2. In the app tap + (or "Import music"). Android's file picker lists Google Drive; pick files
   (select many at once). Offline copies each one into app storage.
   Drive files are downloaded when you pick them, so use Wi-Fi for the import.
3. Songs appear under Library and Downloads. After import you can delete the Drive copy if you like.

Supported: MP3, M4A/AAC, OGG/Opus, WAV, FLAC (whatever Chrome on your phone can decode).
Album art, title, artist and album are read from ID3 tags; otherwise the file name
("Artist - Title.mp3") is used.

## Family setup
Playlists tab has Road Trip, Kids and Relaxing ready, plus Favorites (heart a song).
Use the ... menu on any song to add it to a playlist, play next, or delete it.
Each family phone keeps its own library; repeat the import on each device.

## Notes and limits
- Background play and lock-screen controls use the browser Media Session API. Keep the app installed
  (not just a browser tab) for the most reliable background playback.
- Storage is the browser's IndexedDB; Android may evict it only when the phone is nearly full.
  The app asks for persistent storage, and the Downloads tab shows usage.
- Clearing Chrome's site data for this app deletes the saved music.
- Only import music you have the right to use. The app does not download from or connect to any streaming service.

## Going further (native APK)
Wrap the folder with Capacitor (npm i @capacitor/core @capacitor/cli @capacitor/android,
npx cap init, npx cap add android, npx cap sync, open in Android Studio) if you want a Play-Store style build.
