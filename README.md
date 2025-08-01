# Shuttle Monitoring API

A Flask-based REST API for shuttle service monitoring with comprehensive features including user management, trip tracking, and analytics.

## Features

- 🔐 Multi-role authentication (Admin, Manager, Supervisor, Driver)
- 🚐 Vehicle and driver management
- 📊 Trip logging and analytics
- 📈 Performance reporting
- 🏢 Company branding and settings
- 📧 Email notifications and password reset
- 🔄 Real-time monitoring data

## Quick Start

### Local Development

1. **Create virtual environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Set up environment variables:**
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. **Initialize database:**
```bash
python src/seed_data_enhanced.py
```

5. **Run the application:**
```bash
python src/main.py
```

The API will be available at `http://localhost:5000`

## Deployment

### Deploy to Render (Free)

1. **Prepare your repository:**
   - Push your code to GitHub, GitLab, or Bitbucket
   - Make sure `render.yaml` and `requirements.txt` are in your root directory

2. **Deploy on Render:**
   - Go to [render.com](https://render.com)
   - Sign up/login with your Git provider
   - Click "New +" → "Blueprint"
   - Connect your repository
   - Render will automatically detect the `render.yaml` configuration

3. **Set environment variables:**
   - `SECRET_KEY`: A secure random string
   - `FLASK_ENV`: Set to `production`
   - `CORS_ORIGINS`: Your frontend URL (e.g., `https://your-app.vercel.app`)
   - Email settings (optional):
     - `SMTP_SERVER`, `SMTP_USERNAME`, `SMTP_PASSWORD`

4. **Database setup:**
   - Render will automatically create a PostgreSQL database
   - The `DATABASE_URL` will be set automatically

### Alternative: Manual Deployment

If you prefer manual deployment instead of using the Blueprint:

1. **Create a Web Service:**
   - Go to Render dashboard
   - Click "New +" → "Web Service"
   - Connect your repository
   - Configure:
     - **Build Command:** `pip install -r requirements.txt`
     - **Start Command:** `gunicorn --bind 0.0.0.0:$PORT src.main:app`
     - **Environment:** Python 3

2. **Create a PostgreSQL Database:**
   - Click "New +" → "PostgreSQL"
   - Choose the free plan
   - Note the connection details

3. **Set Environment Variables:**
   - In your web service settings, add the environment variables listed above
   - Set `DATABASE_URL` to your PostgreSQL connection string

## Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `SECRET_KEY` | Flask secret key for sessions | Yes | - |
| `FLASK_ENV` | Flask environment | No | `development` |
| `DATABASE_URL` | Database connection string | No | SQLite (local) |
| `CORS_ORIGINS` | Allowed CORS origins (comma-separated) | No | `http://localhost:5173` |
| `SMTP_SERVER` | Email server for notifications | No | - |
| `SMTP_USERNAME` | Email username | No | - |
| `SMTP_PASSWORD` | Email password | No | - |

## API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `POST /api/auth/forgot-password` - Request password reset
- `POST /api/auth/reset-password` - Reset password with token
- `GET /api/auth/me` - Get current user info

### Core Resources
- `/api/drivers` - Driver management
- `/api/vehicles` - Vehicle management
- `/api/routes` - Route management
- `/api/schedules` - Schedule management
- `/api/trip-logs` - Trip logging and management

### Reports & Analytics
- `/api/reports/dashboard-analytics` - Dashboard metrics
- `/api/reports/performance-metrics` - Performance analytics
- `/api/reports/financial-summary` - Financial reports
- `/api/reports/maintenance-schedule` - Maintenance tracking

### Company Settings
- `/api/company/settings` - Company configuration
- `/api/company/branding` - Public branding info
- `/api/company/logo` - Logo upload

### Monitoring
- `/api/monitoring/live-data` - Real-time monitoring data
- `/api/health` - Health check endpoint

## Database Schema

The application uses SQLAlchemy ORM with the following main models:

- **User** - System users with role-based access
- **Driver** - Driver information and status
- **Vehicle** - Vehicle fleet management
- **Route** - Shuttle routes and stops
- **Schedule** - Driver/vehicle assignments
- **TripLog** - Trip records with approval workflow
- **CompanySettings** - Company branding and configuration

## Sample Data

Run the seed script to create sample data:

```bash
python src/seed_data_enhanced.py
```

This creates:
- Admin, Manager, Supervisor, and Driver users
- 5 sample drivers and vehicles
- 4 shuttle routes
- Sample schedules and trip logs
- Company settings for "Metro Shuttle Services"

**Default Login Credentials:**
- Admin: `admin` / `admin123`
- Manager: `manager` / `manager123`
- Supervisor: `supervisor` / `supervisor123`
- Drivers: `driver1-5` / `driver123`

## Technology Stack

- **Framework:** Flask 3.0
- **Database:** SQLAlchemy (SQLite/PostgreSQL)
- **Authentication:** Session-based with role management
- **CORS:** Flask-CORS for cross-origin requests
- **Deployment:** Gunicorn WSGI server
- **Email:** SMTP for notifications

## Development

### Project Structure
```
src/
├── models/              # Database models
│   ├── user.py         # User and authentication
│   ├── driver.py       # Driver management
│   ├── vehicle.py      # Vehicle fleet
│   ├── route.py        # Shuttle routes
│   ├── schedule.py     # Scheduling
│   ├── trip_log.py     # Trip logging
│   └── company_settings.py # Company configuration
├── routes/             # API endpoints
│   ├── auth.py         # Authentication routes
│   ├── driver.py       # Driver management
│   ├── vehicle.py      # Vehicle management
│   ├── schedule.py     # Scheduling
│   ├── trip_log.py     # Trip logging
│   ├── reports.py      # Analytics and reports
│   ├── company.py      # Company settings
│   └── monitoring.py   # Real-time monitoring
├── static/             # Static files (uploads)
└── main.py            # Application entry point
```

### Adding New Features

1. Create model in `src/models/`
2. Create routes in `src/routes/`
3. Register blueprint in `src/main.py`
4. Update database with migrations or recreate

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License.

