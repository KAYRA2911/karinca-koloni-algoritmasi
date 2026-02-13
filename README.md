import numpy as np
import random
import matplotlib.pyplot as plt
# Şehirler arası mesafe matrisi
mesafeler = np.array([
[0, 2, 2, 5],
[2, 0, 3, 4],
[2, 3, 0, 6],
[5, 4, 6, 0]
])
sehir_sayisi = len(mesafeler)
karinca_sayisi = 10
iterasyon_sayisi = 30
buharlaşma = 0.4
feromon = np.ones((sehir_sayisi, sehir_sayisi))
en_kisa_mesafeler = []
def yol_uzunlugu(yol):
toplam = 0
for i in range(len(yol) - 1):
toplam += mesafeler[yol[i]][yol[i+1]]
return toplam
en_iyi_yol = None
en_kisa_mesafe = float("inf")
for _ in range(iterasyon_sayisi):
iterasyon_en_iyi = float("inf")
for _ in range(karinca_sayisi):
yol = list(range(sehir_sayisi))
random.shuffle(yol)
uzunluk = yol_uzunlugu(yol)
if uzunluk < en_kisa_mesafe:
en_kisa_mesafe = uzunluk
en_iyi_yol = yol
if uzunluk < iterasyon_en_iyi:
iterasyon_en_iyi = uzunluk
for i in range(len(yol) - 1):
feromon[yol[i]][yol[i+1]] += 1 / uzunluk
feromon *= (1 - buharlaşma)
en_kisa_mesafeler.append(iterasyon_en_iyi)
print("En kısa yol:", en_iyi_yol)
print("En kısa mesafe:", en_kisa_mesafe)

# Grafik çizimi
plt.plot(en_kisa_mesafeler)
plt.xlabel("İterasyon")
plt.ylabel("En Kısa Mesafe")
plt.title("Karınca Koloni Algoritması ile En Kısa Yol")
plt.show()
