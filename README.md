# Prescripto - Healthcare Appointment Booking Platform

A full-stack MERN application for booking doctor appointments with separate interfaces for patients, doctors, and administrators.

## 📋 Overview

Prescripto is a comprehensive healthcare appointment management system that allows patients to browse doctors, book appointments, and manage their healthcare needs online. The platform includes role-based access for three user types: patients, doctors, and administrators.

## ✨ Features

### Patient Features
- 🔐 User registration and authentication
- 👨‍⚕️ Browse doctors by speciality
- 📅 Book appointments with available time slots
- 💳 Multiple payment options (Stripe & Razorpay)
- 📋 View and manage appointments
- 👤 Profile management with image upload
- ❌ Cancel appointments

### Doctor Features
- 🔐 Secure doctor login
- 📊 Personal dashboard with statistics
- 📅 View and manage appointments
- ✅ Mark appointments as completed
- ❌ Cancel appointments
- 👤 Update profile (fees, address, availability)
- 🔄 Toggle availability status

### Admin Features
- 🔐 Admin authentication
- ➕ Add new doctors to the platform
- 📋 View all appointments
- 👨‍⚕️ Manage doctor list
- 📊 Dashboard with platform statistics
- ❌ Cancel appointments
- 🔄 Control doctor availability

## 🛠️ Tech Stack

### Frontend
- **React 18** - UI library
- **Vite** - Build tool
- **React Router DOM** - Routing
- **Axios** - HTTP client
- **TailwindCSS** - Styling
- **React Toastify** - Notifications

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **JWT** - Authentication
- **Bcrypt** - Password hashing
- **Cloudinary** - Image storage
- **Multer** - File upload
- **Stripe & Razorpay** - Payment gateways

## 📁 Project Structure

```
prescripto-full-stack/
├── backend/              # Node.js backend
│   ├── config/          # Configuration files
│   ├── controllers/     # Route controllers
│   ├── middleware/      # Custom middleware
│   ├── models/          # Database models
│   ├── routes/          # API routes
│   └── server.js        # Entry point
├── frontend/            # Patient-facing React app
│   ├── src/
│   │   ├── assets/      # Static assets
│   │   ├── components/  # React components
│   │   ├── context/     # Context providers
│   │   └── pages/       # Page components
│   └── package.json
└── admin/               # Admin & Doctor dashboard
    ├── src/
    │   ├── components/  # React components
    │   ├── context/     # Context providers
    │   └── pages/       # Page components
    └── package.json
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB
- Cloudinary account
- Stripe account (optional)
- Razorpay account (optional)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/prescripto-full-stack.git
cd prescripto-full-stack
```

2. **Backend Setup**
```bash
cd backend
npm install
```

Create a `.env` file in the backend directory:
```env
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
ADMIN_EMAIL=admin@prescripto.com
ADMIN_PASSWORD=your_admin_password
CLOUDINARY_NAME=your_cloudinary_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET_KEY=your_cloudinary_secret_key
STRIPE_SECRET_KEY=your_stripe_secret_key
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
PORT=4000
```

Start the backend server:
```bash
npm start
# or for development with nodemon
npm run server
```

3. **Frontend Setup**
```bash
cd ../frontend
npm install
```

Create a `.env` file in the frontend directory:
```env
VITE_BACKEND_URL=http://localhost:4000
```

Start the frontend:
```bash
npm run dev
```

4. **Admin Panel Setup**
```bash
cd ../admin
npm install
```

Create a `.env` file in the admin directory:
```env
VITE_BACKEND_URL=http://localhost:4000
```

Start the admin panel:
```bash
npm run dev
```

## 🔑 API Endpoints

### User Routes (`/api/user`)
- `POST /register` - Register new user
- `POST /login` - User login
- `GET /get-profile` - Get user profile (protected)
- `POST /update-profile` - Update user profile (protected)
- `POST /book-appointment` - Book appointment (protected)
- `GET /appointments` - Get user appointments (protected)
- `POST /cancel-appointment` - Cancel appointment (protected)
- `POST /payment-stripe` - Stripe payment (protected)
- `POST /payment-razorpay` - Razorpay payment (protected)

### Admin Routes (`/api/admin`)
- `POST /login` - Admin login
- `POST /add-doctor` - Add new doctor (protected)
- `GET /all-doctors` - Get all doctors (protected)
- `GET /appointments` - Get all appointments (protected)
- `POST /cancel-appointment` - Cancel appointment (protected)
- `POST /change-availability` - Toggle doctor availability (protected)
- `GET /dashboard` - Get dashboard data (protected)

### Doctor Routes (`/api/doctor`)
- `POST /login` - Doctor login
- `GET /appointments` - Get doctor appointments (protected)
- `GET /profile` - Get doctor profile (protected)
- `POST /update-profile` - Update doctor profile (protected)
- `POST /cancel-appointment` - Cancel appointment (protected)
- `POST /complete-appointment` - Mark appointment complete (protected)
- `POST /change-availability` - Toggle availability (protected)
- `GET /dashboard` - Get doctor dashboard (protected)
- `GET /list` - Get all doctors (public)

## 🗄️ Database Models

### User Model
- name, email, password (hashed)
- phone, address, gender, dob
- profile image

### Doctor Model
- name, email, password (hashed)
- speciality, degree, experience, about
- fees, address, availability status
- slots_booked (object tracking appointments)
- profile image

### Appointment Model
- userId, docId
- slotDate, slotTime
- userData, docData
- amount, payment status
- cancelled, isCompleted flags

## 🔐 Authentication

The application uses JWT-based authentication with three separate token types:
- **User Token** - For patient authentication
- **Admin Token (aToken)** - For admin authentication
- **Doctor Token (dToken)** - For doctor authentication

Tokens are stored in localStorage and sent via headers for protected routes.

## 💡 Key Features Implementation

### Slot Booking System
- Prevents double-booking with slot availability checking
- Stores booked slots in doctor's `slots_booked` object
- Real-time slot availability updates

### Payment Integration
- Dual payment gateway support (Stripe & Razorpay)
- Payment verification endpoints
- Secure payment processing

### Image Upload
- Cloudinary integration for image storage
- Multer middleware for handling multipart/form-data
- Profile pictures for users and doctors

### Role-Based Access Control
- Separate authentication middleware for each role
- Protected routes based on user type
- Token verification for secure access

## 🌐 Deployment

### Backend Deployment
1. Deploy to platforms like Heroku, Railway, or Render
2. Set environment variables
3. Ensure MongoDB connection is configured

### Frontend & Admin Deployment
1. Build the applications:
```bash
npm run build
```
2. Deploy to Vercel, Netlify, or similar platforms
3. Update `VITE_BACKEND_URL` to production backend URL

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 👥 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

For any queries or support, please contact [your-email@example.com]

---

**Made with ❤️ by [Your Name]**
