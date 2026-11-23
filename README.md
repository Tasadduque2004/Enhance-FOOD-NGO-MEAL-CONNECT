# FoodBridge

FoodBridge is a web app (PWA) that connects donors with surplus food to NGOs that need it, so good food reaches people instead of going to waste.

**Live site:** https://foodbridge-1727f.web.app

## Project Overview

The app has three types of users:

- **Donor:** posts surplus food, with a photo.
- **NGO:** gets verified, then accepts donations, schedules pickups and chats with the donor.
- **Admin:** verifies NGOs, oversees the whole system, handles reports and can block users.

### Features

- Post food donations with photo upload
- NGO verification: NGOs are reviewed by an admin before they can accept donations
- NGOs can accept donations
- Schedule and confirm pickup times
- Chat between donor and NGO
- Mark donations as complete and rate the other party
- Report and block system
- Admin dashboard
- Email notifications (on acceptance and pickup scheduling)
- Installable on phones (PWA / Android APK)

### NGO Verification

To keep donations safe and trustworthy, a new NGO account is not active right away:

1. The NGO signs up and submits its details for verification.
2. The admin reviews the request from the Admin Dashboard.
3. Once approved, the NGO can accept donations and schedule pickups.

## Technology Stack

| Part | Technology |
|------|-----------|
| Frontend | HTML, CSS, JavaScript (single file: `index.html`) |
| Database | Firebase Firestore |
| Authentication | Firebase Authentication |
| Hosting | Firebase Hosting |
| Image uploads | Cloudinary |
| Email | EmailJS |
| Installable app | PWA (`manifest.webmanifest`, `sw.js`) |

## Files in This Repository

- `index.html`: the whole app
- `firestore.rules`: database security rules
- `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`: make the app installable on phones
- `firebase.json`: Firebase Hosting and rules deploy settings

## Setup Instructions

### 1. Rules (do this first)

Firebase Console > Firestore Database > Rules > paste `firestore.rules` > Publish.

### 2. Put the site online (Firebase Hosting, free plan is enough)

```
npm install -g firebase-tools
firebase login
firebase init hosting      (choose project foodbridge-1727f, keep public folder ".", do NOT overwrite index.html)
firebase deploy
```

Also add your new site address in Firebase Console > Authentication > Settings > Authorized domains.

### 3. After the first deploy

1. Log in as admin > Admin Dashboard > All donations > "Secure old donations".
2. Cloudinary > Settings > Upload > preset `foodbridge_upload`: allow only jpg/png/webp and set a max file size.
3. Make one real admin: Firebase Console > Firestore > users > your document > role = `admin`.
4. Optional: create a second EmailJS template for pickup schedules and put its ID in `EMAILJS_TEMPLATE_PICKUP` inside `index.html`. Template variables: `donor_email`, `donor_name`, `ngo_name`, `food_name`, `pickup_time`, `pickup_note`.

### 4. Test with three accounts

Donor, NGO, admin: post, accept, schedule, confirm, chat, complete, rate, report, block. Also test NGO verification: sign up as an NGO, approve it as admin, then accept a donation.

## Security Note

The Firebase web API key in `index.html` is a public client key and is restricted to this site's domains in Google Cloud Console. Data access is protected by `firestore.rules`.

## Author

[Tasadduque2004](https://github.com/Tasadduque2004)
