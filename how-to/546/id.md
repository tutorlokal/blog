Ketika saya menerapkan HTTPS pada Odoo dengan menggunakan Nginx, semua berjalan lancar kecuali satu, yakni POSBOX. Ketika mengakses POS yang telah dikonfigurasi untuk menggunakan POSBOX akan muncul pesan kesalahan terkait "*Mix Content*", hal itu disebabkan karena POS UI diakses menggunakan HTTPS, sementara beberapa *resource* lain yang dimuat menggunakan HTTP, karena tercampur seperti itu maka muncullah pesan kesalahan tadi.

Lalu bagaimana solusinya ? Pada artikel ini saya mengusulkan solusi yakni menerapkan HTTPS pada Odoo kecuali POS UI-nya. Sehingga ketika POS UI diakses menggunakan HTTP biasa tidak akan muncul error "*Mix Content*" lagi.

## Solusi

Secara teknis begini cara saya  menerapkan solusi di atas dengan membuat 3 *server block* pada Nginx:

- *Server block* port 80: Menggunakan protokol HTTP dan mengalihkan semua request yang datang pada port ini ke protokol HTTPS pada port 443.
- *Server block* port 443: Menggunakan protokol HTTPS dan menerapkan reverse proxy Nginx. Ketika ada *request* ke URI `/pos/web` pada port ini nantinya akan dialihkan ke port yang lain yang merupakan *reverse proxy* khusus menangani POS.
- *Server block* port 8080: Menggunakan protokol HTTP dan menerapkan reverse proxy Nginx khusus untuk URI `/pos/web` dan untuk *resource* lainnya yang berhubungan dengan POS. Sedangkan untuk *request* URI global akan dialihkan kembali ke HTTPS port 443.

## Contoh Konfigurasi Nginx

Berikut ini contoh konfigurasi Nginx pada *server block* port 80:

```
server {
...
	rewrite ^(.*) https://$host$1 permanent;
...
}
```

Berikut ini contoh konfigurasi Nginx pada *server bock* port 443:

```
server {
...
    # Redirect POS to http
    location ~ ^/pos/web {
        rewrite ^(.*) http://$host:8080$1 permanent;
    }
...
}
```

Berikut ini contoh konfigurasi Nginx pada *server block* port 8080:

```
server {
    listen [::]:8080;
    listen 8080;
    server_name odoo.tutorlokal.com;

	# Bring back all request to HTTPS
    location /web {
        rewrite ^(.*) https://odoo.tutorlokal.com$1 permanent;
    }

    # Except, POS UI and related resources. Keep it serve in HTTP.
    location ~* /(pos/web(.*)|mail|web_editor|web/(action|dataset|webclient|static(.*))|longpolling|point_of_sale|report) {
        proxy_pass  http://upstream.odoo.tutorlokal.com;
        # force timeouts if the backend dies
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_redirect off;

        # set headers
        proxy_set_header    Host            $host;
        proxy_set_header    X-Real-IP       $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

## Solusi Lain

Nah, itu tadi cara saya dalam mengatasi masalah ini, bagaimana dengan Anda ? SIlakan post pada kolom komentar jika Anda punya cara yang lain.

###### Reference

- [https://webkul.com/blog/serve-odoo-posbox-over-https/]: https://webkul.com/blog/serve-odoo-posbox-over-https/
