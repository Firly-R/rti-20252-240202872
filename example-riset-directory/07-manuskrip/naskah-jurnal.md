# Analisis Pengaruh Algoritma Weighted Probability terhadap Peluang Rare Item pada Sistem Gacha Game

**Penulis** : Muhammad Firly Ramadhan  
**Affiliasi** : Studi Ilmu Komputer, Fakultas Sains dan Teknologi, Universitas Putra Bangsa  
**Email** : [mfirlyrmd@gmail.com]

# Abstrak

**Abstrak**

Sistem gacha modern umumnya telah beralih dari probabilitas tetap (*fixed probability*) ke probabilitas berbobot (*weighted probability*) dengan sistem *pity* untuk meminimalkan ketidakpastian ekstrem. Penelitian ini membandingkan pengaruh kedua algoritma tersebut terhadap peluang kumulatif perolehan *rare item* melalui simulasi komputer dengan 100.000 sampel iterasi (probabilitas dasar 0,6%, *soft pity* 50, dan *hard pity* 70). Hasil simulasi menunjukkan bahwa *weighted probability* secara signifikan mempercepat perolehan *rare item* dengan rata-rata 46,35 *pull*, berbanding terbalik dengan *fixed probability* yang membutuhkan rata-rata 167,91 *pull*. Sistem berbobot ini juga mencapai peluang kumulatif 100% tepat pada *pull* ke-70. Temuan ini memberikan wawasan empiris bagi pengembang dalam merancang sistem gacha yang adil, menjaga retensi pemain, tanpa menghilangkan elemen peluang murni.  

**Kata Kunci:** *weighted probability; gacha game; cumulative probability; pity system; eksperimen simulasi.*

---

**Abstract**

*Modern gacha systems have largely transitioned from fixed to weighted probability utilizing a pity system to minimize extreme uncertainty. This study compares the effects of both algorithms on the cumulative probability of acquiring rare items through a computer simulation of 100,000 iterations (0.6% base probability, 50 soft pity, and 70 hard pity). The results indicate that weighted probability significantly accelerates rare item acquisition, averaging 46.35 pulls, compared to 167.91 pulls in the fixed probability model. The weighted system also successfully reaches a 100% cumulative probability exactly at the 70th pull. These findings provide empirical insights for developers to design fair gacha systems that maintain player retention without eliminating the element of pure chance.*

**Keywords:** *weighted probability; gacha game; cumulative probability; pity system; simulation experiment.*


# 1. Pendahuluan

Sistem gacha merupakan salah satu mekanisme monetisasi utama dalam industri video game modern, beroperasi melalui algoritma probabilitas untuk membagikan item virtual secara acak. Pada awalnya, sistem ini bergantung pada algoritma fixed probability (*probabilitas tetap*) di mana peluang mendapatkan rare item selalu konstan. Sayangnya, mekanisme ini memiliki celah berupa ketidakpastian ekstrem (*extreme variance*); pemain bisa gagal dalam ratusan percobaan (*pull*), yang sering kali berujung pada frustrasi dan menurunnya retensi pemain.

Untuk mengatasi kelemahan tersebut, game gacha modern berevolusi menggunakan weighted probability (*probabilitas berbobot*) yang terintegrasi dengan pity system. Melalui mekanisme soft pity dan hard pity, sistem secara dinamis meningkatkan peluang pemain setelah serangkaian kegagalan, hingga akhirnya memberikan jaminan pasti (100%) untuk mendapatkan rare item. Meski implementasi ini sangat lazim, dampak aktual algoritma dinamis ini terhadap *cumulative probability* (*peluang kumulatif*) secara matematis masih kurang terdokumentasi dalam literatur akademik, mengingat mayoritas penelitian terdahulu lebih berfokus pada dampak psikologis, perilaku perjudian, dan model penetapan harga.

Oleh karena itu, penelitian ini bertujuan menganalisis dan membandingkan secara kuantitatif distribusi *cumulative probability* serta rata-rata *pull* antara algoritma *fixed probability* dan *weighted probability* menggunakan eksperimen simulasi. Kebaruan (*novelty*) studi ini terletak pada pemodelan komparatif *head-to-head* menggunakan parameter probabilitas game modern. Hasil penelitian ini diharapkan dapat memberikan acuan objektif bagi pengembang perangkat lunak dalam merancang sistem gacha yang berimbang (*fair*)—mengurangi elemen frustrasi pemain, namun tetap mempertahankan elemen *randomness* yang esensial.


