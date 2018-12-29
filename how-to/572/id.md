Jika di Windows kita mengenal Snagit, yaitu aplikasi screenshot yang dilengkapi dengan image editor, maka di Linux kita dapat menggunakan alternatifnya yang bernama Shutter. Memang tidak secanggih Snagit kalau dibandingkan *head-to-head*, namun menurut saya Shutter sudah lebih dari cukup untuk digunakan di Linux. Berikut fitur Shutter yang saya suka:

- Window Screenshot: kita dapat mengambil screenshit berdasarkan jendela aplikasi sesuai keinginan.
- Selection Screenshot: kita dapat mengambil screenshot sesuai area yang kita inginkan.
- Delay Screenshot: kita dapat mengatur waktu screenshot, ada countdown-nya juga.
- Image Editor: ini yang paling saya butuhkan dalam sebuah aplikasi screenshot yaitu adanya image editor yang sudah bawaan sama seperti snagit.

Masih banyak lagi fitur dari Shutter, fitur-fitur di atas adalah yang paling sering saya gunakan.

## Cara Install Shutter di Ubuntu 18.04

1. Buka terminal.

2. Gunakan perintah berikut untuk memasang shutter:

   ```bash
   $ sudo apt-get install shutter
   ```

3. Jika proses install selesai, silakan buka aplikasi shutter.

## Cara Mengaktifkan Fitur Image Editor pada Shutter

Sayangnya fitur image editor tersebut tidak langsung aktif karena biasanya ada dependency tambahan yang diperlukan, sehingga kita harus juga memasang dependency yang dibutuhkan tersebut. Silakan ikuti perintah berikut:

```bash
$ mkdir /tmp/libgoo-canvas-perl && cd /tmp/libgoo-canvas-perl
$ wget http://archive.ubuntu.com/ubuntu/pool/universe/libg/libgoo-canvas-perl/libgoo-canvas-perl_0.06-2ubuntu3_amd64.deb
$ wget http://archive.ubuntu.com/ubuntu/pool/universe/libe/libextutils-depends-perl/libextutils-depends-perl_0.405-1_all.deb
$ wget http://archive.ubuntu.com/ubuntu/pool/universe/libe/libextutils-pkgconfig-perl/libextutils-pkgconfig-perl_1.15-1_all.deb
$ wget http://archive.ubuntu.com/ubuntu/pool/universe/g/goocanvas/libgoocanvas3_1.0.0-1_amd64.deb
$ wget http://archive.ubuntu.com/ubuntu/pool/universe/g/goocanvas/libgoocanvas-common_1.0.0-1_all.deb
$ sudo dpkg -i *.deb
$ sudo apt install -f
```

Itu saja untuk kali ini, semoga bermanfaat!

## Reference

- https://vitux.com/how-to-install-and-use-shutter-screenshot-tool-in-ubuntu-18-04-lts/

