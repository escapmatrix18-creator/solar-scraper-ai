# 🌞 Solar Company Scraper Dashboard

A comprehensive full-stack web application for scraping, managing, and analyzing solar company data from search engines. Combines powerful web scraping capabilities with a modern web interface to provide actionable insights for solar industry professionals and researchers.

## 📋 Overview

The Solar Company Scraper Dashboard is a production-ready application that automates the discovery and collection of solar company information from Bing search results. Using Scrapy with Playwright for dynamic content handling, it extracts comprehensive contact information including emails, phone numbers, addresses, and LinkedIn profiles. The scraped data is stored in PostgreSQL and presented through a FastAPI backend with a responsive React dashboard.

## ✨ Features

### 🔍 Advanced Web Scraping
- **Intelligent Search**: Automated Bing search for solar companies with customizable queries
- **Dynamic Content Handling**: Playwright integration for JavaScript-heavy websites
- **Contact Extraction**: Comprehensive data collection (emails, phones, addresses, LinkedIn)
- **Smart Classification**: Automatic HR vs main contact email categorization
- **Error Resilience**: Robust handling of 403 errors, captchas, and rate limits

### 📊 Analytics & Insights
- **Real-time Dashboard**: Live statistics and data visualization
- **Search & Filter**: Advanced filtering across all company data fields
- **Export Capabilities**: CSV and JSON export for external analysis
- **Data Management**: Full CRUD operations with pagination
- **Activity Tracking**: Scraping job monitoring and history

### 🔐 User Management
- **Secure Authentication**: JWT-based login and registration system
- **Profile Management**: User account and preference settings
- **Role-based Access**: Admin and user permission levels
- **Session Security**: Secure token management and logout

### 🐳 Production Deployment
- **Docker Containerization**: Complete containerized environment
- **Multi-service Architecture**: PostgreSQL, Redis, Nginx orchestration
- **Health Monitoring**: Built-in health checks and logging
- **Scalable Design**: Horizontal scaling capabilities

## 🛠️ Tech Stack

### Backend
- **FastAPI** - High-performance async web framework
- **SQLAlchemy** - Advanced ORM with PostgreSQL integration
- **Scrapy** - Industrial-strength web scraping framework
- **Playwright** - Browser automation for dynamic content
- **Pydantic** - Data validation and serialization
- **JWT** - Secure authentication tokens

### Frontend
- **React 18** - Modern component-based UI library
- **React Router** - Declarative routing for React
- **Bootstrap 5** - Responsive CSS framework
- **Axios** - Promise-based HTTP client
- **React Toastify** - Elegant notification system

### Infrastructure
- **Docker** - Containerization platform
- **Docker Compose** - Multi-container orchestration
- **PostgreSQL** - Robust relational database
- **Redis** - High-performance caching and sessions
- **Nginx** - Production web server and reverse proxy

## 🚀 Quick Start

### Prerequisites
- Docker and Docker Compose (v3.8+)
- Git
- 4GB+ RAM recommended

### Installation
```bash
# Clone the repository
git clone <repository-url>
cd solar-scraper-dashboard

# Start all services
docker-compose up -d

# Wait for initialization (may take 2-3 minutes)
# Services will be available at:
# - Frontend: http://localhost:3000
# - Backend API: http://localhost:8000
# - API Documentation: http://localhost:8000/docs
```

### Default Credentials
- **Username**: `admin`
- **Password**: `admin123`

> ⚠️ **Important**: Change default credentials immediately after first login!

## 💻 Development Setup

