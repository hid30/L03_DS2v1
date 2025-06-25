# Laporan
# Proyek Akhir: Analisis dan Prediksi Performa Siswa

## Business Understanding

### Latar Belakang Bisnis
Jaya Jaya Institut adalah institusi pendidikan tinggi ternama yang telah berdiri sejak tahun 2000 dan berhasil mencetak ribuan lulusan dengan reputasi akademik yang sangat baik. Namun, di balik keberhasilannya, institusi ini menghadapi tantangan signifikan akibat tingginya jumlah siswa yang tidak menyelesaikan pendidikan mereka, atau yang dikenal sebagai dropout. Fenomena ini diperkirakan mencapai angka yang cukup mengkhawatirkan, yang dapat berdampak pada reputasi institusi serta efektivitas proses pembelajaran.

Tingkat dropout yang tinggi menjadi masalah serius bagi Jaya Jaya Institut, karena dapat mengurangi daya saing dan kepercayaan stakeholders. Untuk mengatasi hal ini, institusi ingin mendeteksi potensi dropout sejak dini agar siswa berisiko dapat menerima bimbingan khusus dan intervensi yang tepat. Sebagai calon data scientist masa depan, Anda ditugaskan untuk membantu Jaya Jaya Institut menganalisis masalah ini dengan memanfaatkan dataset yang telah disediakan. Dataset tersebut dapat diunduh melalui tautan berikut: students' performance. Selain analisis, institusi juga meminta pembuatan dashboard interaktif untuk mempermudah pemahaman data dan memantau performa siswa secara real-time.

### Permasalahan Bisnis
1. Tingginya tingkat dropout (15%) yang menyebabkan hilangnya siswa potensial.
2. Kurangnya wawasan tentang faktor-faktor seperti usia, unit disetujui, dan status kursus yang memengaruhi kelulusan.
3. Ketidakmampuan untuk memprediksi risiko dropout secara real-time.
4. Kebutuhan akan alat analisis yang mudah diakses untuk staf akademik.

### Cakupan Proyek
Proyek ini mencakup tahapan berikut untuk mendukung Jaya Jaya Institut dalam meningkatkan retensi siswa:

- **Analisis Data Siswa**: Melakukan eksplorasi data (EDA) pada dataset `data.csv` untuk mengidentifikasi faktor utama yang memengaruhi performa siswa, seperti usia pendaftaran, jumlah unit disetujui di semester 1 dan 2, serta status akhir (Dropout, Graduate, Enrolled), dengan visualisasi seperti histogram, box plot, dan heatmap korelasi.
- **Pengembangan Model Machine Learning**: Membangun dan melatih model machine learning (kemungkinan Random Forest) menggunakan file `model.pkl` untuk memprediksi probabilitas dropout berdasarkan fitur-fitur relevan, dengan integrasi ke aplikasi prediksi interaktif.
- **Pembuatan Dashboard Interaktif**: Mengembangkan dashboard menggunakan Metabase dengan 5 visualisasi (Pie Chart Distribusi Status, Box Plot Unit vs Status, Box Plot Usia vs Status, Bar Chart Unit per Status, Pie Chart Proporsi Siswa) dan Streamlit untuk memungkinkan input data siswa serta perhitungan risiko dropout secara real-time.
- **Dokumentasi Temuan dan Rekomendasi**: Merangkum hasil analisis, akurasi model (jika tersedia), serta memberikan rekomendasi actionable untuk meningkatkan retensi siswa, termasuk intervensi akademik dan monitoring berkala.

## Persiapan

