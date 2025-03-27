# **AuthoIPTV – A Smart and Seamless IPTV Player.**

<p align="center">
  <img style="height: 300px;" src="https://github.com/glitport/AuthoIPTV/blob/main/screenshots/authoiptv-logo.png?raw=true" alt="AuthoIPTV Icon" title="Smart and Seamless IPTV player application" />
</p>

<p align="center">
  <a href="https://github.com/glitport/AuthoIPTV/releases"><img src="https://img.shields.io/github/release/glitport/AuthoIPTV.svg?style=flat-square" alt="Release"></a> 
  <a href="https://github.com/glitport/AuthoIPTV/releases"><img src="https://img.shields.io/github/downloads/glitport/AuthoIPTV/total.svg?style=flat-square" alt="Download"></a>
</p>

**AuthoIPTV** is a feature-rich **Electron-powered** IPTV player designed for desktop users. It offers a seamless streaming experience with **M3U playlist support, automatic updates, EPG (Electronic Program Guide) integration, and custom authorization headers** for protected streams. Whether you're watching live TV, movies, or shows, AuthoIPTV delivers a smooth and intuitive experience.

## **Key Features:**

- ✅ **M3U Playlist Support** – Load, manage, and stream IPTV playlists with ease.  
- ✅ **Auto-Update Playlists** – Automatically refresh and update M3U playlists.  
- ✅ **EPG Integration** – View electronic program guide (EPG) from playlist sources.
- ✅ **Custom Headers Support** – Authenticate with custom headers for secure streams  
- ✅ **Full-Screen HLS Playback** – Enjoy smooth, immersive streaming.  
- ✅ **Channel Navigation** – Easily browse and switch between channels inside the player.  
- ✅ **Playlist Management** – Add, edit, and organize multiple playlists.
- ✅ **Electron-Based** – Runs as a standalone desktop app for Windows, macOS, and Linux.  
- ✅ **Keyboard Shortcuts for Quick Navigation** – Navigate easily using keyboard controls.  
- ✅ **Material UI Design** – Sleek, user-friendly interface with light and dark mode support.
- ✅ **JSON Playlist Support** – Load and manage playlists in JSON format.  
- ✅ **Custom User-Agent for playlist fetching** – Specify custom User-Agent to fetch a playlist.
- ✅ **Single Stream Playback** – Play a single stream link with custom headers, and ClearKey DRM.
- ✅ **DASH & DRM support** – DASH & DRM (Clear Key) streams are now supported.
- ✅ **Playlist & Channel Search** – to quickly find playlists & channels
- ✅ **Audio Selection for multi-audio streams** – Select your desired audio track.

