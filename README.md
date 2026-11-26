# Akuisisi dan Integrasi Data Pariwisata Pulau Lombok (NTB)

Dokumentasi teknis Ujian Tengah Semester mata kuliah **Data Acquisition & Management (BIFP-243)**, INSTIKI.

## 1. Identitas Mahasiswa
| Informasi | Keterangan |
| :--- | :--- |
| **Nama** | Ni Kadek Rahayu Windari |
| **NIM** | 2501010176 |
| **Program Studi** | Informatika |
| **Kelas** | F |
| **Fokus Wilayah** | Pulau Lombok (Kabupaten Lombok Barat, Lombok Tengah, Lombok Timur, Lombok Utara, dan Kota Mataram) |

## 2. Tujuan Proyek (*Goals*)
1. Mengakuisisi data dari tiga mekanisme berbeda: pengunduhan berkas resmi (CSV), pemanggilan REST API (JSON), dan *web scraping* statis (HTML).
2. Menyimpan seluruh berkas mentah tanpa modifikasi di `data/raw/` dan hasil olahan bersih di `data/processed/`.
3. Mengevaluasi profil kualitas data (jumlah baris, kolom, tipe data, *missing values*, duplikasi) serta estimasi kebutuhan penyimpanan.
4. Mengintegrasikan seluruh sumber data melalui `pd.merge()` berkunci `kunci_wilayah` dan `tahun_kunci` dengan validasi `many_to_one` bebas duplikasi.
5. Mendokumentasikan silsilah data (`provenance.csv` beserta checksum MD5) dan kepatuhan etika data (daftar periksa 9 butir serta bukti `robots.txt`).

## 3. Sumber Data
| No | Metode | Sumber | URL | Lisensi | Status |
| :---: | :--- | :--- | :--- | :--- | :--- |
| 1 | Unduh Berkas CSV | Satu Data NTB (data.ntbprov.go.id), Dinas Pariwisata Provinsi NTB | https://data.ntbprov.go.id/dataset/9f040bf6-9148-42d7-9420-125ee229d599/show | License Not Specified | Tersedia (480 baris) |
| 2 | REST API | Open-Meteo Historical Weather | https://archive-api.open-meteo.com/v1/archive | CC BY 4.0 (Non-Komersial) | Tersedia (5,480 baris harian) |
| 3 | Web Scraping (ID) | Wikipedia (Kecamatan NTB) | https://id.wikipedia.org/wiki/Daftar_kecamatan_dan_kelurahan_di_Nusa_Tenggara_Barat | CC BY-SA 4.0 | Tersedia (117 baris kecamatan NTB) |
| 4 | Web Scraping (EN) | Wikipedia (West Lombok Regency) | https://en.wikipedia.org/wiki/West_Lombok_Regency | CC BY-SA 4.0 | Tersedia (10 kecamatan Lombok Barat) |

## 4. Struktur Direktori Proyek
- `data/raw/`: Berkas mentah orisinal (CSV, JSON API, HTML Wikipedia, dan arsip `robots.txt`) dalam bentuk *bytes* utuh.
- `data/processed/`: Dataset bersih per sumber, tabel terpadu (`hasil_gabungan_akhir.csv`), dan ringkasan lintas wilayah (`ringkasan_per_wilayah.csv`).
- `docs/`: Dokumentasi audit (`provenance.csv`, `data_ethics_checklist.csv`, `rekap_pemeriksaan_akhir.csv`, `endpoint_log.csv`, `metadata_gabungan.json`, `scraping_meta.json`, `robots_check.json`).
- `docs/charts/`: 6 grafik hasil analisis deskriptif dalam format PNG beresolusi 150 DPI.

## 5. Perangkat Lunak & Pustaka (*Tools*)
Python 3, Google Colab, `pandas`, `requests`, `BeautifulSoup4` (`html.parser`), `urllib.robotparser`, `matplotlib`, dan `hashlib`.
