# Estimasi Biaya Pengembangan SiPINTER KPU — *Course Platform as App*

> **Ruang lingkup**: menaikkan **prototipe PWA** SiPINTER (frontend-only, `localStorage`)
> menjadi **platform pembelajaran berbasis aplikasi** setara **Udemy** (LMS marketplace,
> video, web + mobile) dan **Coursiv** (mobile-first, microlearning + AI, model langganan).
> Estimasi mengikuti **Roadmap Kematangan L1→L6** (`ARCHITECTURE.md §10`).
>
> Mata uang: **Rupiah (IDR)**, asumsi rate pasar Indonesia **2026**. Angka bersifat
> *order-of-magnitude* (±25%) untuk perencanaan anggaran (RAB/KAK), bukan penawaran final.
> Kurs acuan: **USD 1 = Rp 16.000**.

---

## 1. Acuan: apa arti "setara Coursiv / Udemy"?

| Kapabilitas | Udemy (marketplace) | Coursiv (AI micro-learning) | Target SiPINTER |
| --- | --- | --- | --- |
| Katalog kursus + learning path | ✅ | ✅ (terkurasi) | ✅ 10 tier, alur 7 tahap |
| Video streaming (HLS, adaptif) | ✅ inti | ✅ pendek | ✅ + materi PDF/SCORM |
| Kuis, ujian, sertifikat | ✅ | ✅ | ✅ + badge QR/TTE |
| Mobile app native (Android/iOS) | ✅ | ✅ (utama) | ✅ + tetap PWA offline |
| AI tutor / asisten | ⏳ baru | ✅ inti | ✅ Claude + RAG |
| Langganan / monetisasi | ✅ beli per-kursus | ✅ subscription | N/A (internal KPU) |
| Analytics & admin | ✅ | ✅ | ✅ heatmap, predictive |
| SSO / manajemen org | ✅ (Udemy Business) | – | ✅ SSO KPU, RBAC per tier |

**Implikasi biaya utama** vs prototipe sekarang: (a) **backend produksi** (Frappe LMS
headless), (b) **infrastruktur video**, (c) **2 aplikasi mobile native**, (d) **AI
berbiaya per-token**, (e) **keamanan/SSO + audit**, (f) **operasional tahunan**.

---

## 2. Tiga opsi pendekatan (build strategy)

| Opsi | Deskripsi | Cocok bila | Dampak biaya |
| --- | --- | --- | --- |
| **A. Open-source first** | Adopsi **Frappe LMS** (sudah jadi acuan core) + kustomisasi; mobile via **PWA + wrapper** (Capacitor) | Anggaran terbatas, tim kecil, *time-to-market* cepat | **Termurah** |
| **B. Hybrid** | Frappe LMS headless + **frontend kustom** (PWA) + **mobile native** (Flutter/React Native) | Butuh UX premium & app store presence | **Menengah** |
| **C. Custom penuh** | Bangun LMS dari nol (microservices), web + 2 native app | Skala nasional, kebutuhan unik, kontrol penuh | **Termahal** |

Rekomendasi default untuk KPU: **Opsi B (Hybrid)** — menghormati keputusan arsitektur
yang sudah ada (Frappe LMS + PWA), sambil menambah app native untuk pengalaman kelas
Coursiv. RAB di bawah memakai Opsi B sebagai basis, dengan kolom MVP/Standard/Enterprise.

---

## 3. Komponen biaya pengembangan (one-time)

### 3.1 Tim & rate (blended, per orang-bulan / *man-month*)

| Peran | Rate / bulan (IDR) | Catatan |
| --- | --- | --- |
| Project Manager / Scrum Master | 25.000.000 | 1 orang, lintas fase |
| Solution Architect / Tech Lead | 35.000.000 | desain sistem, review |
| Backend Engineer (Frappe/Python) | 22.000.000 | LMS headless, API, integrasi |
| Frontend / PWA Engineer | 20.000.000 | frontend kustom (lanjutan dari prototipe) |
| Mobile Engineer (Flutter/RN) | 24.000.000 | Android + iOS dari 1 codebase |
| AI / ML Engineer (RAG, Claude) | 28.000.000 | vector DB, prompt, evaluasi |
| UI/UX Designer | 18.000.000 | design system, riset, prototyping |
| QA Engineer (manual + automation) | 16.000.000 | uji fungsional, regresi, beban |
| DevOps / SRE | 24.000.000 | CI/CD, infra, observability, keamanan |
| Content / Instructional Designer | 15.000.000 | kurasi materi 10 tier, konversi SCORM |

> Rate = *blended cost* (gaji + beban + margin vendor). Untuk swakelola internal KPU,
> kalikan ~0,6–0,7. Untuk vendor/PHL profesional, rate di atas realistis.

### 3.2 Estimasi effort per fase (selaras L1→L6)

