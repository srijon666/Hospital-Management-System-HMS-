# HealthGrid - Advanced Hospital Management System

HealthGrid is a comprehensive, full-stack Hospital Management System designed to streamline hospital operations, ensuring efficient management of patients, doctors, appointments, pharmacy, reports, and messaging. Developed using React.js for the frontend and Express.js with Node.js for the backend, HealthGrid integrates security, authentication, and automation to enhance the healthcare experience.

## Technical Stack

-Frontend: React Native with JavaScript, TailwindCSS
-Backend/Database: MongoDB Atlas
-UI Framework: React Native Paper

### Frontend Development

- **React Native**

  - Cross-platform mobile application development
  - Native performance and user experience
  - Reusable components and efficient state management


### Backend & Database

- **MongoDB Atlas**
  - Real-time database capabilities
  - Authentication and authorization
  - File storage and management
  - RESTful API endpoints
  - PostgreSQL database with row-level security

### UI Framework

- **React Native Paper**
  - Material Design components
  - Customizable and accessible UI elements
  - Consistent design system
  - Dark mode support
  - Responsive layouts

## Key Features

### 1. Secure Authentication & User Management

- Google reCAPTCHA to prevent bot attacks
- Secure login with 6-digit OTP verification via Gmail using Nodemailer
- JWT-based authentication and session management
- Bcrypt password hashing for secure storage
- Student Registration Verification ensures accurate records
- Secure password reset with email verification
- Role-Based Access Control (RBAC) for user permissions

### 2. Advanced Frontend Technologies

- Developed with React.js for dynamic user interactions
- Styled using Tailwind CSS for a responsive UI
- Framer Motion for animations
- UI testing with React Testify

### 3. Robust Backend and Database

- Express.js & Node.js handle API requests and server operations
- MongoDB Atlas for cloud-based database management
- ZOD validation for secure input handling
- Multer for file uploads and document management

## Authentication & User Management Flows

### User Registration

1. **Initial Sign-up**

   - Email verification required
   - Phone number verification (optional)
   - Google reCAPTCHA integration
   - Basic profile information collection

2. **Verification Process**
   - Email verification link sent to registered email
   - 6-digit OTP sent for phone verification
   - Account activation upon successful verification

### Login System

1. **Standard Login**

   - Email/Username and password authentication
   - JWT token generation for session management
   - Remember me functionality
   - Failed attempt tracking and lockout system

2. **OTP-based Login**
   - 6-digit OTP sent to registered email
   - Time-limited OTP validity
   - Secure OTP verification process

### Password Management

1. **Password Reset**

   - "Forgot Password" flow
   - Email verification required
   - Secure password reset link
   - Password strength requirements
   - Password history tracking

2. **Password Update**
   - Current password verification
   - New password confirmation
   - Password policy enforcement
   - Success notification

### Session Management

1. **Login**

   - JWT token generation
   - Session timeout configuration
   - Multiple device support
   - Active session tracking

2. **Logout**
   - Secure session termination
   - Token invalidation
   - Clear local storage
   - Redirect to login page

### Security Features

- Rate limiting for login attempts
- IP-based access control
- Session timeout after inactivity
- Secure cookie management
- Cross-site request forgery (CSRF) protection

## Core Functionalities

### Dashboard

- Functional top navigation bar with search, notifications, and account management
- Quick access to total patients, available beds, appointments, and revenue dashboards
- Dynamic scheduling and real-time appointment updates

### Patient & Doctor Management

- Add, edit, and delete patient/doctor details with full profile dashboards
- Status updates with real-time tracking
- Appointment scheduling, rescheduling, and cancellation

### Medical Records & Pharmacy

- Maintain patient records with department categorization
- Secure file uploads, downloads, and sharing
- Pharmacy stock updates and order management

### Messaging & Reports

- Instant messaging with file attachments
- Secure calling options including video conferencing
- Automated report generation with downloadable PDFs

## Conclusion

HealthGrid is an all-in-one hospital management solution ensuring seamless operations, secure access, and an enhanced user experience for hospitals, doctors, and patients alike.

## Database Schema

### Users Table