## 📥 Download  
🔗 **Latest Release:** [Download AuthoIPTV](https://github.com/glitport/AuthoIPTV/releases/latest)  

## Join Our Community

📢 [Telegram Channel](https://t.me/AuthoIPTV) – Get the latest updates and discussions

### ⚠️ Disclaimer  
AuthoIPTV is a **player only**. It does **not provide any content**. You must add your own M3U playlist to watch videos or channels.  

---

# IPTV Provider Guide: Creating Playlists & Streams  

## Table of Contents  

- [IPTV Provider Guide: Creating Playlists \& Streams](#iptv-provider-guide-creating-playlists--streams)
  - [Table of Contents](#table-of-contents)
  - [Playlist Format](#playlist-format)
    - [1. Basic Playlist](#1-basic-playlist)
    - [2. Playlist with Kodi Properties and DRM License](#2-playlist-with-kodi-properties-and-drm-license)
    - [3. Playlist with VLC Header](#3-playlist-with-vlc-header)
    - [4. Playlist with EXHTTP Header (e.g., Cookie)](#4-playlist-with-exhttp-header-eg-cookie)
  - [Stream Links](#stream-links)
    - [Piped Inline Headers \& DRM](#piped-inline-headers--drm)
    - [Custom Headers](#custom-headers)
  - [Playing a Single Stream](#playing-a-single-stream)
      - [Example: Single Stream with Headers](#example-single-stream-with-headers)
      - [Example: Single Stream with Cookie](#example-single-stream-with-cookie)
    - [**Single Stream with DRM License URL**](#single-stream-with-drm-license-url)
      - [**Example: ClearKey DRM Stream**](#example-clearkey-drm-stream)
      - [**ClearKey License Request \& Response Format**](#clearkey-license-request--response-format)
        - [**Request Example (JSON Format)**](#request-example-json-format)
        - [**Response Example (JSON Format)**](#response-example-json-format)
      - [**Explanation:**](#explanation)
      - [**Important Notes:**](#important-notes)
    - [**Providing DRM License with KeyID:Key String**](#providing-drm-license-with-keyidkey-string)
      - [**Example: Single Stream with DRM License**](#example-single-stream-with-drm-license)
  - [Codec Support](#codec-support)
  - [VOD (Video On Demand) Content Support](#vod-video-on-demand-content-support)
    - [Example: Unsupported VOD Stream](#example-unsupported-vod-stream)

---

## Playlist Format  

- **Use M3U8 Format:** Providers must use the `.m3u8` format for playlists.  
- **Supported Attributes:** Basic M3U attributes, VLC options, Kodi properties, and inline URL headers are supported.  
- **User-Agent Requirement:** Some providers require a specific user agent for access. Our player uses:  

  ```  
  AuthoIPTV (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) autho-iptv/0.5.4-beta.1 Electron/34.4.0
  ```
  Providers must allow this user agent. Additionally, some Chromium-based headers will be sent, and providers should not block them.

### 1. Basic Playlist

```m3u
#EXTM3U
#EXTINF:-1 tvg-id="channel1" tvg-name="Channel One" group-title="News", Channel One
http://provider.com/stream1.m3u8
#EXTINF:-1 tvg-id="channel2" tvg-name="Channel Two" group-title="News", Channel Two
http://provider.com/stream2.m3u8
#EXTINF:-1 tvg-id="channel3" tvg-name="Channel Three" group-title="Sports", Channel Three
http://provider.com/stream3.m3u8
```

### 2. Playlist with Kodi Properties and DRM License

```m3u
#EXTM3U
#EXTINF:-1 tvg-id="movie1" tvg-name="Premium Movie" group-title="Movies", Premium Movie
#KODIPROP:inputstream.adaptive.license_type=clearkey
#KODIPROP:inputstream.adaptive.license_key=https://license-server.com/getlicense
https://drm-provider.com/stream.mpd
```  

### 3. Playlist with VLC Header  

```m3u  
#EXTM3U  
#EXTINF:-1 tvg-id="music1" tvg-name="Music Channel" group-title="Music", Music Channel  
#EXTVLCOPT:http-user-agent=IPTVPlayer/v0.4.2  
http://music-provider.com/stream.m3u8  
```  

### 4. Playlist with EXHTTP Header (e.g., Cookie)  

```m3u  
#EXTM3U  
#EXTINF:-1 tvg-id="premium1" tvg-name="Premium TV" group-title="Premium", Premium TV  
#EXTHTTP:cookie=SESSIONID=abcd1234  
https://premium-provider.com/secure.m3u8  
```  

## Stream Links  

Providers can embed **inline headers**, **DRM schemes**, and **license URLs** within the stream URL.  

### Piped Inline Headers & DRM 

```m3u  
#EXTINF:-1 tvg-id="movie1" tvg-name="Premium Movie" group-title="Movies", Premium Movie  
https://drm-provider.com/stream.mpd|User-Agent=IPTVPlayer/v0.4.2&drmScheme=clearkey&drmLicense=https://license-server.com/getlicense
```  
In this case:
* The user agent is set inline.
* The stream uses Clearkey DRM.
* A license URL is included.

### Custom Headers

```m3u  
#EXTINF:-1 tvg-id="sport1" tvg-name="Sports HD" group-title="Sports", Sports HD  
https://secure-provider.com/stream.m3u8|Custom-Header-1=CustomValue1&Custom-Header-2=CustomValue2
```  
Here, 2 custom headers (`Custom-Header-1` and `Custom-Header-2`) are added.

## Playing a Single Stream  

The player also supports playing a **single stream** using the **Play Stream** dialog.  

- Users can **manually enter a stream URL** and provide optional headers such as:  
  - `User-Agent`  
  - `Cookie`  
  - `Origin`  
  - `Referer`  
  - `DRM License URL / KeyID:Key string`  
- Inline headers and inline DRM configurations are also supported.  

#### Example: Single Stream with Headers  

```
https://provider.com/live.m3u8|User-Agent=IPTVPlayer/v0.4.2&Referer=https://provider.com
```

#### Example: Single Stream with Cookie  

```
https://secure-stream.com/protected.m3u8|Cookie=SESSIONID=abcd1234
```

### **Single Stream with DRM License URL**  

For **ClearKey DRM**, the stream URL should include the **DRM scheme** and **license URL**.  

#### **Example: ClearKey DRM Stream**  

```
https://drm-provider.com/stream.mpd|drmScheme=clearkey&drmLicense=https://license-server.com/getlicense
```

#### **ClearKey License Request & Response Format**  

When the player requests the **ClearKey license**, the license server should return a JSON response with **KeyID:Key** pairs in Base64 format.

##### **Request Example (JSON Format)**  

The player sends a request with the **KeyID** in Base64 format:  

```json
{
  "kids": ["dGhpcy1pcy1hLWtleWlk"]
}
```

##### **Response Example (JSON Format)**  

The license server must return the decryption **KeyID:Key** pair in Base64 format:  

```json
{
  "keys": [
    {
      "kty": "oct",
      "kid": "dGhpcy1pcy1hLWtleWlk",
      "k": "c2FtcGxlLWtleS1zdHJpbmc="
    }
  ],
  "type": "temporary"
}
```

#### **Explanation:**  
- **`kids`** → The KeyID(s) requested by the player.  
- **`keys`** → The returned decryption keys.  
  - `kid`: The KeyID in Base64 format.  
  - `k`: The actual decryption key in Base64 format.  
- **`type`** → Usually `"temporary"` for short-lived session keys.  

#### **Important Notes:**  
- The **KeyID and Key must be Base64-encoded**.  
- Ensure the license server responds with **valid JSON format**.  
- This method applies to **ClearKey DRM** and is **not for Widevine or PlayReady**. 

### **Providing DRM License with KeyID:Key String**  

For DRM-protected streams, the **KeyID:Key** pair must be provided in **Base64** format (or HEX if required by the provider).  

#### **Example: Single Stream with DRM License**  

```
https://drm-provider.com/stream.mpd|drmScheme=clearkey&drmLicense=dGhpcy1pcy1hLWtleWlk:c2FtcGxlLWtleS1zdHJpbmc
```


## Codec Support  

- Some **audio codecs** like **Dolby, AC3, and DTS** are **not supported** due to our Chromium-based playback engine.  
- Providers should ensure their streams use **AAC, MP3, or other widely supported audio codecs** for compatibility.  

## VOD (Video On Demand) Content Support  

- **Not all VOD content is supported** because Chromium does not support all formats.  
- **Unsupported Formats in Chromium-based HLS/HTML5 Players:**  
  - **MPEG-TS with certain codecs** (e.g., MPEG-2 Video, AC3 Audio).  
  - **Certain fragmented MP4 (fMP4) implementations**.  
  - **Older proprietary formats** like RealMedia (`.rm`), QuickTime (`.mov` with some codecs).  
  - **HEVC (H.265) in certain browser environments** (depends on platform support).  

### Example: Unsupported VOD Stream  

```m3u  
#EXTM3U  
#EXTINF:-1 tvg-id="vod1" tvg-name="Classic Movie" group-title="VOD", Classic Movie  
https://vod-provider.com/unsupported-video.ts  
```  

- This `.ts` file may not play if it contains **MPEG-2 Video** and **AC3 Audio**, which are not supported in most Chromium-based players.  
- Providers should use **H.264 (AVC) in MP4 containers with AAC audio** for maximum compatibility.  

---

Following these guidelines will help ensure smooth playback in our IPTV player app.
# IPTV Provider Guide: Creating Playlists & Streams  

## Table of Contents  

- [IPTV Provider Guide: Creating Playlists \& Streams](#iptv-provider-guide-creating-playlists--streams)
  - [Table of Contents](#table-of-contents)
  - [Playlist Format](#playlist-format)
    - [1. Basic Playlist](#1-basic-playlist)
    - [2. Playlist with Kodi Properties and DRM License](#2-playlist-with-kodi-properties-and-drm-license)
    - [3. Playlist with VLC Header](#3-playlist-with-vlc-header)
    - [4. Playlist with EXHTTP Header (e.g., Cookie)](#4-playlist-with-exhttp-header-eg-cookie)
  - [Stream Links](#stream-links)
    - [Piped Inline Headers \& DRM](#piped-inline-headers--drm)
    - [Custom Headers](#custom-headers)
  - [Playing a Single Stream](#playing-a-single-stream)
      - [Example: Single Stream with Headers](#example-single-stream-with-headers)
      - [Example: Single Stream with Cookie](#example-single-stream-with-cookie)
    - [**Single Stream with DRM License URL**](#single-stream-with-drm-license-url)
      - [**Example: ClearKey DRM Stream**](#example-clearkey-drm-stream)
      - [**ClearKey License Request \& Response Format**](#clearkey-license-request--response-format)
        - [**Request Example (JSON Format)**](#request-example-json-format)
        - [**Response Example (JSON Format)**](#response-example-json-format)
      - [**Explanation:**](#explanation)
      - [**Important Notes:**](#important-notes)
    - [**Providing DRM License with KeyID:Key String**](#providing-drm-license-with-keyidkey-string)
      - [**Example: Single Stream with DRM License**](#example-single-stream-with-drm-license)
  - [Codec Support](#codec-support)
  - [VOD (Video On Demand) Content Support](#vod-video-on-demand-content-support)
    - [Example: Unsupported VOD Stream](#example-unsupported-vod-stream)

---

## Playlist Format  

- **Use M3U8 Format:** Providers must use the `.m3u8` format for playlists.  
- **Supported Attributes:** Basic M3U attributes, VLC options, Kodi properties, and inline URL headers are supported.  
- **User-Agent Requirement:** Some providers require a specific user agent for access. Our player uses:  

  ```  
  AuthoIPTV (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) autho-iptv/0.5.4-beta.1 Electron/34.4.0
  ```
  Providers must allow this user agent. Additionally, some Chromium-based headers will be sent, and providers should not block them.

### 1. Basic Playlist

```m3u
#EXTM3U
#EXTINF:-1 tvg-id="channel1" tvg-name="Channel One" group-title="News", Channel One
http://provider.com/stream1.m3u8
#EXTINF:-1 tvg-id="channel2" tvg-name="Channel Two" group-title="News", Channel Two
http://provider.com/stream2.m3u8
#EXTINF:-1 tvg-id="channel3" tvg-name="Channel Three" group-title="Sports", Channel Three
http://provider.com/stream3.m3u8
```

### 2. Playlist with Kodi Properties and DRM License

```m3u
#EXTM3U
#EXTINF:-1 tvg-id="movie1" tvg-name="Premium Movie" group-title="Movies", Premium Movie
#KODIPROP:inputstream.adaptive.license_type=clearkey
#KODIPROP:inputstream.adaptive.license_key=https://license-server.com/getlicense
https://drm-provider.com/stream.mpd
```  

### 3. Playlist with VLC Header  

```m3u  
#EXTM3U  
#EXTINF:-1 tvg-id="music1" tvg-name="Music Channel" group-title="Music", Music Channel  
#EXTVLCOPT:http-user-agent=IPTVPlayer/v0.4.2  
http://music-provider.com/stream.m3u8  
```  

### 4. Playlist with EXHTTP Header (e.g., Cookie)  

```m3u  
#EXTM3U  
#EXTINF:-1 tvg-id="premium1" tvg-name="Premium TV" group-title="Premium", Premium TV  
#EXTHTTP:cookie=SESSIONID=abcd1234  
https://premium-provider.com/secure.m3u8  
```  

## Stream Links  

Providers can embed **inline headers**, **DRM schemes**, and **license URLs** within the stream URL.  

### Piped Inline Headers & DRM 

```m3u  
#EXTINF:-1 tvg-id="movie1" tvg-name="Premium Movie" group-title="Movies", Premium Movie  
https://drm-provider.com/stream.mpd|User-Agent=IPTVPlayer/v0.4.2&drmScheme=clearkey&drmLicense=https://license-server.com/getlicense
```  
In this case:
* The user agent is set inline.
* The stream uses Clearkey DRM.
* A license URL is included.

### Custom Headers

```m3u  
#EXTINF:-1 tvg-id="sport1" tvg-name="Sports HD" group-title="Sports", Sports HD  
https://secure-provider.com/stream.m3u8|Custom-Header-1=CustomValue1&Custom-Header-2=CustomValue2
```  
Here, 2 custom headers (`Custom-Header-1` and `Custom-Header-2`) are added.

## Playing a Single Stream  

The player also supports playing a **single stream** using the **Play Stream** dialog.  

- Users can **manually enter a stream URL** and provide optional headers such as:  
  - `User-Agent`  
  - `Cookie`  
  - `Origin`  
  - `Referer`  
  - `DRM License URL / KeyID:Key string`  
- Inline headers and inline DRM configurations are also supported.  

#### Example: Single Stream with Headers  

```
https://provider.com/live.m3u8|User-Agent=IPTVPlayer/v0.4.2&Referer=https://provider.com
```

#### Example: Single Stream with Cookie  

```
https://secure-stream.com/protected.m3u8|Cookie=SESSIONID=abcd1234
```

### **Single Stream with DRM License URL**  

For **ClearKey DRM**, the stream URL should include the **DRM scheme** and **license URL**.  

#### **Example: ClearKey DRM Stream**  

```
https://drm-provider.com/stream.mpd|drmScheme=clearkey&drmLicense=https://license-server.com/getlicense
```

#### **ClearKey License Request & Response Format**  

When the player requests the **ClearKey license**, the license server should return a JSON response with **KeyID:Key** pairs in Base64 format.

##### **Request Example (JSON Format)**  

The player sends a request with the **KeyID** in Base64 format:  

```json
{
  "kids": ["dGhpcy1pcy1hLWtleWlk"]
}
```

##### **Response Example (JSON Format)**  

The license server must return the decryption **KeyID:Key** pair in Base64 format:  

```json
{
  "keys": [
    {
      "kty": "oct",
      "kid": "dGhpcy1pcy1hLWtleWlk",
      "k": "c2FtcGxlLWtleS1zdHJpbmc="
    }
  ],
  "type": "temporary"
}
```

#### **Explanation:**  
- **`kids`** → The KeyID(s) requested by the player.  
- **`keys`** → The returned decryption keys.  
  - `kid`: The KeyID in Base64 format.  
  - `k`: The actual decryption key in Base64 format.  
- **`type`** → Usually `"temporary"` for short-lived session keys.  

#### **Important Notes:**  
- The **KeyID and Key must be Base64-encoded**.  
- Ensure the license server responds with **valid JSON format**.  
- This method applies to **ClearKey DRM** and is **not for Widevine or PlayReady**. 

### **Providing DRM License with KeyID:Key String**  

For DRM-protected streams, the **KeyID:Key** pair must be provided in **Base64** format (or HEX if required by the provider).  

#### **Example: Single Stream with DRM License**  

```
https://drm-provider.com/stream.mpd|drmScheme=clearkey&drmLicense=dGhpcy1pcy1hLWtleWlk:c2FtcGxlLWtleS1zdHJpbmc
```


## Codec Support  

- Some **audio codecs** like **Dolby, AC3, and DTS** are **not supported** due to our Chromium-based playback engine.  
- Providers should ensure their streams use **AAC, MP3, or other widely supported audio codecs** for compatibility.  

## VOD (Video On Demand) Content Support  

- **Not all VOD content is supported** because Chromium does not support all formats.  
- **Unsupported Formats in Chromium-based HLS/HTML5 Players:**  
  - **MPEG-TS with certain codecs** (e.g., MPEG-2 Video, AC3 Audio).  
  - **Certain fragmented MP4 (fMP4) implementations**.  
  - **Older proprietary formats** like RealMedia (`.rm`), QuickTime (`.mov` with some codecs).  
  - **HEVC (H.265) in certain browser environments** (depends on platform support).  

### Example: Unsupported VOD Stream  

```m3u  
#EXTM3U  
#EXTINF:-1 tvg-id="vod1" tvg-name="Classic Movie" group-title="VOD", Classic Movie  
https://vod-provider.com/unsupported-video.ts  
```  

- This `.ts` file may not play if it contains **MPEG-2 Video** and **AC3 Audio**, which are not supported in most Chromium-based players.  
- Providers should use **H.264 (AVC) in MP4 containers with AAC audio** for maximum compatibility.  

---

Following these guidelines will help ensure smooth playback in our IPTV player app.