| Fase | Level | Lingkup | Durasi | Effort (man-month) |
| --- | --- | --- | --- | --- |
| **F1** | L1 | LMS dasar produksi: Frappe headless, course, learning path, quiz, sertifikat, auth | 3 bln | 14 |
| **F2** | L2 | Sertifikasi: badge, QR validation, TTE, CPD point | 2 bln | 8 |
| **F3** | L3 | Knowledge Management: bank kasus, putusan DKPP/MK, digital library, search | 2 bln | 9 |
| **F4** | L4 | AI Assistant produksi: RAG + vector DB, tutor, summarizer, quiz-gen | 3 bln | 13 |
| **F5** | — | **Mobile app native** (Android + iOS), video streaming (HLS/CDN) | 3 bln | 15 |
| **F6** | L5 | Talent Pool & Succession, analytics lanjutan (heatmap, predictive) | 2 bln | 9 |
| **F7** | L6 | Integrasi ekosistem: SSO KPU, RBAC per tier, hardening, audit keamanan | 2 bln | 10 |
| | | **Total** (paralel sebagian → ~12–14 bln kalender) | **~12–14 bln** | **~78 mm** |

### 3.3 Biaya jasa pengembangan per skenario

| Komponen | MVP (L1–L2 + mobile dasar) | Standard (L1–L4 + mobile) | Enterprise (L1–L6 penuh) |
| --- | --- | --- | --- |
| Effort (man-month) | ~30 mm | ~55 mm | ~78 mm |
| **Jasa pengembangan** | **Rp 650 jt** | **Rp 1,25 M** | **Rp 1,8 M** |
| Desain UI/UX (design system) | Rp 60 jt | Rp 90 jt | Rp 120 jt |
| Migrasi & kurasi konten 10 tier | Rp 50 jt | Rp 120 jt | Rp 200 jt |
| Audit keamanan & pentest | Rp 40 jt | Rp 75 jt | Rp 150 jt |
| Manajemen proyek & dokumentasi | (termasuk) | Rp 80 jt | Rp 120 jt |
| Kontingensi (±10%) | Rp 80 jt | Rp 170 jt | Rp 240 jt |
| **Subtotal one-time** | **± Rp 880 jt** | **± Rp 1,78 M** | **± Rp 2,63 M** |

---

## 4. Biaya operasional & infrastruktur (recurring)

Biaya berjalan per bulan, naik seiring jumlah pengguna aktif (MAU). Skala KPU:
**puluhan–ratusan ribu** penyelenggara (PPK/PPS/KPPS + komisioner + sekretariat).

### 4.1 Infrastruktur (cloud)

| Item | Asumsi | Biaya / bulan (IDR) |
| --- | --- | --- |
| Compute (app server Frappe + API) | 2–4 vCPU autoscale | 3.000.000 – 8.000.000 |
| Database terkelola (PostgreSQL/MariaDB) | HA + backup | 2.500.000 – 6.000.000 |
| Vector DB (RAG) — pgvector/Qdrant | embedding knowledge base | 1.500.000 – 4.000.000 |
| **Video: storage + transcoding + CDN** | Mux/Cloudflare Stream/Bunny | 4.000.000 – 20.000.000 |
| Object storage (materi, sertifikat) | S3-compatible | 1.000.000 – 3.000.000 |
| CDN aset + WAF + DDoS | Cloudflare | 1.500.000 – 4.000.000 |
| Monitoring/log (observability) | APM + uptime | 1.000.000 – 2.500.000 |
| **Subtotal infra** | | **± 14,5 jt – 47,5 jt** |

> **Video adalah cost driver terbesar** untuk platform kelas Udemy. Estimasi kasar
> streaming: **~Rp 150–250 per GB delivered**; 1 jam video HD ≈ 1–1,5 GB.
> 10.000 jam-tonton/bulan ≈ **Rp 2–4 jt** hanya untuk *delivery*, di luar transcoding/storage.

### 4.2 Biaya AI (Claude — per token)

AI Assistant memakai **Claude** via Edge Function (kunci di server). Biaya per-pemakaian:

| Skenario pemakaian | Asumsi | Biaya / bulan (IDR) |
| --- | --- | --- |
| Ringan (RAG offline dominan, AI live sesekali) | < 1 jt token/bln | < Rp 500.000 |
| Menengah (tutor aktif, 5–10k sesi tanya-jawab) | ~20–50 jt token/bln | Rp 2 jt – 6 jt |
| Berat (quiz-gen + summarizer + tutor masif) | > 100 jt token/bln | Rp 12 jt+ |

> Gunakan **prompt caching** + **RAG knowledge base lokal** (sudah ada di prototipe) untuk
> menekan biaya: pertanyaan umum dijawab offline, hanya kasus kompleks ke Claude live.
> Pilih model sesuai tugas (Haiku untuk klasifikasi/ringkas, Opus untuk reasoning berat).

