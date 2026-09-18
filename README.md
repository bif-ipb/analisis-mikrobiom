# Analisis Mikrobiom 16S rRNA

[![Buka di Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bif-ipb/analisis-mikrobiom/blob/main/analisis_mikrobiom.ipynb)

Notebook praktikum untuk mengotomatisasi analisis data mikrobiom 16S rRNA dari NCBI SRA, mulai dari pengambilan metadata hingga analisis diversitas.

## Cakupan

Pipeline memproses 26 run dari BioProject `PRJNA1088555` yang terbagi menjadi:

| Kelompok | Layout | Jumlah run |
|---|---:|---:|
| Conventional farming practice | Paired-end | 12 |
| Organic farming practice | Paired-end | 11 |
| Organic farming practice | Single-end | 2 |
| Not applicable | Paired-end | 1 |

Tahapan utama:

1. Mengambil metadata BioProject dan BioSample dari NCBI.
2. Mengunduh data SRA dan mengubahnya menjadi FASTQ.
3. Menyiapkan FASTA untuk data paired-end dan single-end.
4. Menjalankan `Summary.seqs`, `Screen.seqs`, dan `Unique.seqs` dengan Mothur.
5. Menjalankan Kraken2 melalui Galaxy Australia menggunakan screened reads.
6. Menjalankan Bracken dan Krona jika database yang kompatibel tersedia.
7. Membuat matriks kelimpahan, indeks Shannon, dan matriks Bray-Curtis.

## Notebook

Buka [`analisis_mikrobiom.ipynb`](analisis_mikrobiom.ipynb) menggunakan salah satu lingkungan berikut:

- Google Colab
- Jupyter Notebook atau JupyterLab pada Linux
- Visual Studio Code dengan ekstensi Jupyter pada Windows

Jalankan sel secara berurutan dari atas ke bawah. Konfigurasi awal menyediakan dua mode:

```python
MODE = "uji"       # Memproses satu run
MODE = "lengkap"   # Memproses seluruh 26 run
```

Notebook disetel ke mode `lengkap`. Gunakan mode `uji` untuk pemeriksaan awal pada komputer baru.


### Menjalankan di Google Colab

Klik badge **Buka di Google Colab** di bagian atas README. Colab akan membuka notebook langsung dari branch `main`. Simpan salinan ke Google Drive sebelum mengedit agar perubahan dan hasil eksekusi tidak hilang ketika runtime berakhir.

## Galaxy Australia

Tahap Kraken2 menggunakan [Galaxy Australia](https://usegalaxy.org.au/). Buat API key dari akun Galaxy Australia, kemudian masukkan melalui prompt `getpass` ketika diminta. API key tidak ditulis ke notebook.

Jika hasil `Screen.seqs` sudah tersedia, analisis dapat dilanjutkan langsung dari bagian **Menghubungkan notebook ke Galaxy Australia**. Notebook akan memuat kembali `screen_seqs_manifest.csv` dan tidak mengulang tahap lokal.

## Penyimpanan Hasil

Semua hasil disimpan di direktori `mikrobioma_ncbi/`. Direktori ini tidak disertakan dalam Git karena dapat berisi FASTQ, FASTA, database, dan keluaran analisis berukuran besar.

Pada Google Colab, direktori `/content` akan hilang ketika runtime dihapus. Simpan hasil penting ke Google Drive atau penyimpanan lain sebelum mereset runtime.

## Kontributor

- Prof. Dr.Eng. Wisnu Ananta Kusuma, S.T., M.T.
- Said Thaufik Rizaldi, S.Kom., M.Kom.
- Gilland Fausta Putra Achyar, S.Mat., M.Kom.
- Sinda Cahyani, S.Si.

