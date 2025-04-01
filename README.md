# Hospital-Management-System-HMS-
Hospital Management System is a full-stack web app using Node.js/Express and React/Tailwind CSS. It automates patient registration, appointment booking, payments, and doctor-patient interactions with robust security using JWT, Bcrypt, Google reCAPTCHA, and 6-digit OTP verification for secure, role-based access.
---
# Hospital Management System

A full stack Hospital Management System (HMS) designed to streamline patient registration, appointment booking, doctor–patient interactions, payment processing, and administrative tasks. This project implements robust security measures including Google reCAPTCHA, 6-digit OTP Gmail authentication, JWT-based authentication, and role-based access control (RBAC) to ensure data security and integrity.

## Table of Contents

- [Introduction](#introduction)
- [Abstract](#abstract)
- [Problem Statement](#problem-statement)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [Testing](#testing)
- [Design and Architecture](#design-and-architecture)
- [Risk Analysis](#risk-analysis)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Introduction

This Hospital Management System is developed as a solution for overcoming the challenges faced by traditional hospital queuing and manual data management. The system is divided into two main modules:
- **User Module:** For patients and doctors.
- **Admin Module:** For administrative staff to manage doctor records, patient data, and verify payments.

The application follows an incremental development model where additional requirements can be integrated in future releases.

## Abstract

The HMS project automates the registration, appointment, and payment processes in a hospital. It generates unique IDs for every patient, secures user authentication with OTP and JWT, and allows doctors to manage appointments and add treatment details. Administrators can update doctor details, verify payments, and generate billing receipts. The system is designed with an emphasis on data security, user-friendly interfaces, and robust performance.

## Problem Statement

In many hospitals, manual queuing and appointment management cause long waiting times and inefficient use of resources. The HMS addresses these issues by allowing patients to:
- Register and update their records online.
- Book and cancel appointments from home.
- Receive timely notifications and payment confirmations.

Doctors can manage their appointment lists and update treatment information, while administrators have full control over system data and processes.

## Features

- **User Registration & Login:** Secure registration with form validation and OTP verification via Gmail.
- **Role-Based Access Control (RBAC):** Separate access levels for patients, doctors, and administrators.
- **Appointment Management:** Book, update, or cancel appointments and view appointment status.
- **Payment Processing:** Online payment with bill generation and receipt display.
- **Doctor Module:** Manage patient records, confirm/cancel appointments, and add prescriptions.
- **Admin Dashboard:** Manage doctor entries, verify payments, and view monthly/yearly records.
- **Security Enhancements:**
  - Google reCAPTCHA to prevent bot registrations.
  - JWT tokens for secure session management.
  - Password hashing using Bcrypt with Gensalt.
- **Additional Modules:** Easily extendable to include pharmacy, laboratory, bed allotment, and FAQs.

## Technology Stack

### Frontend
- **React.js** – For building interactive UIs.
- **Tailwind CSS** – For styling and responsive design.
- **Framer Motion** – For smooth animations.
- **React Router Dom** – For client-side routing.
- **Axios** – For HTTP requests.

### Backend
- **Node.js & Express.js** – For building RESTful APIs.
- **MongoDB with Mongoose** – For data storage and management.
- **JWT** – For authentication.
- **Bcrypt** – For secure password hashing.
- **Nodemailer** – For OTP email authentication.
- **ZOD** – For input validation.
- **Cors** – For Cross-Origin Resource Sharing.

### Development Tools
- **Visual Studio Code (VS Code)**
- **Postman** – For API testing.
- **Nodemon** – For development server restarts.
- **Git & GitHub** – For version control.
- **MongoDB Atlas** – For cloud-based database hosting.

## Project Structure

hospital-management-system/ ├── backend/ │ ├── controllers/ │ │ ├── authController.js │ │ ├── patientController.js │ │ ├── doctorController.js │ │ └── adminController.js │ ├── middleware/ │ │ ├── authMiddleware.js │ │ └── rbacMiddleware.js │ ├── models/ │ │ ├── User.js │ │ ├── Appointment.js │ │ ├── Prescription.js │ │ └── Bill.js │ ├── routes/ │ │ ├── authRoutes.js │ │ ├── patientRoutes.js │ │ ├── doctorRoutes.js │ │ └── adminRoutes.js │ ├── app.js │ ├── .env │ └── package.json └── frontend/ ├── public/ ├── src/ │ ├── components/ │ │ ├── Auth/ │ │ │ ├── Login.js │ │ │ ├── Register.js │ │ │ └── VerifyOTP.js │ │ ├── Dashboard.js │ │ └── Appointment.js │ ├── services/ │ │ └── authService.js │ ├── App.js │ ├── index.js │ └── tailwind.css └── package.json
