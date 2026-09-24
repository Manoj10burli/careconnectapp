CareConnect — Healthcare Platform Prototype
Connected Healthcare. Simpler Patient Experience.
A clickable DEMO of a patient / doctor / admin healthcare platform, built with
React, TypeScript and Tailwind CSS. All people, records and clinical values are
fictional sample data. This is a prototype for customer presentation, not a
production medical system, and it is not certified or compliant with HIPAA,
GDPR, India's DPDP Act or any other regulation.
Run it
```bash
npm install
npm run dev        # http://localhost:5173
npm run build      # type-checks, then writes dist/index.html (single self-contained file)
```
Android app
The same code ships as a native Android app via Capacitor. See
docs/ANDROID.md. Quickest route to an APK: push to GitHub
and download it from Actions → Android APK.
```bash
npm run build:android   # build + sync into android/
npm run android:open    # open in Android Studio
```
Demo logins
Role	Demo user	Lands on
Patient	Priya Sharma	`/`
Doctor	Dr. Arjun Menon	`/doctor`
Admin	Neha Kulkarni	`/admin`
Use the one-click demo buttons, or type any seeded email with any password.
Click Demo walkthrough (top bar) for the scripted 11-step customer story:
patient books → confirmation → doctor sees it → opens record → adds note and
prescription → patient sees prescription → uploads/selects report → AI summary →
notifications. Admin → Configuration → Reset demo data restores the seed
before each presentation.
Seed data (src/data/seed.ts)
10 patients · 6 doctors · 6 departments · 24 appointments · 11 medical records ·
11 prescriptions · 11 lab reports · 13 notifications · 3 sample AI documents.
Dates are generated relative to today so the demo always looks current.
Project structure
```
src/
  types/               Domain model (backend-agnostic contracts)
  services/
    interfaces.ts      Service contracts: Auth, User, Appointment, MedicalRecord,
                       Document, Notification, AI, Admin
    index.ts           Service registry — the ONLY place implementations are chosen
    mock/              In-browser implementations + localStorage "database"
    http/              Production API client + example HTTP service
  data/                Demo seed data and sample AI documents
  context/             Auth session and toasts
  hooks/               useData (fetch + live refresh), useLookups
  components/          UI primitives, layout shell, shared clinical views
  pages/               auth / patient / doctor / admin / shared screens
  platform/            Native bridge: notifications, back button, haptics, file sharing
android/               Native Android project (Capacitor 8, SDK 36, min Android 7)
docs/ARCHITECTURE.md   Production architecture, security and roadmap
docs/ANDROID.md        Building, installing and releasing the Android app
```
Pages never import mock code — they call `services.*`. Replacing a mock with a
real backend means implementing the same interface and changing one line in
`src/services/index.ts`.
