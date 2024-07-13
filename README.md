Projek UAS Pengolahan Citra

Proyek pengolahan citra yang Anda kerjakan berkaitan dengan segmentasi warna menggunakan teknik pemrosesan gambar. Berikut beberapa teori dan konsep yang mendukung:

1. Pemrosesan Citra Digital (Digital Image Processing)

Pemrosesan citra digital melibatkan manipulasi dan analisis citra menggunakan komputer untuk meningkatkan kualitas gambar, mengekstraksi informasi, atau mengubah gambar ke format yang lebih sesuai untuk aplikasi tertentu. Beberapa langkah umum dalam pemrosesan citra termasuk peningkatan citra (image enhancement), restorasi citra (image restoration), segmentasi citra (image segmentation), dan pengenalan objek (object recognition).

2. Ruang Warna (Color Spaces)

Ruang warna adalah model matematis yang mendeskripsikan cara warna dapat direpresentasikan sebagai kombinasi angka. Ada beberapa ruang warna yang digunakan dalam pemrosesan citra:

- RGB (Red, Green, Blue)**: Ruang warna dasar yang digunakan dalam tampilan digital.
- HSV (Hue, Saturation, Value)**: Ruang warna yang sering digunakan untuk segmentasi warna karena mendekati cara manusia melihat warna. Dalam ruang warna HSV:
  - Hue mewakili jenis warna.
  - Saturation mewakili intensitas atau kejenuhan warna.
  - Value mewakili kecerahan warna.

3. Segmentasi Citra (Image Segmentation)

Segmentasi citra adalah proses mempartisi citra menjadi beberapa bagian atau objek yang berbeda. Ini adalah langkah penting dalam banyak aplikasi pengenalan pola dan analisis citra. Salah satu teknik segmentasi yang sering digunakan adalah thresholding, di mana piksel dalam citra diklasifikasikan berdasarkan intensitas atau warna.

- Thresholding: Teknik segmentasi di mana piksel dalam citra diubah menjadi biner berdasarkan ambang batas tertentu. Dalam segmentasi warna, thresholding diterapkan pada ruang warna tertentu (seperti HSV) untuk mengisolasi objek berdasarkan warna.

4. Operasi Morfologi (Morphological Operations)

Operasi morfologi digunakan untuk memproses struktur bentuk objek dalam citra biner. Operasi ini berguna untuk membersihkan noise dan menghubungkan komponen terpisah dalam citra.

- Erosi (Erosion): Menghilangkan piksel tepi objek.
- Dilatasi (Dilation): Menambahkan piksel ke tepi objek.
- Morfologi Penutupan (Closing): Kombinasi dilatasi diikuti oleh erosi, digunakan untuk mengisi lubang kecil.
- Morfologi Pembukaan (Opening): Kombinasi erosi diikuti oleh dilatasi, digunakan untuk menghapus noise kecil.

5. Bitwise Operations

Operasi bitwise digunakan untuk memanipulasi gambar pada tingkat bit. Dalam konteks pengolahan citra, operasi bitwise seperti `cv2.bitwise_and()` digunakan untuk menggabungkan dua citra atau sebuah citra dengan mask untuk mengekstrak bagian tertentu dari citra.

Implementasi dalam Proyek Anda

1. Memuat dan Mengonversi Gambar:
   - Gambar dimuat menggunakan OpenCV dan dikonversi ke ruang warna HSV untuk memudahkan segmentasi warna.

2. Mendefinisikan Rentang Warna:
   - Rentang warna untuk kuning dan hijau didefinisikan dalam ruang warna HSV untuk mengisolasi buah nanas dan daunnya.

3. Membuat Mask:
   - Mask dibuat menggunakan teknik thresholding untuk mengekstrak piksel yang berada dalam rentang warna yang ditentukan.

4. Operasi Bitwise:
   - Operasi bitwise digunakan untuk menggabungkan mask dengan gambar asli sehingga hanya bagian yang diinginkan yang ditampilkan.

5. Operasi Morfologi:
   - Operasi morfologi digunakan untuk membersihkan mask dari noise kecil dan menghubungkan komponen terpisah.

6. Menampilkan Hasil:
   - Hasil ditampilkan menggunakan Matplotlib untuk visualisasi yang lebih baik.

Aplikasi Praktis

Segmentasi warna dan pembuatan mask seperti yang dilakukan dalam proyek Anda memiliki banyak aplikasi praktis, termasuk:

- Pengenalan Objek: Mengidentifikasi dan mengisolasi objek tertentu dalam gambar berdasarkan warna.
- Pendeteksian Buah: Dalam industri pertanian, digunakan untuk mendeteksi dan menghitung buah pada tanaman.
- Sistem Penglihatan Robotik: Membantu robot dalam mengenali dan memanipulasi objek berdasarkan warna.
- Analisis Gambar Medis: Mengisolasi area tertentu dalam citra medis untuk analisis lebih lanjut.

