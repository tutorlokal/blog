Saya menggunakan PyCharm untuk proses pengembangan modul di Odoo, salah satu kemudahan yang ditawarkan oleh PyCharm adalah fitur *debug*-nya yang sangat bagus ketimbang harus manual menggunakan PDB atau IPDB. Namun ada yang berbeda sejak Odoo merilis versi 12.0, yakni ketika saya  tengah melakukan *debugging* muncul *exception* aneh yang mengatakan terjadi *KeyboardInterrupt*, dimana masalah tersebut tidak pernah terjadi pada versi Odoo sebelumnya ketika saya melakukan *debugging*. Hal tersebut terjadi berulang-ulang secara konstan setiap kali saya melakukan *debugging* sehingga rasanya cukup mengganggu.

![](https://raw.githubusercontent.com/tutorlokal/blog/master/how-to/594/media/01-keyboardinterrupt-pycharm-odoo.png)

Setelah saya cari tahu masalahnya ternyata disebabkan karena `limit_time_real` pada Odoo yang secara *default* diset dengan nilai 120 telah tercapai. Sehingga solusinya adalah dengan menambah angka limit tersebut, misalnya ingin debugging setidaknya bisa bertahan selama 10 menit, berarti nilai `limit_time_real` pada Odoo perlu diset sebear 600.

Hal tersebut telah saya coba dan berhasil, setelah menunggu 10 menit baru muncul *exception* tersebut. Sebenernya ini bukan solusi permanen, yang saya lakukan hanya menunda kemunculan *exception* tersebut. Jika Anda menemukan solusi lain, silakan komentar di bawah ini. Selamat mencoba, semoga berhasil!

