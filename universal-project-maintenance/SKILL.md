\# Universal Project Maintenance



Gunakan skill ini untuk project software apa pun.



\## Prinsip utama



\- Audit project sebelum mengubah file.

\- Pahami framework, package manager, build system, dan deployment target.

\- Jangan mengubah file di luar scope task.

\- Jangan mengarang hasil verification.

\- Setelah perubahan:

&#x20; 1. jalankan type check jika tersedia

&#x20; 2. jalankan lint jika tersedia

&#x20; 3. jalankan test jika tersedia

&#x20; 4. jalankan production build jika tersedia

&#x20; 5. git diff

&#x20; 6. git status --short

\- Jangan deploy/publish tanpa konfirmasi user.

\- Jangan mengubah credential, API key, secret, atau .env tanpa instruksi eksplisit.



\## Workflow



\### Audit

Identifikasi:

\- framework

\- runtime

\- package manager

\- dependencies

\- scripts

\- environment variables

\- external APIs

\- authentication

\- database

\- deployment platform

\- konfigurasi security



\### Planning

Sebelum edit:

\- jelaskan file yang akan diubah

\- jelaskan dependency yang relevan

\- identifikasi compatibility risk

\- tentukan verification command



\### Implementation

\- ubah seminimal mungkin

\- pertahankan API dan behavior existing

\- jangan melakukan refactor yang tidak diminta



\### Verification

Gunakan command yang benar-benar tersedia di project.



Contoh:

\- npm run typecheck

\- npm run lint

\- npm test

\- npm run build

\- cargo check

\- go test ./...

\- dotnet build

\- php artisan test



Jangan menyebut PASS jika command belum benar-benar dijalankan.



\### Git safety

Setelah selesai:

\- git diff

\- git status --short

\- pastikan hanya file dalam scope yang berubah



\### Deployment

Deployment selalu merupakan tahap terpisah.



Jangan:

\- git push

\- firebase deploy

\- vercel deploy

\- npm publish

\- production migration



tanpa konfirmasi user.

