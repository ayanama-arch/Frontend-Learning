# Advanced Media Features

## 1. Media Fragments

Access specific portions of media files using URL parameters.

**Syntax:**

- Time: `#t=[start],[end]`
- Spatial (images): `#xywh=[x],[y],[width],[height]`

**Example:**

```html
<!-- Play video from 10s to 25s -->
<video src="movie.mp4#t=10,25" controls></video>

<!-- Start audio at 30 seconds -->
<audio src="song.mp3#t=30" controls></audio>
```

## 2. Media Capture

Capture audio/video from user's device using `getUserMedia()`.

**Example:**

```html
<video id="preview" autoplay></video>

<script>
  navigator.mediaDevices
    .getUserMedia({ video: true, audio: true })
    .then((stream) => {
      document.getElementById("preview").srcObject = stream;
    });
</script>
```

## 3. Picture-in-Picture

Allow videos to float in a small window while browsing other content.

**Example:**

```html
<video id="myVideo" src="video.mp4" controls></video>
<button onclick="togglePiP()">Toggle PiP</button>

<script>
  async function togglePiP() {
    const video = document.getElementById("myVideo");
    if (document.pictureInPictureElement) {
      await document.exitPictureInPicture();
    } else {
      await video.requestPictureInPicture();
    }
  }
</script>
```

## 4. Media Session API

Control media playback from system UI (notifications, lock screen, media keys).

**Example:**

```html
<audio id="audio" src="song.mp3" controls></audio>

<script>
  navigator.mediaSession.metadata = new MediaMetadata({
    title: "Song Title",
    artist: "Artist Name",
    artwork: [{ src: "cover.jpg", sizes: "512x512" }],
  });

  navigator.mediaSession.setActionHandler("play", () => {
    document.getElementById("audio").play();
  });

  navigator.mediaSession.setActionHandler("pause", () => {
    document.getElementById("audio").pause();
  });
</script>
```

**Key Use Cases:**

- **Fragments**: Link to specific video timestamps or image regions
- **Capture**: Build webcam apps, video chat, voice recorders
- **PiP**: Enable multitasking while watching videos
- **Session API**: Professional media player controls
