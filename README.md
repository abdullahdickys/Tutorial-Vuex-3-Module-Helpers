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
<a href="https://drive.google.com/file/d/1A0DlMlgpjDIIzdhIx573tthlgrXc3Yx3/view?usp=sharing">https://drive.google.com/file/d/1A0DlMlgpjDIIzdhIx573tthlgrXc3Yx3/view?usp=sharing</a><br>
Buat  <em>file</em>  <code>Donatur.vue</code>  didalam folder  <code>src/components</code>:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>template</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-group<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>label</span> <span class="token attr-name">for</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Donatur<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>label</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>select</span> <span class="token attr-name">@change</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>$emit(<span class="token punctuation">'</span>selectedDonatur<span class="token punctuation">'</span>, $event.target.value)<span class="token punctuation">"</span></span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-control<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>option</span> <span class="token attr-name">value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Pilih Donatur<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>option</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>option</span> <span class="token attr-name">v-for</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>donatur in listDonatur<span class="token punctuation">"</span></span> <span class="token attr-name">:key</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>donatur.id<span class="token punctuation">"</span></span> <span class="token attr-name">:value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>donatur.id<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
                    {{ donatur.name }}
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>option</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>select</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>template</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript">
    <span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token punctuation">{</span>
        computed<span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token comment">//MEMBUAT COMPUTED PROPERTY DENGAN NAMA listDonatur()</span>
            <span class="token function">listDonatur</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                <span class="token comment">//DATA DIAMBIL DARI STATE MODULE donatur</span>
                <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>$store<span class="token punctuation">.</span>state<span class="token punctuation">.</span>donatur<span class="token punctuation">.</span>listDonatur
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
</span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>

</code></pre>
<p><strong>Penjelasan</strong>: Yang perlu diperhatikan adalah  <em>computed property</em>  yang ada, dimana data tersebut berasal dari  <strong>module Vuex</strong>  yang bernama  <code>donatur</code>. Selanjutnya  <em>module</em>  ini akan kita buat pada sub topik selanjutnya.  <em>So</em>, cara mengambil data  <code>state</code>  dari Vuex adalah  <code>this.$store.state</code>  kemudian diikuti dengan nama state (jika tidak didalam  <em>module</em>) atau dengan nama  <em>module</em>  kemudian nama  <em>state</em>  (jika  <em>state</em>  tersebut berada didalam  <em>module</em>).</p>
<p><em>Component</em>  kedua adalah  <code>Clients.vue</code>, tempatkan didalam folder  <code>src/components</code>:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>template</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-group<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>label</span> <span class="token attr-name">for</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Jenis Bantuan<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>label</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>select</span> <span class="token attr-name">@change</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>$emit(<span class="token punctuation">'</span>selectedBantuan<span class="token punctuation">'</span>, $event.target.value)<span class="token punctuation">"</span></span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-control<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>option</span> <span class="token attr-name">value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Pilih Bantuan<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>option</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>option</span> <span class="token attr-name">v-for</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>row in listBantuan<span class="token punctuation">"</span></span> <span class="token attr-name">:key</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>row.id<span class="token punctuation">"</span></span> <span class="token attr-name">:value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>row.id<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
                    {{ row.name }}
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>option</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>select</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>template</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript">
    <span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token punctuation">{</span>
        computed<span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token function">listBantuan</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>$store<span class="token punctuation">.</span>state<span class="token punctuation">.</span>clients<span class="token punctuation">.</span>listBantuan
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
</span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>


