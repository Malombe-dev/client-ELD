# ELD Log Generator - Frontend

A modern React-based Electronic Logging Device (ELD) application for truck drivers to track Hours of Service (HOS) compliance.

## 🚀 Features

- **Trip Planning**: Enter origin, pickup, and destination locations
- **Route Calculation**: Automatic route planning with HOS-compliant stops
- **Interactive Map**: Visual route display with OpenStreetMap and OSRM routing
- **Real-Time Logging**: Live status tracking (Off Duty, Sleeper Berth, Driving, On Duty)
- **ELD Log Generation**: Automatic generation of compliant daily log sheets
- **24-Hour Grid**: Visual representation of driver activities
- **HOS Compliance**: Automatic validation against 11-hour driving limit

## 📋 Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Backend API running (see backend README)

## 🛠️ Installation

1. **Clone the repository**
```bash
git clone https://github.com/Malombe-dev/client-ELD
cd frontend
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**

Create a `.env` file in the root directory:
```env
REACT_APP_API_BASE_URL=http://localhost:8000
```

For production:
```env
REACT_APP_API_BASE_URL=https://your-backend-api.com
```

4. **Start the development server**
```bash
npm start
```

The app will open at `http://localhost:3000`

## 📦 Dependencies

### Core Dependencies
```json
{
  "react": "^18.2.0",
  "react-dom": "^18.2.0",
  "lucide-react": "^0.263.1"
}
```

### External Services
- **Leaflet** (v1.9.4) - Map rendering (loaded via CDN)
- **OpenStreetMap** - Map tiles
- **Nominatim** - Geocoding service
- **OSRM** - Road routing

## 🏗️ Project Structure

```
frontend/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── App.js                    # Main application component
│   ├── components/
│   │   ├── MapView.js           # Interactive map component
│   │   ├── TripInputForm.js     # Trip details form
│   │   ├── RouteDisplay.js      # Route visualization
│   │   ├── RealTimeLogging.js   # Live logging interface
│   │   ├── ELDLogGrid.js        # 24-hour grid component
│   │   └── GeneratedLogs.js     # Log sheet display
│   ├── utils/
│   │   └── storageManager.js    # Local storage utilities
│   ├── index.js
│   └── index.css
├── .env
├── .gitignore
├── package.json
└── README.md
```

## 🎨 Key Components

### 1. Trip Input Form
Collects driver and trip information:
- Driver details (name, carrier info)
- Vehicle/trailer numbers
- Trip locations (current, pickup, dropoff)
- Current cycle hours used
- Trip start time

### 2. MapView Component
- Displays interactive map with route
- Shows markers for all stops (start, pickup, fuel, rest, dropoff)
- Uses OSRM for road-accurate routing
- Geocodes addresses using Nominatim

### 3. Real-Time Logging
- Four status buttons (Off Duty, Sleeper, Driving, On Duty)
- Live duration tracking
- Status history log
- Current trip information display
- HOS compliance indicator

### 4. ELD Log Grid
- Visual 24-hour grid
- Four status rows
- Automatic segment rendering
- Compliant with FMCSA requirements

### 5. Generated Logs
- Printable daily log sheets
- Complete trip information
- Driver signature section
- Remarks and shipping documents

## 🔧 Configuration

### API Endpoints Used

The frontend connects to these backend endpoints:

```javascript
POST /api/calculate-route/
GET  /api/driver-logs/
POST /api/save-log/
POST /api/download-logs-pdf/
```

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `REACT_APP_API_BASE_URL` | Backend API URL | `http://localhost:8000` |

## 🧪 Testing

### Manual Testing Checklist

1. **Trip Planning**
   - [ ] Enter all location fields
   - [ ] Click "Calculate Route"
   - [ ] Verify map displays route
   - [ ] Check fuel stops appear (every ~1000 miles)
   - [ ] Verify rest stops (every ~8 hours)

2. **Live Logging**
   - [ ] Change status multiple times
   - [ ] Verify totals update in real-time
   - [ ] Check status history populates
   - [ ] Confirm HOS compliance indicator works

3. **Log Generation**
   - [ ] Click "Finalize Today's Log"
   - [ ] Verify grid draws correctly
   - [ ] Check all trip details appear
   - [ ] Test print functionality
   - [ ] Try PDF download

### Common Issues

**Map not loading**
- Check console for Leaflet errors
- Verify internet connection (uses CDN)
- Clear browser cache

**Route not calculating**
- Ensure backend is running
- Check API_BASE_URL in .env
- Verify CORS settings on backend

**Grid not drawing**
- Check segments have start/end times
- Verify segment status values (0-3)
- Open browser console for errors

## 🚀 Deployment

### Build for Production

```bash
npm run build
```

This creates an optimized build in the `build/` directory.

### Deploy to Vercel

1. **Install Vercel CLI**
```bash
npm install -g vercel
```

2. **Deploy**
```bash
vercel --prod
```

3. **Configure Environment Variables** in Vercel Dashboard
```
REACT_APP_API_BASE_URL=https://your-backend-api.com
```

### Deploy to Netlify

1. **Install Netlify CLI**
```bash
npm install -g netlify-cli
```

2. **Build and Deploy**
```bash
npm run build
netlify deploy --prod --dir=build
```

3. **Set Environment Variables** in Netlify Dashboard

## 📱 Browser Support

- Chrome (recommended) - v90+
- Firefox - v88+
- Safari - v14+
- Edge - v90+

## 🔒 Security Notes

- No authentication implemented (add before production)
- API calls use CORS (configure backend appropriately)
- Uses localStorage for data persistence
- External APIs (OpenStreetMap, OSRM) are rate-limited

## 🎯 HOS Compliance Rules

The app enforces these regulations:
- **11-hour driving limit** per day
- **14-hour on-duty limit** per day
- **70-hour limit** over 8 days
- **Mandatory breaks** every 8 hours of driving
- **Fuel stops** every 1,000 miles

## 🐛 Known Issues

1. **Rate Limiting**: Nominatim geocoding has rate limits (1 request/second)
2. **Offline Mode**: Requires internet for map and routing
3. **Time Zones**: Uses browser's local timezone
4. **Storage Limits**: localStorage has ~5-10MB limit

## 📚 Additional Resources

- [FMCSA ELD Regulations](https://www.fmcsa.dot.gov/hours-service/elds)
- [Leaflet Documentation](https://leafletjs.com/reference.html)
- [OSRM API](http://project-osrm.org/docs/v5.24.0/api/)
- [React Documentation](https://react.dev/)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License.

## 👥 Support

For issues or questions:
- Open an issue on GitHub
- Contact: [your-email@example.com]

## 🎥 Demo

Watch the [Loom demo video](your-loom-link-here) for a complete walkthrough.

---

**Built with ❤️ for truck drivers to stay HOS compliant**