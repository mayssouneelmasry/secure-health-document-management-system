# Secure Health Document Management System

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.0+-red.svg)
![MySQL](https://img.shields.io/badge/MySQL-5.7+-orange.svg)
![AES-256](https://img.shields.io/badge/Encryption-AES--256-green.svg)
![2FA](https://img.shields.io/badge/2FA-TOTP-purple.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📋 Overview

A comprehensive healthcare document management system with military-grade security features. This full-stack web application allows patients to manage their health records, doctors to create diagnoses and prescriptions, and admins to oversee the entire system – all while ensuring data confidentiality, integrity, and availability through advanced cryptographic protections.

---

## 🎯 Problem Statement

Healthcare data is highly sensitive and frequently targeted by cybercriminals. Traditional systems often lack:

- End-to-end encryption for medical documents
- Proper integrity verification mechanisms
- Multi-factor authentication
- Granular role-based access control
- Comprehensive audit logging

This project addresses these gaps by implementing a **zero-trust security architecture** for healthcare data management.

---

## ✨ Features

### 👤 Patient Features

- Secure Registration/Login - Password hashing + optional 2FA
- Document Management - Upload, download, and manage encrypted health documents
- Doctor Visit Tracking - Log and track medical appointments
- Prescription Management - View all prescribed medications
- Diagnosis History - Access complete medical history
- To-Do List - Manage health-related tasks
- Mood Tracking - Monitor mental wellness over time
- Wellness Chart - Visualize mood trends

### 👨‍⚕️ Doctor Features

- Patient Overview - View all assigned patients
- Create Diagnoses - Add diagnoses linked to patient visits
- Issue Prescriptions - Create and manage prescriptions
- Monitor Mood Data - Track patient wellness trends
- View Visit History - Access complete patient visit records

### 👑 Admin Features

- User Management - Add, edit, delete users and assign roles
- Document Oversight - View and manage all system documents
- Audit Logs - Complete activity logging with export capabilities
- System Monitoring - Track all system actions
- Configuration - Manage system security settings

---

## 🔒 Security Features

- Password Security - PBKDF2-SHA256 hashing
- Document Encryption - AES-256 in EAX mode
- File Integrity - SHA-256 hashing + HMAC
- Digital Signatures - RSA-PSS with 2048-bit keys
- Two-Factor Authentication - TOTP (RFC 6238)
- Session Management - 15-minute timeout
- OAuth Integration - GitHub + Auth0
- Audit Logging - Complete action tracing
- Secure Key Management - Environment variables + Fernet encryption

---

## 🏗️ Project Structure

- **secure-health-document-management-system/**
  - `main.py` - Main Flask application
  - `application` - Application configuration
  - `.env` - Environment variables

  - **templates/**
    - `login.html` - User login page
    - `signup.html` - Registration page
    - `dashboard.html` - Patient dashboard
    - `doctor_dashboard.html` - Doctor dashboard
    - `upload.html` - Document upload
    - `documents.html` - Document list
    - `profile.html` - User profile
    - `doctor_visits.html` - Visit management
    - `diagnoses.html` - Diagnosis management
    - `prescriptions.html` - Prescription management
    - `todo.html` - To-do list
    - `mood.html` - Mood tracking
    - `setup_2fa.html` - 2FA setup
    - `verify_2fa.html` - 2FA verification
    - `disable_2fa.html` - 2FA removal

    - **admin/**
      - `users.html` - User management
      - `edit_user.html` - Edit user
      - `add_user.html` - Add user
      - `audit_logs.html` - Audit log viewer

    - **errors/**
      - `403.html` - Forbidden
      - `404.html` - Not found
      - `500.html` - Server error

  - **static/** - CSS stylesheets and images
  - **Uploads/** - Encrypted document storage
  - **instance/** - Instance-specific files

---

## 🗄️ Database Schema

| Table | Description |
|-------|-------------|
| `user` | User accounts with roles, public/private keys, 2FA secrets |
| `document` | Encrypted document metadata, hashes, HMACs, signatures |
| `audit_log` | Complete system audit trail |
| `doctor_visit` | Patient appointment records |
| `diagnosis` | Medical diagnoses linked to visits |
| `prescription` | Medication prescriptions |
| `todo_item` | Patient to-do list items |
| `mood_entry` | Daily mood tracking entries |

---

## 🔧 How It Works

### 1. Document Security Flow

- User Upload → File Encryption (AES-256-EAX) → Digital Signature (RSA-PSS)
- Hash Generation (SHA-256) → HMAC Generation → Secure Storage
- Integrity Verification on Download → Decryption & Delivery

### 2. Authentication Flow

- User Login → Password Verification (PBKDF2-SHA256)
- 2FA Challenge (if enabled) → TOTP Verification
- JWT Token Generation → Session Creation (15-min timeout)
- Role-Based Access Control

---

## 🚀 Installation

### Requirements

- Python 3.8+
- MySQL 5.7+
- XAMPP/WAMP/LAMP
- Modern Browser (Chrome/Firefox/Edge)

### Environment Variables

Create a `.env` file with:

```env
# Flask Configuration
SECRET_KEY=your-secret-key-here
ENCRYPTION_KEY=your-32-byte-encryption-key
HMAC_KEY=your-32-byte-hmac-key
JWT_SECRET=your-jwt-secret-key

# Database Configuration
MYSQL_USER=root
MYSQL_PASSWORD=your-password
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_DB=info_db_project

# OAuth Configuration (Optional)
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-secret
AUTH0_CLIENT_ID=your-auth0-client-id
AUTH0_CLIENT_SECRET=your-auth0-secret
AUTH0_DOMAIN=your-domain.us.auth0.com

# Admin Configuration
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=AdminSecure123!

# Server Configuration
FLASK_DEBUG=False
USE_SSL_DEV=False
```
---

### Installation Steps

1. Clone the repository
```
git clone https://github.com/yourusername/secure-health-document-management-system.git
cd secure-health-document-management-system
```

3. Create virtual environment
```
python -m venv venv
source venv/bin/activate # On Windows: venv\Scripts\activate
```

5. Install dependencies
```
pip install flask flask-sqlalchemy flask-login werkzeug authlib python-dotenv pyotp qrcode pycryptodome cryptography email-validator matplotlib PyJWT pymysql
```

7. Configure database
```
- Start XAMPP/WAMP and enable MySQL
- Create database: `info_db_project`
- Run application (tables auto-create)
```

5. Generate encryption key
```
python -c "import base64, os; print(base64.urlsafe_b64encode(os.urandom(32)).decode())"
```

7. Run the application
```
python main.py
```

9. Access the application
```
- Open browser to: `http://localhost:5000`
```

---

## 💻 Usage

### First Time Setup

1. Register a new account (role: user or doctor)
2. Log in with your credentials
3. Set up Two-Factor Authentication (recommended)
4. Start uploading documents or managing health records

### Default Admin Account

After first run, a default admin is created:
- **Email:** `admin@example.com`
- **Password:** `AdminSecure123!`

**⚠️ CHANGE THIS PASSWORD IMMEDIATELY AFTER FIRST LOGIN**

---

## 🔐 Security Best Practices

- Use strong passwords (12+ chars, mixed case, numbers, symbols)
- Enable 2FA (TOTP-based authentication)
- Regular backups (export audit logs and database)
- SSL/TLS in production (configure HTTPS)
- Rotate encryption keys (periodically update ENCRYPTION_KEY)
- Monitor audit logs (review suspicious activities)

---

## 📊 Audit Logging

All system actions are logged with:
- Timestamp
- User ID and email
- Action performed
- Detailed metadata

### Export Options
- CSV format for spreadsheet analysis
- LOG format for security monitoring

---

## 👥 Team Members

| Name | ID |
|------|-----|
| Mayssoune Hussein Elmasry | 2205251 |
| Maryam Waheed Zamel | 2205154 |
| Amina Ahmed Ferra | 2205225 |
| Karen Alfred | 2205236 |

---

## 📚 Technologies Used

| Technology | Purpose |
|------------|---------|
| Flask | Web framework |
| SQLAlchemy | ORM for database operations |
| MySQL | Relational database |
| AES-256-EAX | Document encryption |
| RSA-2048 | Digital signatures |
| PBKDF2-SHA256 | Password hashing |
| TOTP | Two-factor authentication |
| JWT | Session tokens |
| OAuth 2.0 | Social login (GitHub/Auth0) |
| Bootstrap 5 | Frontend styling |
| Chart.js | Wellness visualization |

---

## 🔧 Future Improvements

- [ ] Implement end-to-end encrypted messaging between patients and doctors
- [ ] Add blockchain-based audit trail for tamper-proof logging
- [ ] Integrate with FHIR standards for healthcare interoperability
- [ ] Add biometric authentication (fingerprint/face ID)
- [ ] Implement automated backup and disaster recovery
- [ ] Add patient data export (GDPR compliance)
- [ ] Create mobile application (React Native)
- [ ] Add AI-powered anomaly detection for access patterns

---

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

- Special thanks to course instructors for security best practices guidance
- PyCryptodome and Cryptography libraries for encryption implementations
- Auth0 and GitHub for OAuth integration

---

## ⚠️ Disclaimer

This system is designed for educational purposes. For production deployment, additional security hardening, penetration testing, and compliance with healthcare regulations (HIPAA, GDPR) are required.

---

⭐ If you find this project useful, please consider giving it a star on GitHub!