</code></pre>
<p><strong>Note</strong>: Metode yang digunakan sama dengan  <em>component</em>  sebelumnya.</p>
<p><em>Component</em>  trakhir adalah  <code>Transaksi.vue</code>, letakkan didalam folder yang sama dengan  <em>component</em>  sebelumnya:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>template</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>table-responsive<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>table</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>table table-hover table-bordered<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>thead</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tr</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>#<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>Donatur<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>Jenis Bantuan<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>Jumlah<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tr</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>thead</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tbody</span><span class="token punctuation">&gt;</span></span>
                
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tbody</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>table</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>template</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript">
    <span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token punctuation">{</span>
        computed<span class="token punctuation">:</span> <span class="token punctuation">{</span>
            
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
</span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>


</code></pre>
<p><strong>Note</strong>:  <em>Computed property</em>  sengaja kita kosongkan, karena akan menggunakan pemanggilan  <code>state</code>  dengan  <em>helpers</em>.</p>
<p>Buka  <em>file</em>  <code>public/index.html</code>, kemudian tambahkan  <em>cdn</em>  Bootstrap karena kita akan menggunakan  <em>style</em>  dari Bootstrap:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>link</span> <span class="token attr-name">rel</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>stylesheet<span class="token punctuation">"</span></span> <span class="token attr-name">href</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css<span class="token punctuation">"</span></span> <span class="token attr-name">integrity</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO<span class="token punctuation">"</span></span> <span class="token attr-name">crossorigin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>anonymous<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>

</code></pre>
<p>Buka  <em>file</em>  <code>src/App.vue</code>, kemudian modifikasi menjadi:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>template</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">id</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>app<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
		<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>container<span class="token punctuation">"</span></span><span class="token style-attr language-css"><span class="token attr-name"> <span class="token attr-name">style</span></span><span class="token punctuation">="</span><span class="token attr-value"><span class="token property">padding-top</span><span class="token punctuation">:</span> <span class="token number">20</span>px</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
			<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>row<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
				<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>col-md-6<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
					<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card-header<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h3</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card-title<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Form Donasi<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h3</span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card-body<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>list-donatur</span> <span class="token attr-name">@selectedDonatur</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>selectedDonatur<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>lokasi-bencana</span> <span class="token attr-name">@selectedBantuan</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>selectedBantuan<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-group<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
								<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>label</span> <span class="token attr-name">for</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Jumlah Donasi (Rp)<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>label</span><span class="token punctuation">&gt;</span></span>
								<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>input</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>number<span class="token punctuation">"</span></span> <span class="token attr-name">v-model</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>jumlah<span class="token punctuation">"</span></span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-control<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>form-group<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
								<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>button</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>btn btn-primary btn-sm<span class="token punctuation">"</span></span>
									<span class="token attr-name">@click</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>submitDonasi<span class="token punctuation">"</span></span>
									<span class="token attr-name">:disabled</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>isLoading<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
									{{ isLoading ? 'Loading...':'Donasi!' }}
								<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>button</span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
					<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
				<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
				<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>col-md-6<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
					<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card-header<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h3</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card-title<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Donasi Terkumpul<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h3</span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>card-body<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
							<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>list-transaksi</span> <span class="token punctuation">/&gt;</span></span>
						<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
					<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
				<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
			<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
		<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>template</span><span class="token punctuation">&gt;</span></span>

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript">
	<span class="token keyword">import</span> Donatur <span class="token keyword">from</span> <span class="token string">'./components/Donatur.vue'</span>
	<span class="token keyword">import</span> Clients <span class="token keyword">from</span> <span class="token string">'./components/Clients.vue'</span>
	<span class="token keyword">import</span> Transaksi <span class="token keyword">from</span> <span class="token string">'./components/Transaksi.vue'</span>

	<span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token punctuation">{</span>
		<span class="token function">data</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
			<span class="token keyword">return</span> <span class="token punctuation">{</span>
				donatur<span class="token punctuation">:</span> <span class="token string">''</span><span class="token punctuation">,</span>
				clients<span class="token punctuation">:</span> <span class="token string">''</span><span class="token punctuation">,</span>
				jumlah<span class="token punctuation">:</span> <span class="token number">0</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span><span class="token punctuation">,</span>
		computed<span class="token punctuation">:</span> <span class="token punctuation">{</span>
			<span class="token function">isLoading</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                <span class="token comment">//MENGAMBIL STATE DARI ROOT VUEX (store.js)</span>
                <span class="token comment">//JADI, SETELAH .state. LANGSUNG MENYEBUTKAN NAMA STATENYA</span>
                <span class="token comment">//KARENA TIDAK MASUK KEDALAM MODULE</span>
				<span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>$store<span class="token punctuation">.</span>state<span class="token punctuation">.</span>isLoading
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span><span class="token punctuation">,</span>
		methods<span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token comment">//HANDLE EMIT DARI COMPONENT DONATUR</span>
			<span class="token function">selectedDonatur</span><span class="token punctuation">(</span>val<span class="token punctuation">)</span> <span class="token punctuation">{</span>
				<span class="token keyword">this</span><span class="token punctuation">.</span>donatur <span class="token operator">=</span> val
			<span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token comment">//HANDLE EMIT DARI COMPONENT CLIENTS</span>
			<span class="token function">selectedBantuan</span><span class="token punctuation">(</span>val<span class="token punctuation">)</span> <span class="token punctuation">{</span>
				<span class="token keyword">this</span><span class="token punctuation">.</span>clients <span class="token operator">=</span> val
			<span class="token punctuation">}</span><span class="token punctuation">,</span>
			<span class="token function">submitDonasi</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
				<span class="token comment">//AKAN KITA MODIFIKASI SELANJUTNYA</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span><span class="token punctuation">,</span>
		components<span class="token punctuation">:</span> <span class="token punctuation">{</span>
			<span class="token string">'list-donatur'</span><span class="token punctuation">:</span> Donatur<span class="token punctuation">,</span>
			<span class="token string">'lokasi-bencana'</span><span class="token punctuation">:</span> Clients<span class="token punctuation">,</span>
			<span class="token string">'list-transaksi'</span><span class="token punctuation">:</span> Transaksi
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
</span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>

</code></pre>
<p><strong>Note</strong>: Ketiga  <em>component</em>  tersebut kita  <em>import</em>  untuk digunakan pada  <em>form</em>  yang telah disediakan. Untuk penjelasan masing-masing  <em>methods</em>  yang terakait sudah saya sematkan didalam  <em>coding</em>  diatas.</p>
<p>Buat  <em>file</em>  <code>store.js</code>  didalam folder  <code>src</code>  kemudian tambahkan  <em>code</em>  berikut:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">import</span> Vue <span class="token keyword">from</span> <span class="token string">'vue'</span>
<span class="token keyword">import</span> Vuex <span class="token keyword">from</span> <span class="token string">'vuex'</span>

Vue<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>Vuex<span class="token punctuation">)</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token keyword">new</span> <span class="token class-name">Vuex<span class="token punctuation">.</span>Store</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
    state<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        isLoading<span class="token punctuation">:</span> <span class="token boolean">false</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    modules<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">// MODULE AKAN DITEMPATKAN DISINI</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>

</code></pre>
<p>Terakhir buka  <em>file</em>  <code>main.js</code>, kemudian modifikasi menjadi:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">import</span> Vue <span class="token keyword">from</span> <span class="token string">'vue'</span>
<span class="token keyword">import</span> App <span class="token keyword">from</span> <span class="token string">'./App.vue'</span>
<span class="token keyword">import</span> store <span class="token keyword">from</span> <span class="token string">'./store'</span> <span class="token comment">//IMPORT STORE.JS</span>

Vue<span class="token punctuation">.</span>config<span class="token punctuation">.</span>productionTip <span class="token operator">=</span> <span class="token boolean">false</span>

<span class="token keyword">new</span> <span class="token class-name">Vue</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  render<span class="token punctuation">:</span> h <span class="token operator">=&gt;</span> <span class="token function">h</span><span class="token punctuation">(</span>App<span class="token punctuation">)</span><span class="token punctuation">,</span>
  store <span class="token comment">// USE store</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">$mount</span><span class="token punctuation">(</span><span class="token string">'#app'</span><span class="token punctuation">)</span>


</code></pre>
<p>Baca Juga:  <a href="https://daengweb.id/tutorial-vuex-2-mutations-actions">Tutorial Vuex #2: Mutations &amp; Actions</a></p>
<h2 id="membuat-module-vuex--menggunakan-helpers">Membuat Module Vuex &amp; Menggunakan Helpers</h2>
<p><strong><em>Module</em></strong>  memungkinkan kita untuk memecah bagian dari aplikasi kita agar dapat di-<em>handle</em>  dengan mudah, sebab apabila digabungkan dalam satu  <em>file</em>  akan membentuk kumpulan  <em>code</em>  yang cukup besar dan menyulitkan kita untuk mencari bagian bagian yang akan dimodifikasi kemudian hari.</p>
<p>Buat sebuah folder dengan nama  <code>modules</code>  (<strong><em>baca</em></strong>: nama folder boleh beda, bebas.) didalam folder  <code>src</code>  untuk menampung  <em>file module</em>  yang akan dibuat selanjutnya. Terdapat 3 buah  <em>component</em>, dimana masing-masing  <em>component</em>  ini pada  <em>case</em>  kali ini akan kita kelompokkan menjadi 3 buah  <em>modules</em>  juga, yakni:  <strong>donatur, clients dan transaksi</strong>.</p>
<p>Pertama, buat  <em>file</em>  <code>donatur.js</code>  didalam folder  <code>src/modules</code>, kemudian masukkan  <em>code</em>  berikut:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> donatur <span class="token operator">=</span> <span class="token punctuation">{</span>
    namespaced<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    state<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        listDonatur<span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Riski Amelia'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Ima Sumadir'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Apri Yunita'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Tuti Winarti'</span> <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    mutations<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">// NONE</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    actions<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">// NONE</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> donatur

</code></pre>
<p><strong>Penjelasan</strong>: Terdapat sebuah  <strong>state</strong>  <code>listDonatur</code>  yang memiliki data  <em>default</em>  sebanyak 4 buah  <em>object</em>. Dimana data ini akan ditampilkan pada  <em>component</em>  <code>Donatur.vue</code>  yang telah dibuat sebelumnya.</p>
<p><em>File</em>  berikutnya adalah  <code>client.js</code>  yang diletakkan didalam folder  <code>src/modules</code>, kemudian tambahkan  <em>code</em>  berikut:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> clients <span class="token operator">=</span> <span class="token punctuation">{</span>
    namespaced<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    state<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        listBantuan<span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Gempa Lombok'</span><span class="token punctuation">,</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Beasiswa Pendidikan'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Banjir Bandang'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> name<span class="token punctuation">:</span> <span class="token string">'Tanggungan Kesehatan'</span> <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    mutations<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">// NONE</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    actions<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">// NONE</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> clients

</code></pre>
<p><strong>Note</strong>: Kegunaannya sama dengan  <em>module</em>  sebelumnya.</p>
<p>Terakhir, buat  <em>file</em>  <code>transaksi.js</code>  didalam folder  <code>src/modules</code>:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> transaksi <span class="token operator">=</span> <span class="token punctuation">{</span>
    namespaced<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    state<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">//DEFAULT DATA TRANSAKSI YANG AKAN DITAMPILKAN</span>
        <span class="token comment">//PADA COMPONENT TRANSAKSI.VUE</span>
        listTransaksi<span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span> id<span class="token punctuation">:</span> <span class="token string">'TRX1P1'</span><span class="token punctuation">,</span> donatur<span class="token punctuation">:</span> <span class="token string">'Anugrah Sandi'</span><span class="token punctuation">,</span> bantuan<span class="token punctuation">:</span> <span class="token string">'Gempa Lombok'</span><span class="token punctuation">,</span> jumlah<span class="token punctuation">:</span> <span class="token number">100000</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> id<span class="token punctuation">:</span> <span class="token string">'TRX1P2'</span><span class="token punctuation">,</span> donatur<span class="token punctuation">:</span> <span class="token string">'Dharma'</span><span class="token punctuation">,</span> bantuan<span class="token punctuation">:</span> <span class="token string">'Banjir Bandang'</span><span class="token punctuation">,</span> jumlah<span class="token punctuation">:</span> <span class="token number">250000</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span> id<span class="token punctuation">:</span> <span class="token string">'TRX1P3'</span><span class="token punctuation">,</span> donatur<span class="token punctuation">:</span> <span class="token string">'Asis Ramadhan'</span><span class="token punctuation">,</span> bantuan<span class="token punctuation">:</span> <span class="token string">'Beasiswa Pendidikan'</span><span class="token punctuation">,</span> jumlah<span class="token punctuation">:</span> <span class="token number">3000000</span> <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    mutations<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">//MENGUBAH STATE DENGAN</span>
        ADD_DONASI<span class="token punctuation">:</span> <span class="token punctuation">(</span>state<span class="token punctuation">,</span> payload<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
            <span class="token comment">//MENAMBAHKAN DATA BARU KEDALAM ARRAY MENGGUNAKAN PUSH()</span>
            state<span class="token punctuation">.</span>listTransaksi<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>payload<span class="token punctuation">)</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    actions<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token function">save_donasi</span><span class="token punctuation">(</span><span class="token punctuation">{</span> commit<span class="token punctuation">,</span> rootState <span class="token punctuation">}</span><span class="token punctuation">,</span> payload<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// rootState BERARTI MENGAKSES STATE YANG TIDAK BERADA DALAM MODULES</span>
            <span class="token comment">// DALAM HAL INI STATE isLoading YANG ADA DI DALAM FILE store.js</span>
            rootState<span class="token punctuation">.</span>isLoading <span class="token operator">=</span> <span class="token boolean">true</span> <span class="token comment">//SET TRUE UNTUK MEMBERIKAN EFEK LOADING</span>
            <span class="token function">setTimeout</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
                <span class="token comment">//MENGINSTRUKSIKAN PADA MUTATIONS TERKAIT UNTUK MENJALANKAN INSTRUKSINYA</span>
                <span class="token function">commit</span><span class="token punctuation">(</span><span class="token string">'ADD_DONASI'</span><span class="token punctuation">,</span> payload<span class="token punctuation">)</span>
                <span class="token comment">// STATE isLoading DI MATIKAN KEMBALI</span>
                rootState<span class="token punctuation">.</span>isLoading <span class="token operator">=</span> <span class="token boolean">false</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token number">1000</span><span class="token punctuation">)</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> transaksi

</code></pre>
<p>Agar ketiga  <em>modules</em>  tersebut dapat digunakan, maka kita harus mendefinisikannya pada  <em>root</em>  Vuex, dalam hal ini  <em>file</em>  <code>store.js</code>, buka  <em>file</em>  tersebut kemudian modifikasi menjadi:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">import</span> Vue <span class="token keyword">from</span> <span class="token string">'vue'</span>
<span class="token keyword">import</span> Vuex <span class="token keyword">from</span> <span class="token string">'vuex'</span>
<span class="token comment">//IMPORT KETIGA MODULES</span>
<span class="token keyword">import</span> donatur <span class="token keyword">from</span> <span class="token string">'./modules/donatur'</span>
<span class="token keyword">import</span> clients <span class="token keyword">from</span> <span class="token string">'./modules/clients'</span>
<span class="token keyword">import</span> transaksi <span class="token keyword">from</span> <span class="token string">'./modules/transaksi'</span>

Vue<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>Vuex<span class="token punctuation">)</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token keyword">new</span> <span class="token class-name">Vuex<span class="token punctuation">.</span>Store</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
    state<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        isLoading<span class="token punctuation">:</span> <span class="token boolean">false</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    modules<span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token comment">//DEFINISIKAN KETIGA MODULE TERSEBUT</span>
        donatur<span class="token punctuation">,</span>
        clients<span class="token punctuation">,</span>
        transaksi
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>

</code></pre>
<p>Pada  <em>form input</em>  donasi kita memiliki sebuah tombol yang memicu  <em>methods</em>  <code>submitDonasi()</code>  ketika di-klik. Dimana  <em>methods</em>  tersebut masih kita biarkan kosong pada sub topik sebelumnya.  <em>So</em>, buka  <em>file</em>  <code>App.vue</code>  kemudian modifikasi  <em>methods</em>  tersebut menjadi:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token function">submitDonasi</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// dispatch BERARTI MEMANGGIL FUNGSI YANG ADA DI ACTION</span>
    <span class="token comment">// DIMANA FUNGSI TERSEBUT BERNAMA save_donasi</span>
    <span class="token comment">// DAN BERADA DIDALAM MODULE transaksi</span>
    <span class="token comment">// JADI CARA MEMANGGILNYA ADALAH namamodule/namafungsi</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>$store<span class="token punctuation">.</span><span class="token function">dispatch</span><span class="token punctuation">(</span><span class="token string">'transaksi/save_donasi'</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
        <span class="token comment">//MENGIRIM 4 BUAH PARAMETER YANG AKAN DIPUSH KEDALAM LISTS ARRAY listTransaksi</span>
        id<span class="token punctuation">:</span> Math<span class="token punctuation">.</span><span class="token function">random</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">toString</span><span class="token punctuation">(</span><span class="token number">36</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">substring</span><span class="token punctuation">(</span><span class="token number">7</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        donatur<span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>donatur<span class="token punctuation">,</span>
        bantuan<span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>clients<span class="token punctuation">,</span>
        jumlah<span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>jumlah
    <span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>

</code></pre>
<p>Sampai pada tahap ini kita sudah berhasilkan membuat  <em>form</em>  untuk menambahkan data baru kedalam array  <code>listTransaksi</code>  untuk menampung data tersebut. Akan tetapi, listTransaksi belum dapat digunakan oleh  <em>component</em>  <code>Transaksi.vue</code>  karena data tersebut belum didefinisikan pada  <em>component</em>  terkait.</p>
<p>Yap! Kita akan menggunakan  <em>computed property</em>  untuk menggunakan  <em>state</em>  dari  <em>module</em>  transaksi. Hanya saja, jika dua  <em>component</em>  lainnya yakni:  <code>Donatur.vue</code>  dan  <code>Client.vue</code>  menggunakan cara  <code>this.$store.state.namamodule.namastate</code>, maka pada  <em>component</em>  <code>Transaksi.vue</code>  akan menggunakan  <em>helpers</em>  <code>mapState</code>.</p>
<p>Buka file  <code>Transaksi.vue</code>, kemudian modifikasi menjadi:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>template</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>table-responsive<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>table</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>table table-hover table-bordered<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>thead</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tr</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>#<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>Donatur<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>Jenis Bantuan<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>th</span><span class="token punctuation">&gt;</span></span>Jumlah<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>th</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tr</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>thead</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tbody</span><span class="token punctuation">&gt;</span></span>
                 <span class="token comment">&lt;!-- LOOPING LIST ARRAY DARI listTransaksi --&gt;</span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tr</span> <span class="token attr-name">v-for</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>(row, index) in listTransaksi<span class="token punctuation">"</span></span> <span class="token attr-name">:key</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>index<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>td</span><span class="token punctuation">&gt;</span></span>{{ index+1 }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>td</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>td</span><span class="token punctuation">&gt;</span></span>{{ row.donatur }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>td</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>td</span><span class="token punctuation">&gt;</span></span>{{ row.bantuan }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>td</span><span class="token punctuation">&gt;</span></span>
                    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>td</span><span class="token punctuation">&gt;</span></span>{{ row.jumlah }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>td</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tr</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tbody</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>table</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>template</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript">
    <span class="token keyword">import</span> <span class="token punctuation">{</span> mapState <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'vuex'</span> <span class="token comment">//IMPORT mapState</span>
    <span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token punctuation">{</span>
        computed<span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token comment">//MENGGUNAKAN HELPER mapState UNTUK MEMANGGIL MODULE transaksi</span>
            <span class="token operator">...</span><span class="token function">mapState</span><span class="token punctuation">(</span><span class="token string">'transaksi'</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
                <span class="token comment">// DIMANA DATA YANG AKAN DIAMBIL ADALAH STATE listTransaksi</span>
                listTransaksi<span class="token punctuation">:</span> state <span class="token operator">=&gt;</span> state<span class="token punctuation">.</span>listTransaksi
            <span class="token punctuation">}</span><span class="token punctuation">)</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
</span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>

</code></pre>
<p>Sampai pada tahap ini, aplikasi yang kita inginkan sudah berjalan sebagaimana mestinya. Jalankan  <em>command</em>  <code>npm run serve</code>.</p>
<p>Sebagai tambahan karena tidak sempat digunakan pada codingan diatas, maka untuk penggunaan  <em>helpers</em>  <code>mapActions</code>  dapat kamu lakukan dengan cara:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">methods<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    <span class="token operator">...</span><span class="token function">mapActions</span><span class="token punctuation">(</span><span class="token string">'namamodule'</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">'namafungsi'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token comment">//HELPERS ACTIONS YANG BERADA DALAM MODULE</span>
    <span class="token operator">...</span><span class="token function">mapActions</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token string">'namafungsi'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token comment">//HELPERS ACTION YANG TIDAK BERADA DALAM MODULE</span>
    <span class="token function">simpan</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">namafungsi</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token comment">//CARA MENGGUNAKAN ACTIONS YANG SUDAH DIPANGGIL MELALUI HELPERS</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>

