# lan-multicaster
screen sharing to mutiple device in local network 


Open the app from another device using your computer's LAN IP address, for example:

```text
http://192.168.1.7:3000
```

## Usage

### Start a broadcast

1. Open the app on the broadcaster device.
2. Choose `Broadcast Video`.
3. Select a capture source:
   - `Camera` for camera and microphone
   - `Screen` for screen/system capture when the browser supports it
   - `File` for a local video or audio file
4. Choose quality and buffer settings.
5. Click `Start A/V Broadcast`.
6. Share the QR code or 6-digit room code with receiver devices.

### Join as a receiver

1. Open the app on a second device.
2. Choose `Watch Stream`.
3. Scan the QR code, enter the room code, or pick a discovered broadcaster.
4. Press `Play Stream` when prompted.
5. Use receiver controls for fullscreen, player size, fit/fill, volume, and buffer tuning.

## Browser Notes

Screen sharing depends on browser support for `navigator.mediaDevices.getDisplayMedia()`.

- Desktop Chromium browsers usually support screen sharing.
- Mobile browser support varies by platform and browser.
- iOS Safari may not expose web screen sharing.
- Some mobile browsers hide screen sharing on plain LAN HTTP URLs.
- If screen sharing is unavailable, use `Camera` or `File` mode.

For the best chance of screen sharing on mobile, use a browser that exposes `getDisplayMedia()` and serve the app from a secure context, such as HTTPS or localhost.

## LAN and Network Notes

- Broadcaster and receivers should be on the same Wi-Fi/LAN for best latency.
- The signaling API stores rooms in server memory, so rooms reset when the server restarts.
- Current WebRTC config uses a public STUN server and does not include a TURN relay.
- On strict networks, peer-to-peer connections may fail without a TURN server.

## Scripts

```bash
npm run dev
```

Start the development server on `0.0.0.0`.

```bash
npm run build
```

Create a production build.

```bash
npm run start
```

Run the production server on `0.0.0.0`.

```bash
npm run lint
```

Run ESLint checks.

## Troubleshooting

### Receiver cannot find broadcaster

- Make sure both devices are on the same Wi-Fi/LAN.
- Use the broadcaster LAN URL instead of `localhost` on receiver devices.
- Check that firewall rules allow inbound traffic on port `3000`.

### Screen sharing is not available on mobile

The app now tries screen sharing whenever the browser exposes the API, but some mobile browsers do not support web screen capture. Try another browser/device, HTTPS, or use Camera/File mode.

### No audio from screen share

- Desktop browsers often require selecting `Share audio` in the screen picker.
- Some browsers only support tab audio, not full system audio.
- Mobile browser behavior varies.

### Stream connects but video does not play

- Press `Play Stream` on the receiver to satisfy browser autoplay rules.
- Check browser camera/microphone/screen permissions.
- Try the `Medium` or `Large` buffer preset on busy Wi-Fi.
