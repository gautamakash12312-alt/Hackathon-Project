# SevaSetu Health (सेवासेतु स्वास्थ्य)
### Rural Healthcare & Multispecialty Hospital Management Platform
*“Healthcare for Every Village. Advanced Care for Every City.”*

SevaSetu Health is a modern full-stack healthcare e-commerce and hospital management platform designed to bridge India’s rural-urban medical divide. It connects village patients with verified local doctors through a Zomato-style discovery interface, provides real-time ICU and ward bed availability tracking for urban multispecialty hospitals, and gives every citizen a permanent Digital Patient ID with QR code verification.

---

## 🌟 Key Platform Modules

### 1. Rural Healthcare (Zomato-Style Doctor Discovery)
- **Visual Doctor Discovery Cards**: Photos, qualification (MBBS, BAMS, MD, MS), specialization, years of experience, clinic name, village/town, distance in km from patient, consultation fees (INR), rating (out of 5.0), patient review count, available days, and visiting hours.
- **Direct Calling**: Single-click `Call Doctor` button directly opens the phone dialer (`tel:+91...`) with the doctor's verified phone number.
- **WhatsApp Contact**: Direct WhatsApp link (`https://wa.me/...`) for instant inquiries.
- **Interactive Route Simulation**: `Get Directions` opens turn-by-turn route maps with travel times by Car, Two-Wheeler, and Rural Feeder Bus.
- **Doctor Filters & Search**: Search by village (e.g. Chhitauni, Tamkuhi Raj, Fazilnagar), district (Kushinagar, Gorakhpur), PIN code, doctor name, specialization, fee ceiling, and "Available Today" toggle.

### 2. Urban Healthcare (Multispecialty Hospital Discovery)
- **Hospital Directory**: NABH accredited institutions with logo, cover photo, ownership type, establishment year, full address, phone, and emergency hotline.
- **Live Bed Availability Tracker**:
  - Total licensed beds
  - Available vs occupied beds
  - General ward vacancy
  - ICU critical care vacancy
  - Private rooms & Deluxe suites
  - Emergency triage beds
  - Special Care / NICU incubators
  - Color-coded availability status (`Normal Availability`, `High Demand`, `Critical / Almost Full`)
  - Last updated timestamp with audit history
- **Specialties & Clinical Departments** (matching design reference):
  - Cardiology, Neurology, Orthopedics, Pediatrics, Gynecology, Oncology, Nephrology, Emergency Medicine with Department Heads, specialist counts, and direct OPD slot booking.
- **24/7 Level-1 Trauma & Emergency Hotlines**: Immediate 108/102 ambulance dialing.

### 3. Patient ID & Digital Health Vault
- **Unique Patient ID**: Formatted as `HC-2026-XXXXXX` (e.g. `HC-2026-000101`).
- **Digital Health Card**: Printable ID card with live generated 2D QR code (using `qrcode` library).
- **Patient Dashboard** (based on modern clinical portal reference):
  - Health vitals: Blood Pressure, Resting Pulse, Fasting Blood Glucose, Height, Weight.
  - Active prescriptions tracker with medicine dosage, frequency, and doctor instructions.
  - Diagnostic pathology reports viewer & downloader (CBC, ECG, X-Ray, MRI, CT Scan, Ultrasound, Discharge Summaries).
  - Appointment history & digital booking receipts.

### 4. Appointment Booking System
- Date picker and 15-minute slot selector.
- Double-booking prevention via backend validation and database constraints.
- Printable appointment receipt with unique Booking ID (e.g. `APT-2026-XXXXX`).

### 5. Transparent Patient Reviews & Behaviour Ratings
- 8-criteria rating system:
  1. Doctor Behaviour & Listening
  2. Staff Courtesy & Helpfulness
  3. Cleanliness & Hygiene
  4. Patient Care & Nursing
  5. Treatment Experience
  6. Waiting Time Management
  7. Clinic / Hospital Infrastructure
  8. Emergency Response
- Verified patient indicator and moderation.

### 6. Four Dedicated Role Dashboards
- **Patient Dashboard** (`/dashboard/patient`)
- **Doctor Dashboard** (`/dashboard/doctor`): Queue manager, Patient ID record lookup, digital prescription writer, schedule manager.
- **Hospital Admin Dashboard** (`/dashboard/hospital`): Live bed inventory manager, patient report uploader, doctor roster.
- **Super Admin Dashboard** (`/dashboard/admin`): National health metrics, verification queues, DPDP Act 2023 compliance audit logs.