### 4.3 Lisensi, store & layanan pihak ketiga

| Item | Frekuensi | Biaya (IDR) |
| --- | --- | --- |
| Apple Developer Program | tahunan | Rp 1.600.000 / thn |
| Google Play Console | sekali | Rp 400.000 (one-time) |
| Sertifikat TTE / e-Meterai (per dokumen) | per terbit | variatif (BSrE/PSrE) |
| Email/notifikasi (SMTP, push FCM) | bulanan | Rp 500.000 – 2.000.000 |
| Domain + TLS | tahunan | Rp 500.000 / thn |
| SSO/IdP (jika berlangganan) | bulanan | opsional |

### 4.4 Pemeliharaan & dukungan (tahunan)

| Item | Asumsi industri | Biaya / tahun (IDR) |
| --- | --- | --- |
| Maintenance & bug-fix | **~15–20%** dari biaya build | Rp 130 jt – 525 jt |
| Tim support L1/L2 (helpdesk) | 1–2 orang | Rp 150 jt – 350 jt |
| Update konten & kurikulum | berkelanjutan | Rp 100 jt – 250 jt |

---

## 5. Ringkasan total biaya

### 5.1 Tahun pertama (build + operasional)

| Skenario | One-time (build) | Operasional/bln (mid) | Operasional 12 bln | **Total Tahun-1** |
| --- | --- | --- | --- | --- |
| **MVP** (L1–L2 + mobile dasar) | Rp 880 jt | ~Rp 20 jt | ~Rp 240 jt | **± Rp 1,12 M** |
| **Standard** (L1–L4 + mobile + AI) | Rp 1,78 M | ~Rp 35 jt | ~Rp 420 jt | **± Rp 2,20 M** |
| **Enterprise** (L1–L6 penuh, skala nasional) | Rp 2,63 M | ~Rp 60 jt | ~Rp 720 jt | **± Rp 3,35 M** |

### 5.2 Tahun ke-2 dan seterusnya (run-rate)

| Skenario | Maintenance + support / thn | Infra + AI / thn | **Total per tahun** |
| --- | --- | --- | --- |
| MVP | ~Rp 200 jt | ~Rp 240 jt | **± Rp 440 jt** |
| Standard | ~Rp 400 jt | ~Rp 420 jt | **± Rp 820 jt** |
| Enterprise | ~Rp 700 jt | ~Rp 720 jt | **± Rp 1,42 M** |

---

## 6. Penghematan spesifik SiPINTER (kenapa lebih murah dari Udemy from-scratch)

1. **Prototipe sudah berjalan** — 10 tier, alur 7 tahap, kuis, knowledge hub, analytics,
   AI offline+live semua sudah fungsional (`ARCHITECTURE.md §11`). Build = *productionizing*,
   bukan dari nol → hemat **30–40%** fase awal.
2. **Frappe LMS open-source** sebagai core → tak ada lisensi LMS, hemat biaya marketplace.
3. **PWA offline-first** mengurangi beban server & cocok untuk daerah koneksi terbatas
   (PPS/KPPS pelosok) — menekan biaya CDN/video saat offline.
4. **Non-komersial / internal** → tak perlu modul pembayaran, marketplace, payout instruktur,
   anti-fraud transaksi (porsi besar biaya Udemy).
5. **RAG lokal** menekan tagihan AI; Claude live hanya untuk kasus kompleks.
6. **Capacitor wrapper** (jika pilih Opsi A) bisa pangkas biaya mobile dari ~Rp 360 jt
   (native) menjadi ~Rp 80–120 jt, dengan trade-off performa.

---

## 7. Rekomendasi & catatan

- **Mulai dari MVP (Opsi A/B)** → rilis L1–L2 + PWA-wrapper dalam ~4–5 bulan, validasi
  adopsi, baru lanjut ke AI & native penuh. *Time-to-value* cepat, risiko anggaran kecil.
- **Video** adalah variabel biaya paling sensitif — pertimbangkan **kompresi agresif,
  durasi pendek ala Coursiv (microlearning)**, dan caching offline untuk menekan CDN.
- **AI**: utamakan RAG offline; ukur token sungguhan di pilot sebelum proyeksi skala.
- **Pengadaan KPU**: petakan ke **SBM/SHBJ** dan format **RAB/KAK/TOR** (lih. `USULAN-HNP.md`).
  Skema **swakelola + PHL** dapat menurunkan rate man-month ~30–40% dibanding vendor penuh.
- Angka di dokumen ini **indikatif untuk perencanaan**; mintalah **2–3 penawaran vendor**
  untuk validasi sebelum penetapan pagu.

---

*Dokumen perencanaan internal — bukan penawaran kontraktual. Verifikasi rate & pajak (PPN/PPh)
sesuai ketentuan pengadaan barang/jasa pemerintah yang berlaku.*
