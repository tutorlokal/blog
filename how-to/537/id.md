Pagi ini saya menemui sebuah kasus dimana saya perlu *update record* pada suatu tabel di database PostgreSQL secara massal. Katakanlah saya memiliki tabel bernama **tbl_katalog** yang memiliki kolom sebagai berikut:

| Nama Kolom | Tipe Kolom |
| ---------- | ---------- |
| id         | int        |
| product_id | int        |
| vendor_id  | int        |
| price      | float      |

Nah, kemudian saya ingin merubah harga pada *record* dengan ID tertentu yang saya inginkan. Misalnya perubahan yang saya inginkan seperti ini:

| id   | price |
| ---- | ----- |
| 62   | 45100 |
| 95   | 35250 |
| 171  | 65800 |

Ada banyak sekali *record* yang hendak saya rubah yang tidak mungkin saya lakukan satu per satu menggunakan perintah `UPDATE ... SET ...`. Oleh karena itu saya membuat file CSV yang berisi daftar ID dan harga yang baru, kemudian lakukan query untuk memperbarui data yang sudah ada dalam database secara massal.

Pertama, buatlah tabel sementara untuk menampung isi dari file CSV tadi.

```sql
CREATE TEMP TABLE tmp_new_price (
    id int,
    price float
);
```

Kedua, *import* file CSV ke tabel *temporary* yang dibuat tadi. Pada PostgreSQL terdapat dua perintah untuk *import record* dari file CSV, yang pertama `COPY` dan `\copy`. Perbedaannya adalah ketika menggunakan `COPY` maka perlu menggunakan *user* dengan akses *superuser*, sedangkan perintah `\copy` bisa digunakan oleh user dengan semua role. Di bawah ini contoh saya menggunakan `COPY` :

```sql
COPY tmp_new_price FROM '/absolute/path/to/file' (FORMAT csv);
```

Baru kemudian menggunakan perintah `UPDATE` dengan mengambil nilai dari tabel *temporary* ke tabel yang ingin diperbarui:

```sql
UPDATE tbl_katalog
SET price = tmp_new_price.price
FROM tmp_new_price
WHERE tbl_katalog.id = tmp_new_price.id;
```

Setiap *record* yang ID-nya sesuai dengan ID yang ada di dalam tabel *temporary* akan diperbarui. Jika proses *update* berhasil, selanjutnya *drop* tabel *temporary* tadi.

```sql
DROP TABLE tmp_new_price;
```

Demikian artikel kali ini, semoga bisa bermanfaat.

###### Reference

- https://stackoverflow.com/questions/8910494/how-to-update-selected-rows-with-values-from-a-csv-file-in-postgres