# 2. Tinjauan Pustaka

## 2.1 Sistem Gacha dan Loot Box
Sistem *gacha* memiliki kemiripan fundamental dengan mekanisme *loot box* di video game Barat, di mana pemain menukarkan mata uang (seringkali dibeli dengan uang sungguhan) untuk mendapatkan kotak hadiah virtual yang berisi *item* acak [2], [8]. Keduanya bergantung pada *Random Number Generator* (RNG) yang memetakan probabilitas tertentu untuk setiap *item*. Namun, sistem *gacha* modern umumnya lebih kompleks daripada *loot box* tradisional, dengan menambahkan banner promosi waktu terbatas dan mekanik bertingkat untuk *item* eksklusif. Penelitian menunjukkan bahwa mekanisme hadiah acak ini merangsang rilis dopamin, mirip dengan efek mesin slot, yang berkontribusi pada *engagement* tinggi [11].

## 2.2 Probabilitas pada Mekanik Gacha (Fixed vs Weighted)
Secara statistik, peluang memperoleh *item* dalam sistem *gacha* dapat dimodelkan menggunakan distribusi probabilitas diskrit. 
Pada sistem *Fixed Probability*, setiap percobaan (*pull*) adalah *independent event* dengan probabilitas keberhasilan $p$. Peluang kumulatif setidaknya satu keberhasilan setelah $n$ percobaan (*pull*) dapat dihitung menggunakan rumus distribusi Binomial komplementer:
$$ P(\text{setidaknya 1 sukses}) = 1 - (1 - p)^n $$
Sistem ini tidak memperhitungkan riwayat percobaan, sehingga peluang $p$ tetap konstan [1].

Sebaliknya, *Weighted Probability* mengimplementasikan probabilitas bersyarat di mana $p$ bervariasi bergantung pada $n$ dan jumlah kegagalan berturut-turut. Pada sistem ini, *engine* game akan menyesuaikan bobot (peluang) secara dinamis. Jika pemain gagal mendapatkan *rare item*, fungsi probabilitas akan mulai mendistribusikan bobot yang lebih besar ke *rare item* pada *pull* berikutnya. Hal ini menghilangkan sifat kejadian independen dari setiap percobaan gacha setelah melewati ambang batas tertentu.

## 2.3 Pity System dalam Game Modern
Untuk mereduksi frustrasi pemain akibat *outlier* statistik dari *fixed probability*, sebagian besar pengembang game modern mengimplementasikan *pity system*. Menurut Chen & Fang (2023) [1], *pity system* umumnya dibagi menjadi dua tahap:
1. **Soft Pity:** Suatu ambang batas jumlah percobaan $k$ di mana nilai $p$ secara inkremental dinaikkan. Pada fase ini, peluang mendapatkan *rare item* meningkat drastis per *pull*.
2. **Hard Pity:** Ambang batas maksimal di mana probabilitas $p$ disetel menjadi $1$ ($100\%$), menjamin pemain akan mendapatkan *rare item*.

Implementasi sistem ini selain berfungsi sebagai mekanisme keamanan bagi pemain (*safety net*), juga bertindak sebagai jangkar harga tak langsung (titik *ceiling price*) untuk sebuah *rare item* dalam ekonomi game [3], [10]. 

## 2.4 Related Works (Penelitian Terkait)
Beberapa studi terkini meneliti *gacha* dari perspektif analisis model matematika dan psikologi pemain. Gan (2022) [3] mengkaji sistem gacha dengan menghubungkannya pada *Prospect Theory* untuk menemukan *optimal pricing* dan menyimpulkan bahwa *pity system* memaksimalkan utilitas nilai tambah yang dirasakan pemain. Han et al. (2026) [4] merumuskan desain *loot box* optimal untuk menjaga stabilitas *in-game economy*. 

Namun, studi terkait pengukuran empiris perbedaan langsung peluang kumulatif dari algoritma probabilitas dinamis dibandingkan model probabilitas statis—khususnya yang menyajikan visualisasi data komparatif dari simulasi ribuan pemain—masih terbatas. Penelitian ini mengisi celah tersebut (*research gap*) dengan mensimulasikan model matematis *weighted probability* dalam struktur perangkat lunak, dan mengekstrak metrik kuantitatif (*cumulative probability*) untuk dianalisis.


# 3. Metodologi