### Backend Setup
```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install Playwright browsers
playwright install chromium

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Run database migrations
alembic upgrade head

# Start development server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### Frontend Setup
```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start development server
npm start
```

## 📖 Usage

### Starting Scraping Jobs
1. **Login** to the dashboard with your credentials
2. **Click "Start Scraping"** button on the dashboard
3. **Configure Parameters**:
   - Search query (e.g., "solar installer companies India")
   - Maximum results (1-100)
4. **Submit** the job and monitor progress

### Managing Company Data
- **Browse Companies**: View all scraped companies with pagination
- **Search & Filter**: Use the search bar to find specific companies
- **View Details**: Click any company card for comprehensive information
- **Export Data**: Download results as CSV or JSON files
- **Delete Records**: Remove unwanted company entries

### User Account Management
- **Register**: Create new user accounts
- **Login/Logout**: Secure authentication system
- **Profile**: Update personal information and preferences

## ⚙️ Configuration

### Environment Variables
Create a `.env` file in the backend directory:

```env
# Database Configuration
DATABASE_URL=postgresql://solar_user:solar_password@localhost:5432/solar_scraper

# JWT Configuration
JWT_SECRET_KEY=your-super-secret-jwt-key-change-in-production
JWT_ALGORITHM=HS256
JWT_EXPIRATION_HOURS=24

# Redis Configuration
REDIS_URL=redis://localhost:6379

# Scrapy Configuration
SCRAPY_SETTINGS_MODULE=scrapy_spiders.settings
PLAYWRIGHT_BROWSERS_PATH=/app/.playwright

# API Configuration
API_HOST=0.0.0.0
API_PORT=8000
```

### Scrapy Settings
Configure scraping behavior in `backend/scrapy_spiders/scrapy_spiders/settings.py`:

```python
# Politeness and Performance
CONCURRENT_REQUESTS = 2
CONCURRENT_REQUESTS_PER_DOMAIN = 1
DOWNLOAD_DELAY = 3
RANDOMIZE_DOWNLOAD_DELAY = True

# User Agents
USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15",
    # Add more user agents...
]

# Proxy Configuration (optional)
# HTTP_PROXY = "http://proxy.example.com:8080"
# HTTPS_PROXY = "http://proxy.example.com:8080"
```

## 🔌 API Endpoints

### Authentication Endpoints
- `POST /auth/login` - User authentication
- `POST /auth/register` - User registration
- `GET /auth/me` - Current user information
- `PUT /auth/me` - Update user profile
- `POST /auth/logout` - User logout

### Dashboard Endpoints
- `GET /dashboard/companies` - List companies with pagination
- `GET /dashboard/companies/{id}` - Company details
- `DELETE /dashboard/companies/{id}` - Delete company
- `GET /dashboard/stats` - Dashboard statistics
- `POST /dashboard/scrape` - Initiate scraping job
- `GET /dashboard/export` - Export company data

## 🔧 Troubleshooting

### Common Issues

**403 Scraping Errors**
```bash
# Enable proxy configuration in settings.py
HTTP_PROXY = "http://your-proxy:port"
# Or add more user agents
# Or increase DOWNLOAD_DELAY
```

**Database Connection Issues**
```bash
# Check PostgreSQL container status
docker-compose logs postgres
# Verify connection string in .env
# Ensure database is healthy
docker-compose exec postgres pg_isready
```

**Playwright Browser Installation**
```bash
# Inside backend container
docker-compose exec backend playwright install chromium
# Or locally in virtual environment
playwright install chromium
```

**Frontend Build Errors**
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
# Check for conflicting dependencies
npm ls --depth=0
```

**Memory Issues**
```bash
# Increase Docker memory allocation
# Or reduce CONCURRENT_REQUESTS in settings
# Monitor with docker stats
```

## ⚡ Performance & Scalability

### Polite Scraping Practices
- **Rate Limiting**: Configurable delays between requests
- **User Agent Rotation**: Multiple user agents to avoid detection
- **Concurrent Request Control**: Limited parallel requests per domain
- **Session Management**: Proper browser session handling

### Caching & Optimization
- **Redis Caching**: Session storage and API response caching
- **Database Indexing**: Optimized queries with proper indexing
- **Pagination**: Efficient handling of large datasets
- **Lazy Loading**: Frontend component loading optimization