Dengan memahami teori-teori ini, Anda dapat lebih baik mengaplikasikan teknik-teknik tersebut dalam proyek pengolahan citra Anda dan mengembangkan solusi yang lebih efektif.





**Tahapan-Tahapan** : 
Berikut penjelasan kode yang Anda tulis untuk pengolahan citra menggunakan OpenCV dan Matplotlib:

### Penjelasan Kode:

```python
# Load image
img = cv2.imread("nanass.jpg")
```
- **Memuat gambar**: Gambar dengan nama "nanass.jpg" dibaca dan disimpan dalam variabel `img` menggunakan OpenCV.

```python
# Convert to HSV
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- **Konversi ke format HSV**: Gambar yang dimuat dikonversi dari format BGR (standar OpenCV) ke format HSV untuk memudahkan segmentasi warna.

```python
# Define range of yellow color in HSV
lower_yellow = np.array([20, 100, 100])
upper_yellow = np.array([30, 255, 255])
```
- **Menentukan rentang warna kuning dalam format HSV**: Rentang warna kuning didefinisikan dengan nilai minimum `lower_yellow` dan nilai maksimum `upper_yellow`.

```python
# Threshold the HSV image to get only yellow colors
mask_yellow = cv2.inRange(hsv, lower_yellow, upper_yellow)
```
- **Thresholding untuk mendapatkan warna kuning**: `cv2.inRange` digunakan untuk membuat mask yang hanya berisi piksel yang berada dalam rentang warna kuning yang telah ditentukan.

```python
# Bitwise-AND mask and original image for yellow
res_yellow = cv2.bitwise_and(img, img, mask=mask_yellow)
```
- **Menggabungkan mask dengan gambar asli untuk warna kuning**: `cv2.bitwise_and` digunakan untuk menggabungkan mask kuning dengan gambar asli sehingga hanya bagian yang berwarna kuning yang ditampilkan.

```python
# Define range of green color in HSV
lower_green = np.array([35, 50, 50])
upper_green = np.array([85, 255, 255])
```
- **Menentukan rentang warna hijau dalam format HSV**: Rentang warna hijau didefinisikan dengan nilai minimum `lower_green` dan nilai maksimum `upper_green`.

```python
# Threshold the HSV image to get only green colors
mask_green = cv2.inRange(hsv, lower_green, upper_green)
```
- **Thresholding untuk mendapatkan warna hijau**: `cv2.inRange` digunakan untuk membuat mask yang hanya berisi piksel yang berada dalam rentang warna hijau yang telah ditentukan.

```python
# Bitwise-AND mask and original image for green
res_green = cv2.bitwise_and(img, img, mask=mask_green)
```
- **Menggabungkan mask dengan gambar asli untuk warna hijau**: `cv2.bitwise_and` digunakan untuk menggabungkan mask hijau dengan gambar asli sehingga hanya bagian yang berwarna hijau yang ditampilkan.

```python
# Convert the yellow result to grayscale
gray = cv2.cvtColor(res_yellow, cv2.COLOR_BGR2GRAY)
```
- **Konversi hasil warna kuning ke grayscale**: Hasil citra warna kuning `res_yellow` dikonversi ke format grayscale.

```python
# Set non-masked pixels to white (255)
gray[gray != 0] = 255
```
- **Mengatur piksel non-mask menjadi putih**: Semua piksel yang tidak di-mask (bernilai bukan 0) diatur menjadi putih (255) pada citra grayscale.

```python
# Create a 2x2 subplot
plt.figure(figsize=(12, 12))

# Original Image
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Citra Asli')
plt.axis('on')

# White Mask
plt.subplot(2, 2, 2)
plt.imshow(gray, cmap='gray')
plt.title('Mask Buah Nanas (Putih)')
plt.axis('on')

# Yellow Pineapple
plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(res_yellow, cv2.COLOR_BGR2RGB))
plt.title('Tampilan Nanas (Kuning)')
plt.axis('on')

# Green Leaves
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(res_green, cv2.COLOR_BGR2RGB))
plt.title('Tampilan Daun (Hijau)')
plt.axis('on')

plt.show()
```
- **Membuat subplot 2x2 dan menampilkan gambar**:
  - Subplot 1: Menampilkan gambar asli.
  - Subplot 2: Menampilkan mask putih untuk buah nanas.
  - Subplot 3: Menampilkan hasil segmentasi warna kuning untuk nanas.
  - Subplot 4: Menampilkan hasil segmentasi warna hijau untuk daun nanas.
- `plt.imshow()` digunakan untuk menampilkan gambar pada setiap subplot, dan `plt.show()` digunakan untuk menampilkan semua subplot yang telah dibuat.

**Kesimpulan**
Kode ini memproses gambar "nanass.jpg" untuk membuat mask yang mengisolasi warna kuning (buah nanas) dan hijau (daun nanas), serta menampilkan hasilnya dalam beberapa subplot menggunakan Matplotlib. Mask putih juga dibuat dari hasil segmentasi warna kuning untuk memperlihatkan area buah nanas secara lebih jelas.