## 3.1 Desain Eksperimen
Penelitian ini menggunakan pendekatan kuantitatif dengan desain eksperimen komparatif berbasis simulasi komputasi (*computer simulation-based experiment*). Simulasi dirancang untuk merepresentasikan mesin probabilitas pada *game gacha* modern, yang memungkinkan pengujian ekstensif terhadap algoritma RNG (*Random Number Generator*) dalam lingkungan terkendali [12].

Unit analisis dalam eksperimen ini adalah *log* transaksi *pull* individu (percobaan pengundian) yang merekam status keberhasilan mendapatkan *rare item* atau kegagalan (mendapatkan *non-rare item*). Data yang dievaluasi merupakan data primer yang dibangkitkan dari *probability engine* (*pull simulator*) yang merepresentasikan $100.000$ responden (*virtual players*). Populasi pengujian secara statis berukuran 100.000 iterasi penyelesaian untuk memastikan sampel statistik yang cukup besar dalam menormalkan variansi RNG.

## 3.2 Kondisi Eksperimen
Skenario pengujian dibagi menjadi dua grup komparatif secara eksplisit:
1. **Kondisi A (Baseline): Algoritma Fixed Probability.** Probabilitas mendapatkan *rare item* bersifat independen dan konstan pada setiap percobaan sebesar $0,6\%$. Tidak ada *pity system* yang diterapkan pada skenario ini.
2. **Kondisi B (Intervention): Algoritma Weighted Probability.** Probabilitas mendapatkan *rare item* mengikuti struktur mekanik dinamis (*pity system*) dengan parameter dasar yang sama ($0,6\%$), namun diberikan injeksi probabilitas secara progresif.

## 3.3 Parameter Simulasi Algoritma
Simulator *gacha* dibangun menggunakan bahasa pemrograman Python dengan memanfaatkan pustaka fungsi matematis standar, dieksekusi dengan menetapkan *random seed* global konstan untuk menjamin reproduktibilitas deterministik. 

Parameter sistem diatur selaras dengan model matematika game *gacha* kontemporer:
- **Base Probability:** $0,6\%$ ($0,006$)
- **Soft Pity Threshold:** *Pull* ke-$50$. Mulai titik ini, probabilitas *base* ditambahkan dengan probabilitas inkremental setiap kali pengundian gagal.
- **Hard Pity Threshold:** *Pull* ke-$70$. Jika pemain mencapai *pull* ke-70 tanpa pernah mendapatkan *rare item*, probabilitas sukses diubah paksa secara *hard-coded* menjadi $100\%$ ($1,0$).

Fungsi probabilitas $P(x)$ untuk *Weighted Probability* pada pull ke-$x$ (diasumsikan belum mendapatkan *rare item*) secara matematis didefinisikan sebagai:
- Jika $x < 50$, $P(x) = 0,006$
- Jika $50 \le x < 70$, $P(x) = 0,006 + \frac{x - 49}{70 - 50}$
- Jika $x = 70$, $P(x) = 1,0$

## 3.4 Metode Pengumpulan dan Analisis Data
Modul *pull simulator* merekam jumlah percobaan yang dibutuhkan setiap responden virtual dari *pull* ke-1 hingga titik pertama mereka sukses mendapatkan *rare item* (dibatasi maksimum 90 *pull* logis). Output rekaman dari setiap skenario disimpan secara terpisah dalam memori selama *runtime* dan diekspor ke dalam basis data *Comma-Separated Values* (.csv).

Analisis data difokuskan pada perhitungan Metrik *Cumulative Probability* dan *Average Pulls* (rata-rata jumlah *pull* yang dibutuhkan). *Cumulative probability* pada *pull* ke-$N$ dihitung dengan mengekstraksi frekuensi kumulatif pemain yang sukses mendapatkan item pada atau sebelum percobaan ke-$N$, lalu membaginya dengan jumlah total populasi virtual ($100.000$), yang dinyatakan dalam satuan persentase. Hasil analisis deskriptif kemudian diproyeksikan dalam tabel ringkasan distribusi dan visualisasi perbandingan grafik deret.


# 5. Hasil dan Analisis

## 5.1 Rata-Rata Jumlah Pengundian (Average Pulls)
Hasil observasi terhadap populasi virtual sebanyak $100.000$ iterasi menghasilkan metrik statistik deskriptif berupa rata-rata jumlah pengundian (rata-rata *pull*) yang dibutuhkan seorang pemain untuk mendapatkan satu *rare item*. 