---

## ⚡ Fast 1-Click Demo Accounts

To test any role without typing passwords, use the **1-Click Demo Role Switcher** in the top navigation bar, or log in with:

| Role | Email | Password | Access Details |
|---|---|---|---|
| **Patient** | `patient@sevasetu.com` | `patient123` | ID: `HC-2026-000101` (Ramesh Kumar) |
| **Rural Doctor** | `doctor@sevasetu.com` | `doctor123` | Dr. Arvind Mishra (General Medicine) |
| **Hospital Admin**| `hospital@sevasetu.com` | `hospital123` | Apex Lifeline Super Specialty Hospital |
| **Super Admin** | `admin@sevasetu.com` | `admin123` | National Health Board Inspector |

---

## 🛠️ Technology Stack

- **Frontend**: Next.js 14 (App Router), React 18, TypeScript, Tailwind CSS, Lucide Icons, Canvas Confetti.
- **Backend**: Next.js API Route Handlers (REST), JWT authentication with HTTP-only cookies, bcryptjs password hashing.
- **Database & ORM**: SQLite (`prisma/dev.db`) managed through Prisma ORM 5.
- **Digital Health ID**: Dynamic QR Code generation with `qrcode`.
- **Bilingual Interface**: English & Hindi (हिन्दी) switcher.

---

## 🚀 How to Run the Application

1. **Install dependencies** (already installed in workspace):
   ```bash
   npm install
   ```

2. **Generate Database & Seed Data**:
   ```bash
   npx prisma generate
   npx prisma db push
   node prisma/seed.js
   ```

3. **Start Development Server**:
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) in your web browser.

4. **Production Build & Launch**:
   ```bash
   npm run build
   npm start
   ```

---

## 📁 Project Architecture

```
├── prisma/
│   ├── schema.prisma       # Prisma schema (14 models with relations)
│   ├── seed.js             # Rich seed script with doctors, hospitals, beds, reports
│   └── dev.db              # SQLite production-ready local database
├── src/
│   ├── app/
│   │   ├── api/            # 14 REST API route handlers
│   │   │   ├── auth/       # Login, register, logout, me
│   │   │   ├── doctors/    # Discovery, filters, profile
│   │   │   ├── hospitals/  # Discovery, departments, live beds
│   │   │   ├── appointments/# Booking, conflict prevention
│   │   │   ├── medical-reports/ # Diagnostic vault
│   │   │   ├── prescriptions/   # Rx generator
│   │   │   ├── reviews/    # 8-criteria behaviour ratings
│   │   │   └── admin/stats/# Platform telemetry
│   │   ├── rural-healthcare/ # Zomato-style Doctor Discovery page
│   │   ├── urban-healthcare/ # Multispecialty Hospital Discovery page
│   │   ├── doctors/[id]/   # Detailed Doctor Profile & Timetable
│   │   ├── hospitals/[id]/ # Hospital Profile & Live Beds Dashboard
│   │   ├── dashboard/      # Patient, Doctor, Hospital, and Admin portals
│   │   ├── login/          # Authentication page with 1-click switcher
│   │   ├── register/       # Patient ID generator & digital profile
│   │   └── page.tsx        # Modern homepage with dual cards
│   ├── components/
│   │   ├── Navbar.tsx      # Navigation with role switcher & language toggle
│   │   ├── Footer.tsx      # Emergency helpline & compliance
│   │   ├── DoctorCard.tsx  # Zomato-style card with call dialer
│   │   ├── HospitalCard.tsx# Bed status & emergency cards
│   │   ├── BedAvailabilityTracker.tsx # Interactive live bed counter
│   │   ├── BookingModal.tsx# Appointment booking & receipt printer
│   │   ├── DirectionsModal.tsx # Simulated GPS directions
│   │   ├── PatientQrModal.tsx  # Digital Health ID Card with QR
│   │   └── ReviewModal.tsx # 8-factor feedback modal
│   ├── context/
│   │   ├── AuthContext.tsx # User session & 1-click role switcher
│   │   └── LanguageContext.tsx # English & Hindi bilingual dictionary
│   └── lib/
│       ├── prisma.ts       # Prisma Client singleton
│       ├── auth.ts         # JWT token signing & session verification
│       └── utils.ts        # Formatting & ID generators
```
