# Tahap 1 — Desain Eksperimen dan Struktur Data

**Status:** Draft awal

---

## 1. Tujuan Tahap

Tahap ini berfokus pada perancangan eksperimen simulasi untuk membandingkan dua kondisi algoritma probabilitas pada sistem gacha:

- Kondisi A: fixed probability
- Kondisi B: weighted probability dengan pity system

Tujuan utamanya adalah memastikan eksperimen memiliki parameter yang konsisten, data yang terstruktur, dan hasil yang dapat dibandingkan secara objektif.

## 2. Komponen Eksperimen

1. **Probability engine** — modul yang menentukan probabilitas saat setiap pull dilakukan.
2. **Pull simulator** — proses simulasi berulang untuk banyak pemain virtual.
3. **Logger / recorder** — menyimpan hasil setiap pull ke data mentah.
4. **Analyzer** — menghitung cumulative probability dan average pulls to rare.

## 3. Parameter Penelitian

| Parameter | Nilai |
|---|---:|
| Jumlah sampel | 100.000 responden virtual |
| Base probability | 0,6% |
| Soft pity threshold | pull ke-50 |
| Hard pity threshold | pull ke-70 |
| Random seed | 42 |
| Batas maksimum simulasi | 90 pull |

## 4. Struktur Data Hasil Simulasi

Data hasil eksperimen disimpan dalam format CSV dengan kolom utama berikut:

```text
Pull_Ke, Cumulative_Probability_Fixed, Cumulative_Probability_Weighted
```

Selain itu, hasil pengolahan lebih lanjut disimpan ke folder [../04-data](../04-data) dan [../06-output](../06-output).

## 5. Alur Eksperimen

```text
Parameter penelitian → simulasi pull → pencatatan hasil → penghitungan cumulative probability → ekspor CSV → visualisasi
```

## 6. Keputusan Teknis

1. Penelitian menggunakan simulasi komputer karena memungkinkan kontrol parameter yang lebih baik dibanding eksperimen langsung pada sistem game nyata.
2. Kedua kondisi diuji dengan parameter yang sama agar hasil perbandingan valid.
3. Data hasil eksperimen akan dipakai sebagai dasar analisis statistik dan penulisan naskah penelitian.
