---


---

<h2 id="tutorial-vuex-3-module--helpers">Tutorial Vuex #3: Module &amp; Helpers</h2>
<p><em><strong>Kesimpulan</strong></em><br>
<img src="https://vuex.vuejs.org/vuex.png" alt="enter image description here"><br>
Kadang kita mengenal lelucon, “<strong><em>Ketika codingan yang kita buat, hanya kita dan dan Tuhan yang tahu. Dan setelah beberapa saat, hanya Tuhan saja yang tahu</em></strong>.”.</p>
<p>Salah satu fitur lainnya dari Vuex, selain memudahkan kamu dalam manajemen  <em>state</em>  agar dapat digunakan oleh semua  <em>component</em>  yang berperan, juga memungkinkan kamu untuk memecah  <em>block code</em>  yang telah dibuat kedalam  <strong>Module</strong>  sesuai dengan peruntukannya masing-masing. Misalnya, kita memiliki 3 buah fitur, yakni:  <strong><em>Donatur, Client dan Transaksi</em></strong>. Jika ketiga  <em>code</em>  untuk meng-<em>handle</em>  fitur tersebut disatukan dalam satu buah  <em>file</em>, maka mengelolanya akan sangat membingungkan dikemudian hari. Bagaimana tidak? Jika  <em>code</em>  dari masing-masing fitur saling tercampur baur satu sama lain.</p>

