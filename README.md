
# Smart Attendance System (Node-RED + MySQL)

This project is a **smart attendance system** built using **Node-RED** and **MySQL**. It allows staff to register, scan in/out using UID (e.g. QR code), and logs their working time automatically into a database. The system also includes login authentication and station-based form handling with real-time display.

## 🔧 Features Implemented

### ✅ Staff Registration
- New staff can register via a form (`ui_form`) which includes:
  - Company
  - Name
  - Email
  - IC
  - Staff ID
  - Car & Motorcycle license (checkbox)
  - Phone number
  - **Password field is masked**
- UID must be scanned before form submission.
- Data is stored into the `database` table in MySQL.

### 📥 Scan-In Workflow
- Staff scans their UID (e.g. QR).
- Timestamp, date, and time are recorded (`ts_in`, `date_in`, `time_in`).
- A station selection form is triggered.
- Upon submission, matching staff info is pulled from the `database`, and a new scan-in record is inserted into the `attendance` table.

### 📤 Scan-Out Workflow
- Staff scans their UID to clock out.
- The system searches the latest matching `scan-in` record by UID and date.
- Records the `ts_out`, `date_out`, and `time_out`.
- Calculates total work time (in `h m` format).
- Saves a complete attendance record into the `attendance` table.

### 🔐 Login Authentication
- Login form accepts Staff ID and Password.
- Matches credentials against MySQL records.
- On successful login, redirects user to appropriate dashboard tab (admin or user).

### 🖥️ Real-Time Display
- Shows Name, Staff ID, Station, Time In, Time Out on a UI dashboard.
- Automatically resets the display and form after 3 seconds using a `delay` node and `link` logic.

### 🧹 Data Cleanup
- Context variables and form states are reset after each flow to avoid conflicts or repeated entries.

## 📂 Technologies Used

- **Node-RED** for flow-based visual programming
- **MySQL** as backend storage
- **Node-RED Dashboard** for front-end UI
- **Context Storage (flow.set/get)** for session and UID management

## 🗃️ Database Tables

### `database`
Stores staff registration data:
- `index_no`, `comp`, `name`, `email`, `ic`, `staff_id`, `license_d`, `license_b2`, `phone`, `uid`, `password`

### `attendance`
Logs each in/out scan:
- `index_no`, `comp`, `name`, `staff_id`, `station`, `uid`, `date_in`, `time_in`, `ts_in`, `date_out`, `time_out`, `ts_out`, `total_worktime`

## 📌 Future Improvements (Suggested)
- Auto-skill up logic based on attendance trends
- Admin dashboard for reporting and management
- Role-based access and permission levels
