# VisionTransformer Comparison on CIFAR-10

Notebook ini menyiapkan eksperimen transfer learning antara Swin Transformer (Tiny) dan DeiT Small pada dataset CIFAR-10. Pipeline diimplementasikan pada file `VisionTransformer_Comparison.ipynb` dan meliputi pemuatan dataset, visualisasi, pelatihan, evaluasi metrik per kelas, serta pengukuran waktu inferensi dengan prosedur warm-up. Seluruh proses disusun agar dapat dijalankan langsung di Google Colab sehingga tidak perlu menyiapkan lingkungan lokal yang berat.

## Struktur Repositori
- `VisionTransformer_Comparison.ipynb` &mdash; notebook utama yang berisi seluruh kode eksperimen.
- `requirements.txt` &mdash; daftar dependensi Python yang diperlukan untuk menjalankan notebook.

## Prasyarat
- Akun Google dan akses Google Colab (runtime GPU sangat disarankan).
- Jika ingin menjalankan secara lokal, gunakan Python 3.10+, GPU ≥8 GB, serta pip/virtual environment.

## Instalasi Dependensi
1. (Opsional) Buat dan aktifkan virtual environment.
2. Instal seluruh paket:
   ```bash
   pip install -r requirements.txt
   ```
3. Jika ingin menjalankan notebook melalui VS Code / JupyterLab, pastikan kernel menunjuk ke environment yang telah berisi dependensi di atas.

> Notebook juga menjalankan `pip install timm seaborn scikit-learn psutil` pada sel pertama untuk memastikan dependensi utama tersedia. Langkah ini dapat dilewati jika Anda sudah menjalankan perintah `pip install -r requirements.txt`.

## Menjalankan Notebook
1. Buka [Google Colab](https://colab.research.google.com/), pilih *File → Upload Notebook* dan unggah `VisionTransformer_Comparison.ipynb`.
2. Aktifkan runtime GPU melalui *Runtime → Change runtime type → GPU*.
3. Eksekusi sel secara berurutan. Notebook terbagi menjadi tahap-tahap yang diberi judul (Instalasi, Import Library, Load Dataset, Visualisasi, Utility Model, Training, Evaluasi, Inferensi, Ringkasan, dan Ekspor JSON) sehingga mudah diikuti.
4. Dataset CIFAR-10 akan otomatis diunduh oleh torchvision ke direktori kerja Colab (akan tersimpan di `/content/data/` selama sesi berlangsung). Pastikan runtime memiliki koneksi internet aktif.

> Untuk eksekusi lokal, jalankan `jupyter notebook VisionTransformer_Comparison.ipynb` setelah memasang dependensi via `pip install -r requirements.txt`.

### Catatan Pelaksanaan
- Ubah nilai pada dictionary `CONFIG` (sel "Langkah 3") untuk menyesuaikan hyperparameter seperti ukuran batch, jumlah epoch, learning rate, atau jumlah gambar yang digunakan saat benchmarking inferensi.
- Fungsi `benchmark_inference` mengukur rata-rata waktu per gambar, deviasi standar, throughput, dan estimasi waktu menyapu keseluruhan test set. Pastikan tidak ada proses berat lain di GPU/CPU ketika mengukur.
- Setelah setiap model selesai, notebook menampilkan kurva loss/accuracy, confusion matrix, tabel klasifikasi per kelas, dan merangkum seluruh metrik ke tabel ringkasan.

## Lisensi / Kredit
Dataset CIFAR-10 berasal dari [torchvision.datasets](https://pytorch.org/vision/stable/datasets.html#cifar). Model Swin dan DeiT disediakan oleh [timm](https://github.com/huggingface/pytorch-image-models). Notebook dikembangkan untuk tujuan pembelajaran perbandingan Vision Transformer.
