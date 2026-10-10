# meurah-keepalive

Penjadwal pemeliharaan untuk **demo publik Meurah** — Space
[`ghiyatsa/meurah`](https://huggingface.co/spaces/ghiyatsa/meurah) di Hugging Face.

## Kenapa repo ini ada

Space gratis di Hugging Face otomatis **tertidur setelah 48 jam tanpa
permintaan**. Alur kerja di repo ini mengirim satu permintaan ringan setiap
**12 jam** (09.00 dan 21.00 WIB) ke alamat demo, sehingga ambang tidur itu
tidak pernah tercapai — demo tetap siap dibuka kapan saja.

## Cara kerja

`.github/workflows/keepalive.yml` berjalan otomatis 2× sehari (dan bisa
dijalankan manual dari tab **Actions**):

1. **Ping demo** — satu `GET https://ghiyatsa-meurah.hf.space`, ringan dan
   aman; intervalnya sengaja longgar agar tidak terhitung lalu lintas agresif
   (permintaan yang terlalu rapat dapat dianggap penyalahgunaan oleh Hugging
   Face).
2. **Segarkan timer jadwal** — GitHub menonaktifkan alur terjadwal di repo
   publik yang tidak ada aktivitas selama 60 hari. Giliran ini memanggil API
   *enable* pada alurnya sendiri; pemanggilan itu menyetel ulang timer 60 hari
   (pola yang dipakai luas untuk repo pemeliharaan), jadi jadwal tetap hidup
   meski repo ini tidak pernah disentuh.

## Menghentikan

Hapus repo ini, atau nonaktifkan alurnya dari **Actions → Jaga demo Meurah →
Disable workflow**. Setelah itu Space kembali tidur dalam 48 jam tanpa akses —
dan akan bangun sendiri saat ada yang membukanya.

> Repo ini hanya berisi jadwal pemeliharaan; kode aplikasi Meurah ada di
> [muhfikry/a12026prjind03](https://github.com/muhfikry/a12026prjind03).
