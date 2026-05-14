# CarCare

A desktop vehicle maintenance tracker built with Python, Tkinter, and MySQL. CarCare allows users to register their vehicle, log service records such as oil changes and tire replacements, monitor vehicle health, and receive maintenance reminders. The application is structured across multiple screens, each implemented as a separate Python module.

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [Running the Application](#running-the-application)
- [Module Reference](#module-reference)
- [Assets](#assets)
- [Author](#author)
- [License](#license)

---

## Features

- Landing page with application overview and entry points for new and existing users
- New user registration collecting name, contact number, and email
- Vehicle data entry and service record logging
- Maintenance reminders based on logged service history
- Vehicle health monitoring for tracking service intervals and potential issues
- Email notification support via a dedicated email module

---

## Project Structure

```
CarCare/
|
|-- main.py               # Entry point; landing page with New User / Existing User navigation
|-- first.py              # Early prototype of the signup screen (development reference)
|-- page2.py              # Vehicle data entry screen
|-- page3.py              # Service record logging screen
|-- page4.py              # Maintenance reminder screen
|-- page5.py              # Vehicle health and history screen
|-- emial.py              # Email notification module
|-- test.py               # Test script
|
|-- Poppins-Regular.ttf   # Bundled Poppins font file
|
|-- icon.png              # Application window icon
|-- login.png             # Signup screen background/illustration
|-- ic1.png               # Feature icon: Service Reminders
|-- ic2.png               # Feature icon: Monitor Health
|-- rsz_5main.png         # Landing page vehicle illustration
|-- rsz_signin.png        # Sign-in screen asset
|-- rsz_1signin.png       # Sign-in screen asset (alternate size)
```

---

## Tech Stack

**Language**

- Python 3.x

**GUI**

- tkinter — base windowing toolkit; used for all windows, labels, entries, and buttons
- tkinter.messagebox — used for dialog boxes and form submission confirmations

**Database**

- MySQL — stores user registrations, vehicle records, and service history
- mysql-connector-python — Python driver for MySQL

**Typography**

- Poppins — used in signup and form screens; bundled as `Poppins-Regular.ttf`
- Cabin — used for the main landing page heading (loaded as a system font)
- Fira Sans — used for landing page body text and feature descriptions (loaded as a system font)

**Email**

- smtplib or equivalent — used in `emial.py` for sending maintenance reminder notifications

---

## Prerequisites

- Python 3.8 or above
- MySQL Server running locally
- pip

---

## Installation

Clone the repository:

```bash
git clone https://github.com/Atharvakumkar/CarCare.git
cd CarCare
```

Install required Python packages:

```bash
pip install mysql-connector-python
```

Tkinter is included with standard Python distributions. If it is not available on your system:

```bash
# Ubuntu/Debian
sudo apt install python3-tk

# macOS (via Homebrew)
brew install python-tk
```

---

## Database Setup

Ensure MySQL is running, then create the required database and tables. Connect to MySQL and run:

```sql
CREATE DATABASE carcare;
USE carcare;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    contact VARCHAR(20),
    email VARCHAR(100)
);

CREATE TABLE vehicles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    vehicle_name VARCHAR(100),
    model VARCHAR(100),
    year INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE service_records (
    id INT AUTO_INCREMENT PRIMARY KEY,
    vehicle_id INT,
    service_type VARCHAR(100),
    service_date DATE,
    next_due_date DATE,
    notes TEXT,
    FOREIGN KEY (vehicle_id) REFERENCES vehicles(id)
);
```

Update the MySQL connection credentials in the relevant page files to match your local MySQL username and password.

---

## Running the Application

```bash
python main.py
```

The application opens to the landing page (1050x600). From there, select "New User" to register or "Existing User" to log in and access the dashboard.

---

## Module Reference

### `main.py`

The application entry point. Builds the main landing window (1050x600) with the "Welcome To 99 Customs!" heading, a vehicle illustration, and two feature cards: "Service Reminders" and "Monitor Health". Provides two buttons at the bottom: "New User" and "Existing User", both routing to the signup/login flow via a `Toplevel` window.

### `first.py`

An early-stage prototype of the signup screen. Contains the base signup form layout (name, contact, email) and a stub for the vehicle data entry screen opened on submit. This file serves as a development reference and is superseded by the signup flow in `main.py`.

### `page2.py`

Vehicle data entry screen. Collects vehicle details from the user (vehicle name, model, year) and writes them to the MySQL `vehicles` table linked to the registered user.

### `page3.py`

Service record logging screen. Allows users to log a service type (e.g. oil change, tire replacement), the date performed, and the next due date. Writes records to the `service_records` table.

### `page4.py`

Maintenance reminder screen. Reads upcoming service due dates from the database and surfaces them to the user so they can stay ahead of scheduled maintenance.

### `page5.py`

Vehicle health and history screen. Displays a full log of past service records for the user's vehicle and highlights any overdue maintenance intervals.

### `emial.py`

Email notification module. Sends maintenance reminder emails to the user's registered email address when service records approach their due date.

### `test.py`

Test script used during development to verify database connections and individual module behaviour.

---

## Assets

All image assets must be in the same directory as the Python files. The application loads them by filename at runtime. If any asset is missing, the relevant window will raise a `FileNotFoundError` or silently fall back depending on how the load is wrapped.

| File | Used in |
|---|---|
| `icon.png` | Window icon (`main.py`) |
| `rsz_5main.png` | Landing page vehicle illustration (`main.py`) |
| `login.png` | Signup screen background illustration |
| `ic1.png` | Service Reminders feature icon (`main.py`) |
| `ic2.png` | Monitor Health feature icon (`main.py`) |
| `rsz_signin.png` | Sign-in screen asset |
| `rsz_1signin.png` | Sign-in screen asset (alternate size) |
| `Poppins-Regular.ttf` | Font used in form screens |

---

## Authors

Atharva Kumkar
Raj Mohite

---

## License

This project is released under the MIT License.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files, to deal in the software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, and to permit persons to whom the software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
