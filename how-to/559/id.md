Suatu ketika saya membutuhkan pemindaian *barcode* pada Odoo, namun saat itu tidak ada perangkat *barcode scanner* yang bisa saya gunakan untuk melakukan pengujian fitur *scan barcode*. Sehingga saya mencoba untuk melakukan simulasinya tanpa harus menggunakan perangkat *barcode scanner* yang sesungguhnya.

Hal itu dimungkinkan dengan menggunakan Javascript yang kita eksekusi melalui *Chrome Console*. Berikut langkah-langkah untuk melakukan simulasi ini:

1. Buka halaman pada Odoo dimana ingin melakukan *barcode scanning*.

2. Kemudian bukan *console* pada *browser*, jika menggunakan Google Chrome maka bisa menggunakan *keyboard shortcut* **CTRL+SHIFT+J**.

3. Kemudian jalankan *script* berikut pada *console* tersebut!

   ```javascript
   function triggerKeypressEvent(char) {
       var keycode;
       if (char === "Enter") {
           keycode = $.ui.keyCode.ENTER;
       } else {
           keycode = char.charCodeAt(0);
       }
       return $('body').trigger($.Event('keypress', {which: keycode, keyCode: keycode}));
   }
   ```

4. Kemudian anda bisa menyimulasikan proses pemindaian *barcode* dengan menggunakan *script* berikut:

   ```javascript
   _.each("711301249806".split('').concat('Enter'), triggerKeypressEvent)
   ```

   ***Hint***:

   - Silakan ganti nilai "711301249806" sesuai dengan kode barcode anda.

5. Selanjutnya Odoo akan merespon *event scan barcode* sesuai fitur yang tersedia.

Berikut video demonstrasi ketika saya mencoba langkah-langkah di atas, selamat menyaksikan semoga bermanfaat !
[![](https://img.youtube.com/vi/LQYGjeclD2Q/maxresdefault.jpg)](https://www.youtube.com/watch?v=LQYGjeclD2Q "Testing Inventory Adjustments with Barcode Scan Simulation in Odoo")