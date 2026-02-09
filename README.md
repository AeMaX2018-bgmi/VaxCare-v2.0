# VaxCare Backend

A secure, HIPAA-compliant backend API for the VaxCare vaccine management system.

## 🚀 Features

- **Secure Authentication**: JWT-based auth with refresh tokens
- **Data Protection**: Row-level security, encryption, audit logging
- **HIPAA Compliance**: Designed for healthcare data requirements
- **Comprehensive API**: Complete vaccine management functionality
- **Docker Ready**: Easy deployment with Docker Compose
- **Production Ready**: Security headers, rate limiting, validation

## 🏗️ Architecture

- **Backend**: Node.js + Express.js
- **Database**: PostgreSQL with Row-Level Security
- **Authentication**: JWT with bcrypt password hashing
- **Security**: Helmet, CORS, rate limiting, input validation
- **Deployment**: Docker containers with health checks

## 📋 Prerequisites

- Node.js 18+ or Docker
- PostgreSQL 15+ (or use Docker Compose)
- npm or yarn

## 🚀 Quick Start

### Option 1: Docker Compose (Recommended)

1. **Clone and setup**:
   ```bash
   git clone <repository>
   cd vaxcare-backend
   cp .env.example .env
   ```

2. **Update environment variables** in `.env`:
   ```env
   DB_PASSWORD=your_secure_password
   JWT_SECRET=your_super_secure_jwt_secret_key_here
   JWT_REFRESH_SECRET=your_super_secure_refresh_secret_key_here
   ```

3. **Start services**:
   ```bash
   docker-compose up -d
   ```

4. **Run migrations**:
   ```bash
   docker-compose exec backend npm run migrate
   ```

5. **Verify setup**:
   ```bash
   curl http://localhost:3000/health
   ```

### Option 2: Local Development

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Setup PostgreSQL database**:
   ```sql
   CREATE DATABASE vaxcare_db;
   CREATE USER vaxcare_user WITH PASSWORD 'your_password';
   GRANT ALL PRIVILEGES ON DATABASE vaxcare_db TO vaxcare_user;
   ```

3. **Configure environment**:
   ```bash
   cp .env.example .env
   # Edit .env with your database credentials
   ```

4. **Run migrations**:
   ```bash
   npm run migrate
   ```

5. **Start development server**:
   ```bash
   npm run dev
   ```

## 📚 API Documentation

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | User login |
| POST | `/api/auth/refresh` | Refresh access token |
| GET | `/api/auth/me` | Get current user info |
| POST | `/api/auth/logout` | User logout |

### Profile Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/profile` | Get user profile |
| POST | `/api/profile` | Create/update profile |
| DELETE | `/api/profile` | Delete profile |

### Children Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/children` | Get all children |
| GET | `/api/children/:id` | Get specific child |
| POST | `/api/children` | Add new child |
| PUT | `/api/children/:id` | Update child info |
| DELETE | `/api/children/:id` | Delete child |

### Vaccine Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/vaccines/schedule` | Get standard vaccine schedule |
| GET | `/api/vaccines/records` | Get user's vaccine records |
| GET | `/api/vaccines/dashboard` | Get vaccination dashboard |
| POST | `/api/vaccines/record` | Record new vaccine |
| PUT | `/api/vaccines/record/:id` | Update vaccine record |
| DELETE | `/api/vaccines/record/:id` | Delete vaccine record |

### Vaccine Drives

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/drives` | Get all vaccine drives |
| GET | `/api/drives/:id` | Get specific drive |
| GET | `/api/drives/location/:location` | Get drives by location |
| GET | `/api/drives/upcoming/next30days` | Get upcoming drives |
| GET | `/api/drives/search/:query` | Search drives |

## 🔒 Security Features

### Data Protection
- **Encryption**: Passwords hashed with bcrypt (12 rounds)
- **Row-Level Security**: Users can only access their own data
- **Audit Logging**: All sensitive operations logged
- **Input Validation**: Comprehensive validation with Joi
- **SQL Injection Protection**: Parameterized queries

### API Security
- **Rate Limiting**: 100 requests per 15 minutes per IP
- **CORS**: Configurable allowed origins
- **Security Headers**: Helmet.js for security headers
- **JWT Security**: Secure token generation and validation
- **HTTPS Ready**: Production-ready SSL configuration

### HIPAA Compliance Features
- **Data Minimization**: Only collect necessary health data
- **Access Controls**: Role-based access with RLS
- **Audit Trail**: Complete audit logging
- **Data Encryption**: At-rest and in-transit encryption
- **Secure Disposal**: Proper data deletion procedures

## 🗄️ Database Schema

### Core Tables
- `users` - User authentication data
- `user_profiles` - Personal health information
- `children` - Child information
- `standard_vaccines` - Vaccine reference data
- `user_vaccines` - Vaccination records
- `vaccine_drives` - Vaccination campaigns
- `notifications` - User notifications
- `audit_logs` - Security audit trail

### Key Features
- UUID primary keys for security
- Automatic timestamps
- Row-level security policies
- Comprehensive indexing
- Foreign key constraints

## 🔧 Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `NODE_ENV` | Environment mode | `development` |
| `PORT` | Server port | `3000` |
| `DB_HOST` | Database host | `localhost` |
| `DB_PORT` | Database port | `5432` |
| `DB_NAME` | Database name | `vaxcare_db` |
| `DB_USER` | Database user | `vaxcare_user` |
| `DB_PASSWORD` | Database password | Required |
| `JWT_SECRET` | JWT signing secret | Required |
| `JWT_REFRESH_SECRET` | Refresh token secret | Required |
| `JWT_EXPIRE` | Access token expiry | `24h` |
| `JWT_REFRESH_EXPIRE` | Refresh token expiry | `7d` |
| `BCRYPT_ROUNDS` | Password hash rounds | `12` |
| `RATE_LIMIT_WINDOW` | Rate limit window (min) | `15` |
| `RATE_LIMIT_MAX` | Max requests per window | `100` |
| `ALLOWED_ORIGINS` | CORS allowed origins | `http://localhost:3000` |

## 🧪 Testing

```bash
# Run tests
npm test

# Run with coverage
npm run test:coverage

# Run specific test file
npm test -- auth.test.js
```

## 📊 Monitoring

### Health Check
```bash
curl http://localhost:3000/health
```

### Logs
```bash
# View application logs
docker-compose logs -f backend

# View database logs
docker-compose logs -f postgres
```

## 🚀 Deployment

### Production Deployment

1. **Update environment variables** for production
2. **Set up SSL/TLS** certificates
3. **Configure reverse proxy** (nginx/Apache)
4. **Set up monitoring** and logging
5. **Configure backups** for database

### Docker Production

```bash
# Build production image
docker build -t vaxcare-backend:latest .

# Run with production compose
docker-compose -f docker-compose.prod.yml up -d
```

## 🔐 Security Considerations

### For Production
- Use strong, unique passwords and secrets
- Enable SSL/TLS encryption
- Set up proper firewall rules
- Regular security updates
- Monitor audit logs
- Implement backup encryption
- Set up intrusion detection

### HIPAA Compliance Checklist
- [ ] Encrypt data at rest and in transit
- [ ] Implement access controls
- [ ] Set up audit logging
- [ ] Create data backup procedures
- [ ] Establish incident response plan
- [ ] Train staff on HIPAA requirements
- [ ] Sign Business Associate Agreements

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an issue in the repository
- Check the documentation
- Review the API examples

## 🔄 Updates

Keep your installation updated:
```bash
git pull origin main
docker-compose pull
docker-compose up -d
npm run migrate
```