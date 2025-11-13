# ==========================================
# 📊 Analisis Nilai Siswa
# ==========================================
# Penulis : [Navalovsky Jose Allenzo]
# Deskripsi : Program untuk membaca data nilai siswa,
#             menghitung statistik dasar, dan menampilkan visualisasi.
# ==========================================

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sb

# === 1. Membaca Data CSV ===
# Pastikan file 'nilai_siswa.csv' berada di folder yang sama dengan file ini.
# Gunakan separator (;) sesuai format data.
data = pd.read_csv('nilai_siswa.csv', sep=';')

# === 2. Informasi Dasar Dataset ===
print("=== INFO DATA ===")
print(data.info())
print("\n=== 5 BARIS PERTAMA ===")
print(data.head())
print("\n=== DESKRIPSI NUMERIK ===")
print(data.describe(include='all'))

# === 3. Pastikan Kolom 'Nilai' Bertipe Numerik ===
# Jika ada nilai yang tidak bisa dikonversi (misal teks), akan dijadikan NaN
data['Nilai'] = pd.to_numeric(data['Nilai'], errors='coerce')

# === 4. Pengecekan Nilai Kosong (NaN) ===
if data['Nilai'].isna().any():
    print("\n⚠ Ada nilai kosong setelah konversi:")
    print(data[data['Nilai'].isna()])

# === 5. Nilai Maksimum dan Minimum per Mata Pelajaran ===
agg_minmax = data.groupby('Matpel')['Nilai'].agg(['max', 'min'])
print("\n=== MAX & MIN per Matpel ===")
print(agg_minmax)

# === 6. Hitung Rata-Rata Nilai per Mata Pelajaran ===
rata = data.groupby('Matpel')['Nilai'].mean()
print("\n=== RATA-RATA per Matpel ===")
print(rata)

# === 7. Visualisasi: Grafik Batang Rata-Rata Nilai ===
warna = ['#FF6B6B', '#FFD93D', '#6BCB77', '#4D96FF', '#C77DFF']

rata.plot(kind='bar', color=warna[:len(rata)], edgecolor='black')
plt.title('Rata-Rata Nilai per Mata Pelajaran')
plt.xlabel('Mata Pelajaran')
plt.ylabel('Nilai Rata-Rata')
plt.tight_layout()
plt.show()

# === 8. (Opsional) Visualisasi: Boxplot Sebaran Nilai ===
# Hapus tanda komentar di bawah untuk menampilkan boxplot
# sb.boxplot(x='Matpel', y='Nilai', data=data)
# plt.title('Sebaran Nilai per Mata Pelajaran')
# plt.tight_layout()
# plt.show()

# ==========================================
# Akhir Program
# ==========================================
![Grafik Rata-Rata Nilai](diagram_siswa.png)