- **Kondisi A (Fixed Probability):** Membutuhkan rata-rata **$167,91$ pull**. Mengingat probabilitas dasar adalah $0,6\%$ atau $1$ berbanding $166,6$, hasil rata-rata eksperimen ini sesuai dengan perhitungan teoretis ekspektasi logis dari distribusi geometrik (di mana $E(X) = 1/p$).
- **Kondisi B (Weighted Probability):** Membutuhkan rata-rata **$46,35$ pull**. Kehadiran *pity system* memotong ekor panjang (*long tail*) dari distribusi probabilitas, sehingga secara drastis mengurangi rata-rata percobaan yang dibutuhkan oleh pemain sebesar kurang lebih $72\%$. 

Hasil ini membuktikan bahwa algoritma *weighted probability* jauh lebih ramah terhadap waktu dan sumber daya pemain dibandingkan algoritma probabilitas statis murni, karena menjamin batas matematis nilai tengah.

## 5.2 Analisis Cumulative Probability
Nilai *Cumulative Probability* (Peluang Kumulatif) mengindikasikan berapa persentase basis populasi pemain yang sukses mendapatkan minimal satu *rare item* pada *pull* tertentu.

Tabel 1 menyajikan hasil perbandingan titik potong *Cumulative Probability* dari data *log* eksperimen:

| Percobaan (Pull Ke-$N$) | Cumulative Probability Fixed | Cumulative Probability Weighted |
|:---:|:---:|:---:|
| 1 | $0,58\%$ | $0,60\%$ |
| 10 | $5,80\%$ | $5,85\%$ |
| 30 | $16,30\%$ | $16,74\%$ |
| 50 (*Soft Pity*) | $25,66\%$ | $29,92\%$ |
| 60 | $29,98\%$ | $99,00\%$ |
| 70 (*Hard Pity*) | $33,96\%$ | $100,00\%$ |

Berdasarkan Tabel 1, pergerakan peluang kumulatif pada Kondisi A (*Fixed*) dan Kondisi B (*Weighted*) hampir identik dari *pull* ke-1 hingga *pull* ke-50, karena pada rentang tersebut fungsi probabilitas Kondisi B masih beroperasi pada konstanta $p = 0,006$. Sedikit variasi angka sepenuhnya merupakan dampak dari entropi RNG dari sampel simulasi.

Perbedaan fundamental terjadi tepat setelah *pull* ke-50 (*soft pity*). Pada algoritma *Weighted Probability*, injeksi bobot linear membuat *cumulative probability* melonjak drastis, mencapai angka fantastis $99,00\%$ pada *pull* ke-60. 
Batas mutlak (*hard pity*) divalidasi pada *pull* ke-70 dengan nilai peluang keberhasilan kumulatif persis mencapai $100,00\%$. Sebagai perbandingan, di titik yang sama (*pull* ke-70), kurang lebih $66\%$ populasi sistem *Fixed Probability* masih bernasib sial (*bad luck*) dan belum mendapatkan satupun *rare item*.

## 5.3 Pembahasan Trade-Off dan Keadilan Sistem (*Player Fairness*)
Kondisi A memperlihatkan apa yang disebut variansi ekstrem (*extreme variance*). Meskipun probabilitasnya "tetap" setiap kalinya, kenyataan matematis di tingkat populasi menunjukkan kurang dari sepertiga total pemain ($33,96\%$) yang mendapatkan hasil positif pada 70 percobaan pertama. Sisa dua pertiga pemain berisiko mengalami kelelahan (*burnout*) dan pengeluaran finansial yang tak terbatas.

Penerapan Kondisi B menyeimbangkan struktur insentif antara pengembang dan pemain. *Weighted probability* meminimalkan simpangan baku, memastikan adanya batas *spending* maksimal (sekitar $70$ kali harga *pull* dalam mata uang game) bagi pemain yang tidak beruntung, tanpa serta-merta memberikan item tersebut kepada pemain di 50 *pull* pertama (yang menjaga potensi pendapatan awal/ *early-game revenue* perusahaan). Dengan demikian, mekanisme ini mendukung keadilan pemain (*fairness*) yang disyaratkan oleh regulasi gacha, seperti standar pengungkapan probabilitas industri.


# 6. Kesimpulan dan Saran