### Scalability Features
- **Horizontal Scaling**: Multiple scraper instances possible
- **Database Sharding**: Support for large data volumes
- **Async Processing**: Non-blocking API operations
- **Background Jobs**: Scraping runs asynchronously

## 🔒 Security Considerations

### Authentication Security
- **Strong JWT Secrets**: Use cryptographically secure keys
- **Password Hashing**: bcrypt with salt rounds
- **Token Expiration**: Short-lived tokens with refresh mechanism
- **Rate Limiting**: API endpoint protection

### Data Protection
- **Input Validation**: Comprehensive input sanitization
- **SQL Injection Prevention**: Parameterized queries
- **XSS Protection**: Content Security Policy headers
- **HTTPS Enforcement**: SSL/TLS in production

### Infrastructure Security
- **Container Security**: Minimal base images and regular updates
- **Network Segmentation**: Service isolation with Docker networks
- **Secret Management**: Environment variables for sensitive data
- **Regular Updates**: Keep dependencies and base images current

## 🎯 Advanced Scraping Features

### Intelligent Data Extraction
- **Email Classification**: Automatic HR/main contact detection using keywords
- **Phone Number Parsing**: Regex patterns for Indian and international formats
- **LinkedIn Discovery**: Profile URL extraction and validation
- **Address Extraction**: Geographic location parsing with pin codes

### Smart Navigation
- **Domain Discovery**: Automatic company website identification
- **Contact Page Detection**: Intelligent follow-up to contact/about pages
- **Pagination Handling**: Bing result page navigation
- **Content Analysis**: Context-aware data extraction

### Error Handling & Recovery
- **Retry Mechanisms**: Configurable retry attempts with backoff
- **Captcha Detection**: Automatic blocking detection and logging
- **Fallback Strategies**: Alternative extraction methods
- **Debug Logging**: Comprehensive error tracking and reporting

## 🧪 Testing

### Backend Testing
```bash
# Run pytest suite
cd backend
pytest

# Run with coverage
pytest --cov=app --cov-report=html

# Specific test categories
pytest tests/test_auth.py
pytest tests/test_scraping.py
```

### Test Coverage
- **Email Regex Validation**: Comprehensive email pattern testing
- **Contact Classification**: HR vs main email logic verification
- **Data Extraction**: Phone, address, LinkedIn parsing accuracy
- **Spider Configuration**: Scrapy settings and middleware testing
- **API Integration**: Endpoint functionality and error handling

### Frontend Testing
```bash
# Run React test suite
cd frontend
npm test

# Run with coverage
npm test -- --coverage
```

## 🗺️ Roadmap

### Phase 1 (Current Release)
- ✅ Core scraping functionality
- ✅ User authentication system
- ✅ Basic dashboard interface
- ✅ Docker deployment

### Phase 2 (Next Release)
- [ ] Email verification system
- [ ] Advanced search and filtering
- [ ] Data visualization charts
- [ ] Scheduled scraping jobs
- [ ] API rate limiting

### Phase 3 (Future)
- [ ] CRM system integration
- [ ] Machine learning insights
- [ ] Mobile application
- [ ] Multi-language support
- [ ] API marketplace

### Community Requests
- [ ] Bulk data import/export
- [ ] Custom scraping templates
- [ ] Team collaboration features
- [ ] Advanced analytics dashboard

## 📄 License & Support

### License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### Support
- **Issues**: Report bugs and request features on [GitHub Issues](https://github.com/your-repo/issues)
- **Discussions**: Join community discussions on [GitHub Discussions](https://github.com/your-repo/discussions)
- **Documentation**: Full API docs available at `/docs` endpoint
- **Troubleshooting**: Check the troubleshooting section above

### Contributing
We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Acknowledgments
- Built with ❤️ for the solar energy community
- Special thanks to the open-source communities of FastAPI, Scrapy, and React

---

**Ready to revolutionize your solar company research?** Get started with the Solar Company Scraper Dashboard today! 🌞
