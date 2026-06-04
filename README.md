#  Road-Sentry

**Sistem Pelaporan & Deteksi Kerusakan Jalan Berbasis AI**

> Capstone Coding Camp 2026 — DBS Foundation | Tim CC26-PSU062
> Tema: **Inclusive & Resilient Communities**

Road-Sentry adalah platform web yang memungkinkan masyarakat melaporkan kerusakan jalan secara real-time, dilengkapi deteksi otomatis berbasis AI  dan dasboard admin dengan visualisasi peta GIS untuk mendukung respons infrastruktur yang lebih cepat dan merata.

---

##  Tim CC26-PSU062

| Nama | ID | Path | Peran |
|------|-----|------|-------|
| Abdul Latif Dzuhri | CACC222D6Y0876 | AI Engineer 
| Andhika Pratama Kurniawan | CACC222D6Y2564 | AI Engineer 
| Prety Afriani | CFCC220D6X2808 | Full-Stack Web Developer  (Frontend)
| Kanaya Aurellia Firsiel | CFCC220D6X1414 | Full-Stack Web Developer (Backend) 
| Yoga Dwi Prayoga | CDCC222D6Y1769 | Data Scientist 
| Fardho Zurrahman | CDCC222D6Y1784 | Data Scientist 
---

##  Fitur Utama

- **Pelaporan Publik** — Warga dapat mengirim foto kerusakan jalan beserta lokasi
- **Deteksi AI Otomatis** — YOLOv8s mendeteksi jenis kerusakan: `pothole`, `crack`, `manhole`
- **Priority Scoring** — Sistem menilai tingkat prioritas perbaikan berdasarkan tingkat kerusakan, kondisi jalan sekitar, fasilitas terdekat, dan frekuensi laporan
- **Admin Dashboard** — Peta GIS interaktif dengan detail laporan dan hasil AI per titik kerusakan
- **Status Tracking** — Pelapor dapat memantau status laporan mereka secara real-time setelah submit laporan
- **Foto Perbandingan** — Tampilan foto asli vs hasil anotasi AI dengan lightbox fullscreen

---

## Cara Menjalankan Project

### 1. Clone Repositori

```bash
git clone https://github.com/knyaurelliaaf/Capstone-Project-RoadSentry.git
cd Capstone-Project-RoadSentry
```

---

### 2. Menjalankan AI Service (FastAPI + YOLOv8)

```bash
cd "AI Engineer"

# Install dependencies
pip install -r requirements.txt
```

Jalankan server:

```bash
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

### 3. Menjalankan Backend (Node.js + Express)

```bash
cd ../Backend

# Install dependencies
npm install
```

Buat file `.env` di folder `Backend/`:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/road-sentry
# Jika pakai MongoDB Atlas:
# MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/road-sentry

FASTAPI_URL=http://localhost:8000
```

Jalankan server:

```bash
npm run dev

> Backend akan berjalan di `http://localhost:5000`

---

### 4. Menjalankan Frontend (React + Vite)

```bash
cd ../Frontend

# Install dependencies
npm install
```

Buat file `.env` di folder `Frontend/`:

```env
VITE_API_URL=http://localhost:5000
```

Jalankan development server:

```bash
npm run dev
```

> Frontend akan berjalan di `http://localhost:5173`

---

##  Alur Penggunaan

1. **Warga** membuka aplikasi dan mengisi form laporan kerusakan jalan (foto + lokasi + deskripsi)
2. **Backend** menerima laporan, menyimpan ke MongoDB, lalu mengirim gambar ke FastAPI
3. **FastAPI** menjalankan YOLOv8s → mengembalikan `annotated_image` (base64), `damage_summary`, dan `detections`
4. **Priority Scoring Engine** menghitung skor prioritas berdasarkan tingkat kerusakan, kondisi jalan via Overpass API, fasilitas sekitar, frekuensi laporan, dan usia laporan
5. **Pelapor** dapat memantau status laporan di halaman `ReportStatus` dengan polling otomatis tiap 3 detik
6. **Admin** melihat semua laporan di peta GIS, dengan detail AI dan skor prioritas per laporan

---


Proyek ini dibuat untuk keperluan Capstone Coding Camp 2026 — DBS Foundation.

---

