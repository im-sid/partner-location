# The Proximity Finder

Real-time location sharing between two users with live distance tracking.

## Features

- 🌍 **Real-time Location Tracking** - Share your location with one other person
- 📍 **Distance Calculation** - See the distance between you and your partner in real-time
- 🔐 **Secure Sessions** - 10-digit session codes with 2-user limit
- 🗺️ **Interactive Map** - Powered by Leaflet and OpenStreetMap
- 💾 **Session Persistence** - Sessions survive page refreshes
- 📱 **PWA Ready** - Install as an app on mobile devices
- 🎨 **Beautiful UI** - Clean design with custom color palette

## Tech Stack

- **Frontend**: HTML5, Tailwind CSS, Vanilla JavaScript
- **Map**: Leaflet.js with OpenStreetMap tiles
- **Backend**: Firebase (Firestore + Anonymous Auth)
- **Geolocation**: Browser Geolocation API + Nominatim reverse geocoding

## Setup

### Prerequisites

- A Firebase project with:
  - Anonymous Authentication enabled
  - Firestore database created
  - Proper security rules configured

### Firebase Security Rules

Add these rules to your Firestore:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /artifacts/{appId}/public/data/locations/{sessionCode} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### Configuration

1. Clone this repository
2. Update Firebase config in `index.html` (lines 175-181) with your Firebase project credentials
3. Deploy to any static hosting service (Netlify, Vercel, GitHub Pages, Firebase Hosting)

### Local Development

1. Open `index.html` in a browser or use a local server:
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js
   npx serve
   
   # Using VS Code Live Server extension
   ```

2. Access at `http://localhost:8000`

**Note**: For mobile testing, you need HTTPS. Use ngrok:
```bash
npx ngrok http 8000
```

## Usage

### Creating a Session

1. Open the app
2. Allow location access when prompted
3. Wait for country detection
4. Click "Create Session"
5. Share the 10-digit code with your partner

### Joining a Session

1. Open the app
2. Enter the 10-digit session code
3. Click "Join"
4. Both users will see each other's location and distance in real-time

### Ending a Session

- **Session Creator**: Click "Stop Session" - This ends the session for both users
- **Session Joiner**: Click "Leave Session" - Creator will see "waiting for partner"

## PWA Installation

### Generating Icons

1. Open `generate-icons.html` in a browser
2. Right-click each canvas and save as PNG to the `icons/` folder
3. Or use an online tool like [PWA Asset Generator](https://www.pwabuilder.com/imageGenerator)

Required icon sizes: 32, 72, 96, 128, 144, 152, 192, 384, 512

### Enable PWA

After generating icons, uncomment these lines in `index.html`:
- Line 16: `<link rel="manifest" href="manifest.json">`
- Lines 19-20: Icon links

## Deployment

### Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Deploy
netlify deploy --prod
```

### Vercel

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel --prod
```

### Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login and init
firebase login
firebase init hosting

# Deploy
firebase deploy --only hosting
```

## Security

- Firebase credentials in the code are **safe** - they're meant to be public
- Security is enforced through Firebase Security Rules
- Restrict your Firebase API key to your domain in Google Cloud Console
- Only authenticated users can access data
- Sessions are limited to 2 users

## Browser Support

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (with HTTPS)

## License

MIT License - Feel free to use and modify

## Contributing

Pull requests are welcome! For major changes, please open an issue first.

## Troubleshooting

### Location not detecting
- Enable location services in Windows/OS settings
- Allow location access in browser
- Check browser console for errors
- Ensure you're on HTTPS (or localhost)

### Session not connecting
- Check Firebase console for errors
- Verify Firestore security rules are published
- Ensure Anonymous Auth is enabled
- Check browser console for Firebase errors

### Map not loading
- Check internet connection
- Verify Leaflet CDN is accessible
- Check browser console for errors

## Credits

- Maps: [OpenStreetMap](https://www.openstreetmap.org/)
- Geocoding: [Nominatim](https://nominatim.openstreetmap.org/)
- Map Library: [Leaflet](https://leafletjs.com/)
- UI Framework: [Tailwind CSS](https://tailwindcss.com/)