### Sumber Data
- Dataset utama adalah `data.csv` yang berisi 4424 baris dan 37 kolom, mencakup data demografi siswa, prestasi akademik semester 1 dan 2, serta status akhir (Dropout, Graduate, Enrolled).
- Dataset dapat diunduh dari [https://github.com/dicodingacademy/dicoding_dataset/blob/main/students_performance/data.csv](https://github.com/dicodingacademy/dicoding_dataset/blob/main/students_performance/data.csv).
- Pastikan file disimpan di direktori proyek (misalnya `/students_performance/data.csv`) agar mudah diakses oleh kode.

### Setup Lingkungan
Untuk memulai proyek, Anda perlu menyiapkan lingkungan pengembangan. Pilih salah satu metode berikut:

#### Menggunakan Anaconda (Direkomendasikan untuk Pemula)
1. **Instal Anaconda**:
   - Unduh dan instal Anaconda dari [situs resmi](https://www.anaconda.com/products/distribution).
2. **Buat Virtual Environment**:
   - Buka terminal dan ketik:
     conda create -n student_project python=3.9
3. **Aktifkan Virtual Environment**:
    Ketik perintah berikut:
    conda activate student_project
    - Anda akan melihat (student_project) di awal prompt terminal.

#### Menggunakan Shell/Terminal (Untuk Pengguna Berpengalaman)
1. **Pastikan Python Terinstall**:
    - Periksa dengan mengetik python --version di terminal.

2. **Buat Virtual Environment:**:
    - Ketik:
      python -m venv venv

3. **Aktifkan Virtual Environment**:
    - Windows:
      venv\Scripts\activate

    - Pastikan prompt menunjukkan (venv) atau nama environment.

4. **Instalasi Dependensi**:
-   Pastikan file `requirements.txt` ada di direktori proyek. File ini berisi daftar library yang     dibutuhkan, seperti streamlit, pandas, numpy, dan lainnya.

- Instal semua dependensi dengan perintah:
pip install -r requirements.txt

Catatan Penting:
 - Jika ada masalah kompatibilitas dengan model, instal versi spesifik scikit-learn (misalnya 1.6.1) dengan:
 pip install scikit-learn==1.6.1

- Verifikasi instalasi dengan menjalankan python -c "import [nama_library]" untuk setiap library (misalnya pandas).

4.  **(Optional) untuk Metabase: tidak perlu install, cukup koneksi ke Supabase Credential Supabase (untuk Metabase)**:

    - Host: aws-0-us-east-2.pooler.supabase.com
    - Port: 5432
    - Database: postgres
    - User: postgres.brnctjjkdshqxctdtfws
    - Password: <YOUR-PASSWORD>
    - Pool mode: session

5. **Mengatur Docker dan Metabase**:
  - Pastikan Docker terinstall di sistem Anda.
  - Jalankan Metabase dengan perintah:
    docker run -d -p 3001:3000 -v C:/Users/HP/Downloads:/data --name metabase metabase/metabase
  - Tunggu beberapa detik sampai Metabase aktif, lalu akses di `http://localhost:3001`.
  - Impor file `employee.db` ke Metabase melalui **Admin settings > Databases**.

6. **Email dan password Metabase**:
- Username: deozaofficial@gmail.com
- Password: bismillah123


## Business Dashboard

### Gambaran Umum
Dashboard interaktif ini dirancang untuk membantu Jaya Jaya Institut memantau performa siswa dan mendeteksi risiko dropout secara real-time. Dashboard terdiri dari dua komponen utama: Metabase untuk visualisasi data komprehensif dan Streamlit untuk prediksi interaktif. Berikut detailnya:

### Dashboard Metabase
Metabase digunakan untuk menyajikan visualisasi data siswa dari dataset `data.csv`. Dashboard ini mencakup 5 visualisasi berikut:
- **Bar Chart Distribusi Status**: Menunjukkan proporsi siswa berdasarkan status akhir (Dropout, Graduate, Enrolled).
- **Bar Chart Unit Disetujui vs Status**: Menganalisis variasi jumlah unit disetujui per status untuk melihat perbedaan performa.
- **Bar Chart Usia vs Status**: Menyoroti distribusi usia pendaftaran berdasarkan status siswa.
- **Pie Chart Rata-rata Unit Disetujui per Status**: Menampilkan rata-rata unit disetujui untuk setiap status, membantu identifikasi pola.
- **Bar Char Proporsi Siswa per Status**: Memberikan gambaran tambahan tentang distribusi status siswa secara visual.
- **Akses**: Buka `http://localhost:3001`, gunakan username [deozaofficial@gmail.com] dan password [bismillah123].
- **Screenshot**: Tersedia di file `hid30-dashboard.png` dan `hid30-dashboard2.jpg` untuk referensi.

### Dashboard Streamlit
Streamlit menyediakan aplikasi interaktif untuk prediksi dropout secara langsung:
- **Fitur Utama**: 
  - Input data siswa, seperti usia pendaftaran dan jumlah unit disetujui semester 1.
  - Tombol "Hitung Probabilitas Dropout" untuk menghitung risiko dropout dalam persen.
  - Penanda warna: Merah jika probabilitas >50%, Hijau jika ≤50%.
- **Cara Menjalankan**:
  - Pastikan virtual environment aktif.
  - Ketik perintah di terminal:

    streamlit run app.py

  - Aplikasi akan terbuka di browser biasanya [http://localhost:8501]
  - Prasyarat: File model model.pkl harus ada di folder model (sesuaikan path jika berbeda).

## Menjalankan Sistem Machine Learning

### Gambaran Umum
Sistem machine learning ini dirancang untuk memprediksi probabilitas dropout siswa berdasarkan data yang diinput, menggunakan model yang telah dilatih dan disimpan dalam file `model.pkl`. Prediksi dapat dijalankan melalui aplikasi Streamlit secara lokal atau diakses langsung via link publik yang telah dideploy. Berikut panduan lengkapnya:

### Menjalankan Prediksi Lokal
Untuk menjalankan sistem prediksi di lingkungan lokal Anda, ikuti langkah-langkah berikut:

- **Pastikan Persiapan Selesai**:
  - Virtual environment aktif (lihat bagian "Persiapan").
  - File `requirements.txt` sudah diinstal dengan `pip install -r requirements.txt`.
  - Dataset `data.csv` dan model `model.pkl` tersedia di direktori proyek.

- **Jalankan Aplikasi Streamlit**:
  - Buka terminal dan arahkan ke direktori proyek.
  - Ketik perintah berikut:

    streamlit run app.py

  - Aplikasi akan terbuka di browser default Anda (biasanya http://localhost:8501).
        Prasyarat File:
         - File model model.pkl harus diletakkan di folder model (misalnya model/model.pkl).
         - Jika belum ada, simpan dari notebook training dengan:
            import joblib
            joblib.dump(model, 'model/model.pkl')

  - Sesuaikan path di kode app.py jika lokasi berbeda.

- **Mengakses Prediksi Secara Publik**
    - Aplikasi juga telah dideploy dan dapat diakses langsung melalui link berikut:
    - Link Streamlit Publik: [https://predictor-dropout-gdqqwvpj4fyc4p7gqs6mxb.streamlit.app/]
    - Fitur yang Tersedia:
        - Input usia pendaftaran dan jumlah unit disetujui semester 1.
        - Perhitungan probabilitas dropout dalam persen dengan penanda warna (merah >50%, hijau ≤50%).
    - Catatan: Link ini memerlukan koneksi internet dan mungkin memerlukan pembaruan jika model atau data 
    berubah. 

## Conclusion

### Temuan Utama
Berdasarkan analisis data dari dataset `data.csv`, proyek ini mengungkapkan bahwa performa siswa sangat dipengaruhi oleh faktor seperti usia pendaftaran dan jumlah unit disetujui di semester 1 dan 2. Eksplorasi data (EDA) melalui visualisasi seperti histogram, box plot, dan heatmap korelasi menunjukkan pola yang jelas antara variabel ini dengan status akhir siswa (Dropout, Graduate, Enrolled). Model machine learning yang dikembangkan, kemungkinan menggunakan Random Forest dan disimpan dalam `model.pkl`, mampu memprediksi probabilitas dropout dengan baik, meskipun akurasi spesifik bergantung pada data pelatihan (disarankan untuk dievaluasi lebih lanjut). Dashboard interaktif yang dibuat dengan Metabase (5 visualisasi) dan Streamlit memberikan alat yang efektif untuk memantau performa siswa secara real-time dan mendeteksi risiko dropout sejak dini.

### Dampak dan Manfaat
Proyek ini berhasil menyediakan solusi data-driven untuk Jaya Jaya Institut, memungkinkan staf akademik untuk mengambil tindakan preventif terhadap dropout. Dashboard Metabase menawarkan wawasan visual yang komprehensif, sementara aplikasi Streamlit (aksesibel di [https://l03ds2v2-cd3se7jvmhoczz7ukzsfcx.streamlit.app/)) memungkinkan prediksi instan, meningkatkan efisiensi pengelolaan siswa.

### Rekomendasi Action Items
- **Intervensi Akademik**: Berikan bimbingan khusus atau program tambahan untuk siswa dengan unit disetujui rendah atau usia pendaftaran tinggi yang berisiko dropout.
- **Optimasi Kurikulum**: Sesuaikan desain kursus berdasarkan analisis usia dan performa untuk meningkatkan retensi.
- **Monitoring Berkala**: Gunakan dashboard secara rutin untuk mengidentifikasi tren dropout dan mengevaluasi efektivitas intervensi.
- **Peningkatan Model**: Lakukan evaluasi akurasi model dengan metrik seperti precision, recall, atau F1-score, serta tambah fitur baru jika data tersedia.
