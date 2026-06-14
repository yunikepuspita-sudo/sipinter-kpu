# SiPINTER KPU — Election Knowledge & Competency Platform

**SiPINTER KPU** (*Sistem Pembelajaran Integratif, Terstruktur & Berjenjang*; alias
**ELSA — Election Learning & Succession Academy**) adalah platform pembelajaran berjenjang
KPU yang mengintegrasikan **pembelajaran + sertifikasi + knowledge management + succession
planning**. PWA *offline-first* (vanilla JS, tanpa build step), berbasis *Policy Brief*
**"Tiered Facilitation Model"**; core LMS terinspirasi [Frappe LMS](https://github.com/frappe/lms).

> Demo (setelah GitHub Pages aktif): `https://<user>.github.io/sipinter-kpu/`

## Fitur
- **Tiered Competency Engine — 10 tier**: Komisioner KPU RI · Provinsi · Kab/Kota ·
  Sekretariat Prov/Kab · PPK · PPS · KPPS · Relawan Demokrasi · Masyarakat Umum.
- **Alur 7 tahap** (Tiered Facilitation Model) — Tahap 2 dipersonalisasi per jenjang.
- **Knowledge Hub** — bank kasus sengketa, putusan DKPP/MK, PKPU/JDIH, best practice, FAQ.
- **AI Learning Assistant** — offline (RAG ringan) + live Claude (Edge Function `lms-ai`).
- **Certification & Talent** — CPD, digital badge, sertifikat, talent pool & succession.
- **Analytics** — dashboard, heatmap kompetensi, evaluasi dampak, predictive.
- **Sinkronisasi** — ekspor/impor JSON + konektor headless Frappe LMS.

## Struktur
\`\`\`
index.html  data.js  ai.js  sync.js  app.js  styles.css   # aplikasi PWA (root)
manifest.json  service-worker.js  icons/  screenshots/     # aset PWA
ARCHITECTURE.md   # blueprint platform (8 layer, 10 tier, integrasi, roadmap)
DEPLOY.md         # panduan deployment (AI Live, Frappe LMS, SSO, RAG)
USULAN-HNP.md     # integrasi ke Usulan HNP KPU Jabar + glosarium akronim
BIAYA-PENGEMBANGAN.md  # RAB estimasi biaya jadi app kelas Udemy/Coursiv (L1-L6)
supabase/functions/lms-ai/   # Edge Function relay Claude (kunci di server)
.github/workflows/pages.yml  # auto-deploy GitHub Pages
\`\`\`

## Menjalankan lokal
\`\`\`bash
python3 -m http.server 8080   # buka http://localhost:8080/
\`\`\`

## AI Live (opsional)
Tanpa konfigurasi, AI Assistant menjawab dari Knowledge Base lokal (offline). Untuk Claude:
1. \`supabase functions deploy lms-ai --no-verify-jwt\`
2. Set secret \`ANTHROPIC_API_KEY\` di Supabase.
3. Di app: **AI Assistant -> Pengaturan** -> mode *Edge* -> isi URL function.

## Regenerasi aset (ikon & screenshot)
\`\`\`bash
sudo apt-get install -y librsvg2-bin
cd screenshots && ./build.sh
\`\`\`

---
Prototipe edukatif & non-komersial. Verifikasi konten ke sumber resmi (JDIH KPU, DKPP, MK)
sebelum penggunaan kelembagaan. Berasal dari repo ReNamer-Pro (public/lms-kpu).