```sql
users (
  id: uuid PRIMARY KEY,
  email: string UNIQUE,
  password_hash: string,
  full_name: string,
  role: enum('admin', 'doctor', 'patient', 'staff'),
  phone_number: string,
  created_at: timestamp,
  updated_at: timestamp,
  last_login: timestamp,
  is_verified: boolean,
  verification_token: string,
  reset_token: string,
  profile_picture: string
)
```

### Patients Table

```sql
patients (
  id: uuid PRIMARY KEY,
  user_id: uuid REFERENCES users(id),
  date_of_birth: date,
  gender: enum('male', 'female', 'other'),
  blood_group: string,
  address: string,
  emergency_contact: jsonb,
  medical_history: jsonb,
  insurance_details: jsonb,
  created_at: timestamp,
  updated_at: timestamp
)
```

### Doctors Table

```sql
doctors (
  id: uuid PRIMARY KEY,
  user_id: uuid REFERENCES users(id),
  specialization: string,
  department: string,
  qualification: string[],
  experience: integer,
  consultation_fee: decimal,
  availability: jsonb,
  created_at: timestamp,
  updated_at: timestamp
)
```

### Appointments Table

```sql
appointments (
  id: uuid PRIMARY KEY,
  patient_id: uuid REFERENCES patients(id),
  doctor_id: uuid REFERENCES doctors(id),
  appointment_date: timestamp,
  status: enum('scheduled', 'completed', 'cancelled', 'no_show'),
  type: enum('consultation', 'follow_up', 'emergency'),
  notes: text,
  created_at: timestamp,
  updated_at: timestamp
)
```

### Medical Records Table

```sql
medical_records (
  id: uuid PRIMARY KEY,
  patient_id: uuid REFERENCES patients(id),
  doctor_id: uuid REFERENCES doctors(id),
  diagnosis: text,
  prescription: jsonb,
  lab_reports: jsonb[],
  notes: text,
  created_at: timestamp,
  updated_at: timestamp
)
```

### Pharmacy Table

```sql
pharmacy (
  id: uuid PRIMARY KEY,
  name: string,
  description: text,
  category: string,
  quantity: integer,
  price: decimal,
  manufacturer: string,
  expiry_date: date,
  created_at: timestamp,
  updated_at: timestamp
)
```

### Messages Table

```sql
messages (
  id: uuid PRIMARY KEY,
  sender_id: uuid REFERENCES users(id),
  receiver_id: uuid REFERENCES users(id),
  content: text,
  attachment_url: string,
  is_read: boolean,
  created_at: timestamp,
  updated_at: timestamp
)
```

## Project Structure

```
healthgrid/
├── app/                      # Main application directory
│   ├── assets/              # Static assets (images, fonts, etc.)
│   │   ├── common/         # Shared components
│   │   ├── forms/          # Form components
│   │   └── layouts/        # Layout components
│   ├── screens/            # Screen components
│   │   ├── auth/          # Authentication screens
│   │   ├── dashboard/     # Dashboard screens
│   │   ├── patients/      # Patient management screens
│   │   ├── doctors/       # Doctor management screens
│   │   ├── appointments/  # Appointment screens
│   │   ├── pharmacy/      # Pharmacy screens
│   │   └── messages/      # Messaging screens
│   ├── navigation/        # Navigation configuration
│   ├── services/          # API and service integrations
│   │   ├── api/          # API calls
│   │   ├── auth/         # Authentication services
│   │   └── storage/      # Storage services
│   ├── utils/            # Utility functions
│   ├── hooks/            # Custom React hooks
│   ├── constants/        # App constants
│   ├── types/           # TypeScript type definitions
│   └── config/          # Configuration files
├── docs/                 # Documentation
├── tests/               # Test files
├── .env                 # Environment variables
├── app.json            # Expo configuration
├── package.json        # Dependencies
└── README.md           # Project documentation
```

## Environment Variables

```env
# MongoDB Atlas Configuration
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster‑name>.mongodb.net/<dbname>?retryWrites=true&w=majority
MONGODB_DB_NAME=<dbname>

# Email Configuration
SMTP_HOST=your_smtp_host
SMTP_PORT=your_smtp_port
SMTP_USER=your_smtp_user
SMTP_PASS=your_smtp_pass

# JWT Configuration
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=24h

# Other Configuration
APP_URL=your_app_url
NODE_ENV=development
```