## 6.1 Kesimpulan
Penelitian ini telah menyajikan analisis kuantitatif secara empiris mengenai implementasi algoritma probabilitas pada sistem video game *gacha*. Berdasarkan data hasil simulasi $100.000$ populasi percobaan, mekanisme *weighted probability* dengan *pity system* terbukti secara eksponensial lebih efisien dan menjamin kesetaraan bagi pemain dibandingkan model *fixed probability* tradisional. Intervensi peningkatan probabilitas di fase *soft pity* (mulai *pull* ke-50) berhasil mereduksi titik puncak frustrasi, dan *hard pity* memastikan jaminan pasti $100\%$ perolehan barang langkah tepat pada percobaan ke-70. Hal ini secara signifikan memangkas rata-rata panjang percobaan (*average pulls to rare*) dari $167,91$ kali di sistem *fixed* menjadi hanya $46,35$ kali di sistem *weighted*, mengeliminasi fenomena batas peluang tak hingga yang merugikan secara psikologis.

## 6.2 Saran
Temuan dari studi ini membuka arah riset lanjutan dalam bidang algoritma desain hiburan interaktif (*interactive entertainment design algorithm*). Disarankan untuk mensimulasikan matriks probabilitas *multi-banner* bertingkat (misalnya, kondisi spesifik *featured weapon/character* rasio 50/50 yang sering diterapkan game populer) pada studi selanjutnya. Selain itu, diperlukan penelitian kualitatif pendamping mengenai tingkat kepuasan riil demografi pemain saat menyentuh *soft pity* berbanding perolehan murni (*raw luck*) guna mengkalibrasi lebih lanjut parameter probabilitas ideal bagi *player retention*.


# 7. Daftar Pustaka

[1] C. Chen and Z. Fang, “Gacha game analysis and design,” *Proceedings of the ACM on Measurement and Analysis of Computing Systems*, vol. 7, no. 1, pp. 1-45, 2023.

[2] L. Y. Xiao, T. C. Fraser, and P. W. Newall, “Opening pandora’s loot box: Weak links between gambling and loot box expenditure in China, and player opinions on probability disclosures and pity-timers,” *Journal of Gambling Studies*, vol. 39, no. 2, pp. 645-668, 2023.

[3] T. Gan, “Gacha game: When prospect theory meets optimal pricing,” *arXiv preprint arXiv:2208.03602*, 2022.

[4] J. Han, C. T. Ryan, and X. T. Tong, “Algorithms for loot box design,” *Operations Research*, 2026.

[5] L. Y. Xiao, L. L. Henderson, and P. W. Newall, “What are the odds? Poor compliance with UK loot box probability disclosure industry self-regulation,” *Plos one*, vol. 18, no. 9, p. e0286681, 2023.

[6] C. Cokki, H. Maupa, W. Wanstum, and S. Sulaiman, “Gacha Addiction and In-App Purchases: a Study on Genshin Impact Players in Indonesia,” *Matrik: Jurnal Manajemen, Strategi Bisnis, dan Kewirausahaan*, vol. 19, no. 1, 2025.

[7] R. Y. Priyangga and I. Salehudin, “Engagement and Consumption Behavior in Gacha Games: A PLS-SEM Study on Generation Z in Indonesia,” *Journal of Games, Game Art, and Gamification*, vol. 10, no. 2, pp. 65-73, 2025.

[8] J. W. Han, “Effects of Mobile Gacha Games on Gambling Behavior and Psychological Health,” *arXiv preprint arXiv:2504.00057*, 2025.

[9] R. Cao, W. Zhang, and F. Sun, “Price discrimination in mobile gacha games: A comprehensive study of the scarcity–pricing, gachaing–user profiling, and recharging–profiting models,” *Managerial and Decision Economics*, vol. 45, no. 6, pp. 3716-3733, 2024.

[10] N. O. M. Bakrie, C. Aditama, and L. Sanny, “The art of the gacha lure: Determinants of the continuous use of mobile role-playing games (RPG) with gacha system in Indonesia,” *JOURNAL OF APPLIED ENGINEERING AND TECHNOLOGICAL SCIENCE (JAETS)*, vol. 6, no. 1, pp. 626-640, 2024.

[11] M. Drummond and A. Sauer, "Video game loot boxes are psychologically akin to gambling," *Nature Human Behaviour*, vol. 2, no. 8, pp. 530-532, 2018.

[12] R. E. Shannon, *Systems Simulation: The Art and Science*. Englewood Cliffs, NJ: Prentice-Hall, 1975.


