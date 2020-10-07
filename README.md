---


---

<h2 id="tutorial-vuex-3-module--helpers">Tutorial Vuex #3: Module &amp; Helpers</h2>
<p><em><strong>Kesimpulan</strong></em><br>
<img src="https://vuex.vuejs.org/vuex.png" alt="enter image description here"><br>
Kadang kita mengenal lelucon, “<strong><em>Ketika codingan yang kita buat, hanya kita dan dan Tuhan yang tahu. Dan setelah beberapa saat, hanya Tuhan saja yang tahu</em></strong>.”.</p>
<p>Salah satu fitur lainnya dari Vuex, selain memudahkan kamu dalam manajemen  <em>state</em>  agar dapat digunakan oleh semua  <em>component</em>  yang berperan, juga memungkinkan kamu untuk memecah  <em>block code</em>  yang telah dibuat kedalam  <strong>Module</strong>  sesuai dengan peruntukannya masing-masing. Misalnya, kita memiliki 3 buah fitur, yakni:  <strong><em>Donatur, Client dan Transaksi</em></strong>. Jika ketiga  <em>code</em>  untuk meng-<em>handle</em>  fitur tersebut disatukan dalam satu buah  <em>file</em>, maka mengelolanya akan sangat membingungkan dikemudian hari. Bagaimana tidak? Jika  <em>code</em>  dari masing-masing fitur saling tercampur baur satu sama lain.</p>
<h2 id="tahap-persiapan">Tahap Persiapan</h2>
<pre class=" language-javascript"><code class="prism  language-javascript">vue create donasi
</code></pre>
<p>Next  <em>install library</em>  Vuex</p>
<pre class=" language-javascript"><code class="prism  language-javascript">npm install vuex <span class="token operator">--</span>save
</code></pre>
<p>Kita akan membuat 3 buah  <em>component</em>, yakni:  <strong>Donatur.vue</strong>  (untuk meng-<em>handle list</em>  donatur),  <strong>Clients.Vue</strong>  (untuk meng-<em>handle</em>  jenis bantuan) dan  <strong>Transaksi.vue</strong>  (untuk mencatat transaksi donasi yang telah dilakukan). Adapun hasil yang akan kita capai adalah sebagai berikut:<br>
<img src="https://drive.google.com/file/d/1A0DlMlgpjDIIzdhIx573tthlgrXc3Yx3/view?usp=sharing" alt="enter image description here"></p>

