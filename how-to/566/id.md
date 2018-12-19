Apakah anda pernah membuat map dengan menggunakan salah satu pustaka Javascript yaitu **Leaflet** ? 

[Leaflet]: https://leafletjs.com/	"LeafletJS"

 merupakan pustaka sumber terbuka untuk Javascript untuk membantu anda membangun aplikasi berbasis peta yang interaktif dan *mobile-friendly*. Dengan menggunakan pustaka ini, kita dapat dengan mudah membuat map pada aplikasi yang sedang kita kembangkan. Berikut contoh hasil tangkapan layar dari sebuah map yang saya buat menggunakan Leaflet.

![](https://raw.githubusercontent.com/tutorlokal/blog/master/how-to/566/media/1-leaflet-map-attribution-show.jpg)

Coba lihat pada bagian yang saya tandai dengan panah warna merah, terdapat atribusi yang bertuliskan "Leaflet" dan jika tulisan tersebut diklik maka akan mengarahkan anda ke situs resmi Leaflet.

Pada artikel kali ini saya akan memberikan trik mengenai bagaimana  caranya supaya tulisan 'Leaflet' pada bagian atribusi tersebut dapat dihilangkan. 

Sebenarnya caranya cukup sederhana, pada saat inisiasi map, tambahkan opsi `attributionControl: false` agar tidak muncul bagian atribusi pada map.

```javascript
var map = L.map('mapid', {
            ...
            attributionControl: false
        });

```
Selanjutnya perlu menambahkan kontrol terhadap map tersebut dengan kode berikut:

```javascript
L.control.attribution({prefix: false}).addAttribution('Tutor Lokal').addTo(map);
```
Dengan menggunakan kode tersebut maka atribusi yang muncul hanyalah tulisan "Tutor Lokal" tanpa disertai tulisan 'Leaflet'.
![](https://raw.githubusercontent.com/tutorlokal/blog/master/how-to/566/media/2-leaflet-map-attribution-hide.png)


Demikian trik kali ini, selamat mencoba dan semoga berhasil !