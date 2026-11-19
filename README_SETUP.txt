EQUINOX GYM WEBSITE — SETUP GUIDE
=================================

Included
- index.html: responsive gym management website (Admin / Trainer / Member views)
- manifest.webmanifest + sw.js: installable PWA shell
- firestore.rules: starter database security rules

IMPORTANT
This is a deployable starter website, not a hosted live service yet. You must connect it to a Firebase project that you own. The website will not sync online until the Firebase configuration and user profiles are created.

1) Create Firebase project
- Open https://console.firebase.google.com/ in your browser.
- Create a project named Equinox Gym.
- Add a Web app. Copy the Firebase config object.
- In index.html, find `const firebaseConfig = ...` and replace the placeholder values with your real config.
- Enable Authentication > Sign-in method > Email/Password.
- Create a Firestore Database (Production mode).

2) Apply security rules
- In Firestore Database > Rules, paste the contents of firestore.rules and Publish.
- Review rules with a developer before storing real member data. These are starter rules and should be tested against your exact workflow.

3) Create first admin
- In Firebase Authentication > Users, add an admin email and password.
- Copy that user's UID.
- In Firestore, create collection `users`, document ID = that exact UID.
- Add fields:
    role (string) = admin
    name (string) = Gym Admin
- Sign in on the website.

4) Create trainer and member accounts
- Create each account in Firebase Authentication > Users.
- Create a `users` document whose ID is the new user's UID.
- Trainer profile fields: role="trainer", name="Trainer Name".
- Member profile fields: role="member", name="Member Name".
- For a member account, set the member record's `uid` field to that member's Auth UID and email to their login email.
- For trainer assignment, set member record's `trainerUid` to the trainer's Auth UID and `trainer` to trainer's display name.
- For trainer-created members, assign trainerUid to their UID.

5) Publish free on Firebase Hosting
- Easiest mobile-friendly route: use Firebase Hosting's console / a browser-based deployment workflow, or use Firebase CLI from a computer.
- Firebase CLI commands (computer):
    npm install -g firebase-tools
    firebase login
    firebase init hosting
    # choose the project; set public directory to this folder; configure as single-page app: No
    firebase deploy --only hosting
- Firebase Hosting has a free Spark quota. Free quotas and policies can change; if you exceed them, service may pause or require a paid plan.
- Your free URL will look like https://YOUR_PROJECT_ID.web.app

6) Install on Android
- Open the deployed URL in Chrome.
- Menu (⋮) > Add to Home screen / Install app.

DEMO
- Open index.html in a browser through a local static server or deployed hosting.
- Choose Explore demo to preview with sample records. Demo edits stay only in that browser/device and are not online.

CURRENT MVP FEATURES
- Admin / trainer / member sign-in role routing
- Member records: add, edit, delete (admin delete only)
- Attendance records
- Payment entries (admin)
- Fitness progress entries
- Member CSV export
- Responsive mobile layout and PWA shell

NOT YET INCLUDED
- Automated fee reminders, payment gateway, trainer self-service account creation, detailed 30-day daily workout/nutrition form matching, PDF reports, advanced audit logs and production-grade security review.
