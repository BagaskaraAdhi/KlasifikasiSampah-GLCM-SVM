<div align="center">
  <h1>♻️ Klasifikasi Citra Sampah Menggunakan GLCM dan SVM</h1>
  <p>
    <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
    <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white" alt="OpenCV" />
    <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white" alt="Scikit-Learn" />
    <img src="https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white" alt="Pandas" />
  </p>
</div>

<br>

Proyek ini merupakan implementasi *Computer Vision* dan *Machine Learning* untuk melakukan klasifikasi material fisik sampah secara otomatis. Sistem ini dibangun untuk mengenali jenis sampah berdasarkan **fitur-fitur tekstur permukaan** menggunakan algoritma **Support Vector Machine (SVM)**, tanpa bergantung pada warna objek. Proyek ini mencakup seluruh *pipeline* data, mulai dari prapemrosesan, ekstraksi citra, eksplorasi data (EDA), hingga evaluasi *Confusion Matrix*.

<hr>

<h1>📦 Informasi Dataset</h1>
Dataset yang digunakan terdiri dari <b>2.532 sampel citra</b> yang terbagi ke dalam 5 kelas material utama. Data visual ini diproses untuk mendapatkan karakteristik tekstur yang unik dari setiap jenis sampah.
<ul>
  <li><b>Cardboard (Kardus):</b> 403 sampel</li>
  <li><b>Glass (Kaca):</b> 501 sampel</li>
  <li><b>Metal (Logam):</b> 410 sampel</li>
  <li><b>Paper (Kertas):</b> 594 sampel</li>
  <li><b>Plastic (Plastik):</b> 482 sampel</li>
</ul>
Dataset publik ini diambil dari Kaggle: <a href="https://www.kaggle.com/datasets/asdasdasasdas/garbage-classification" target="_blank">Garbage Classification Dataset</a>.

<hr>

<h1>⚙️ Fitur yang Diekstraksi (GLCM)</h1>
Karena warna seringkali mengecoh dalam pemilahan limbah, proyek ini berfokus pada <b>Fitur Orde Kedua (Tekstur)</b> menggunakan metode <i>Gray Level Co-occurrence Matrix</i> (GLCM). Parameter yang digunakan adalah jarak 1 piksel dengan 4 arah sudut ($0^\circ, 45^\circ, 90^\circ, 135^\circ$).
Fitur kuantitatif yang diekstrak meliputi:
<ul>
  <li><b>Contrast:</b> Mengukur tingkat kekasaran dan variasi intensitas lokal citra.</li>
  <li><b>Homogeneity:</b> Mengukur keseragaman atau kehalusan distribusi piksel.</li>
  <li><b>Dissimilarity:</b> Mengukur jarak linear antar piksel yang bertetangga.</li>
  <li><b>Energy:</b> Mengukur konsentrasi pola atau <i>Angular Second Moment</i> (ASM).</li>
  <li><b>Correlation:</b> Mengukur ketergantungan linear antar nilai keabuan piksel.</li>
</ul>

<hr>

<h1>🚀 Tahapan Proyek</h1>
<ul>
  <li><b>Prapemrosesan Citra:</b> Mengonversi seluruh citra RGB menjadi <i>Grayscale</i> menggunakan OpenCV agar algoritma fokus murni pada intensitas cahaya dan pola fisik permukaan.</li>
  <li><b>Pembentukan Dataset Tabular:</b> Merata-ratakan 5 nilai fitur GLCM dari setiap gambar dan mengompilasinya menjadi format <i>DataFrame</i> Pandas, lalu mengekspornya menjadi file Excel (Dataset Numerik).</li>
  <li><b>Eksplorasi Data (EDA):</b> Menganalisis sebaran dan irisan antar kelas menggunakan <i>Scatterplot</i> (Contrast vs Homogeneity).</li>
  <li><b>Standardisasi Data:</b> Menyamakan rentang skala seluruh fitur tekstur menggunakan <code>StandardScaler</code> untuk stabilitas algoritma.</li>
  <li><b>Pemodelan Machine Learning:</b> Melatih model klasifikasi <b>SVM</b> menggunakan <code>kernel='rbf'</code> (<i>Radial Basis Function</i>) untuk menangani pola sebaran data tekstur yang bersifat <i>non-linear</i>, dengan pembagian data latih-uji 80:20.</li>
  <li><b>Evaluasi Model:</b> Mengukur kemampuan klasifikasi menggunakan metrik Akurasi, Presisi, Recall, F1-Score, dan divisualisasikan melalui <i>Confusion Matrix</i>.</li>
</ul>

<hr>

<h1>📊 Hasil dan Evaluasi</h1>
Pengujian model pada data uji (20% dari dataset) menghasilkan metrik performa sebagai berikut:
<ul>
  <li><b>Akurasi Keseluruhan:</b> 55.23%</li>
  <li><b>Performa Terbaik:</b> Model mengenali kelas <b>Kaca</b> dan <b>Kardus</b> dengan tingkat keyakinan (presisi/recall) tertinggi.</li>
</ul>

<b>Insight dari Confusion Matrix:</b>
<ul>
  <li>Terdapat tantangan klasifikasi pada kelas <b>Kertas</b> dan <b>Kardus</b>. Mesin sering keliru menebak di antara kedua kelas ini.</li>
  <li><b>Analisis:</b> Kesalahan ini secara matematis sangat logis karena kertas kusut/basah dan kardus memiliki matriks kekasaran tekstur (GLCM) yang hampir identik jika hanya dianalisis dari spektrum <i>grayscale</i>.</li>
  <li><b>Kesimpulan:</b> Fitur tekstur terbukti efektif sebagai fondasi sistem kecerdasan buatan, namun untuk mencapai akurasi industri, metode ini perlu dikombinasikan dengan ekstraksi bentuk (<i>edge detection</i>) atau bobot warna.</li>
</ul>
