# VisionTransformer Comparison on CIFAR-10

Notebook ini menyiapkan eksperimen transfer learning antara Swin Transformer (Tiny) dan DeiT Small pada dataset CIFAR-10. Pipeline diimplementasikan pada file `VisionTransformer_Comparison.ipynb` dan meliputi pemuatan dataset, visualisasi, pelatihan, evaluasi metrik per kelas, serta pengukuran waktu inferensi dengan prosedur warm-up.

## Struktur Repositori
- `VisionTransformer_Comparison.ipynb` &mdash; notebook utama yang berisi seluruh kode eksperimen.
- `data/` &mdash; lokasi default untuk cache CIFAR-10 (akan otomatis dibuat/dimuat oleh torchvision).
- `requirements.txt` &mdash; daftar dependensi Python yang diperlukan untuk menjalankan notebook.
- `Tugas_Vision_Transformer_Comparison.pdf` &mdash; dokumen referensi (tidak diperlukan untuk menjalankan kode).

## Prasyarat
- Python 3.10 atau lebih baru.
- GPU dengan memori minimal 8 GB direkomendasikan (notebook menggunakan resolusi 224×224 dan batch size 128; pada GPU 6 GB perlu menurunkan `CONFIG["batch_size"]` agar terhindar dari OOM).
- Pip/virtual environment (conda, venv, dsb.) untuk mengelola paket.

## Instalasi Dependensi
1. (Opsional) Buat dan aktifkan virtual environment.
2. Instal seluruh paket:
   ```bash
   pip install -r requirements.txt
   ```
3. Jika ingin menjalankan notebook melalui VS Code / JupyterLab, pastikan kernel menunjuk ke environment yang telah berisi dependensi di atas.

> Notebook juga menjalankan `pip install timm seaborn scikit-learn psutil` pada sel pertama untuk memastikan dependensi utama tersedia. Langkah ini dapat dilewati jika Anda sudah menjalankan perintah `pip install -r requirements.txt`.

## Menjalankan Notebook
1. Buka terminal pada direktori ini (`VisionTransformer-Comparison`).
2. Jalankan Jupyter (Notebook atau Lab):
   ```bash
   jupyter notebook VisionTransformer_Comparison.ipynb
   ```
3. Eksekusi sel secara berurutan. Notebook terbagi menjadi tahap-tahap yang diberi judul (Instalasi, Import Library, Load Dataset, Visualisasi, Utility Model, Training, Evaluasi, Inferensi, Ringkasan, dan Ekspor JSON) sehingga mudah diikuti.
4. Dataset CIFAR-10 akan otomatis diunduh oleh torchvision ke folder `data/` jika belum tersedia. Pastikan koneksi internet aktif saat pertama kali menjalankan notebook.

### Catatan Pelaksanaan
- Ubah nilai pada dictionary `CONFIG` (sel "Langkah 3") untuk menyesuaikan hyperparameter seperti ukuran batch, jumlah epoch, learning rate, atau jumlah gambar yang digunakan saat benchmarking inferensi.
- Fungsi `benchmark_inference` mengukur rata-rata waktu per gambar, deviasi standar, throughput, dan estimasi waktu menyapu keseluruhan test set. Pastikan tidak ada proses berat lain di GPU/CPU ketika mengukur.
- Setelah setiap model selesai, notebook menampilkan kurva loss/accuracy, confusion matrix, tabel klasifikasi per kelas, dan merangkum seluruh metrik ke tabel ringkasan.
- Sel terakhir mengekspor ringkasan metrik penting (profil parameter, metrik utama, waktu inferensi, hardware) ke `experiment_results_summary.json` untuk dokumentasi lanjutan.

## Penyesuaian & Troubleshooting
- **Out Of Memory (OOM):** Turunkan `CONFIG["batch_size"]` atau ukuran input (`CONFIG["image_size"]`) jika GPU Anda memiliki memori terbatas.
- **Mengganti backbone:** Tambahkan entri baru pada dictionary `MODEL_SPECS` untuk menguji model timm lain selama memiliki checkpoint pra-latih dengan resolusi 224.
- **Headless environment:** Jalankan `jupyter nbconvert --to notebook --execute VisionTransformer_Comparison.ipynb` untuk mengeksekusi notebook tanpa UI. Pastikan semua dependensi tersedia.

## Lisensi / Kredit
Dataset CIFAR-10 berasal dari [torchvision.datasets](https://pytorch.org/vision/stable/datasets.html#cifar). Model Swin dan DeiT disediakan oleh [timm](https://github.com/huggingface/pytorch-image-models). Notebook dikembangkan untuk tujuan pembelajaran perbandingan Vision Transformer.
