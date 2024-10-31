# Mini-Project-Android
Mini Project KSM Android


Ini adalah program aplikasi Manajemen RS Sederhana. Di sini, kita bisa menyimpan data pasien dan juga data karyawan RS, seperti dokter yang praktik dan juga suster atau perawat yang berjaga. Mini project ini dibangun dengan NodeJS dan dites API-nya menggunakan Postman. Selamat mencoba! []~(￣▽￣)~*

1. **Menggunakan Program**

Untuk menggunakan program, install project dan eksekusi
```sh
npm install
```
Untuk package.json, pastikan **tidak** menggunakan ```type:module```

2. **Format Data <br>**
<p>Untuk format data, pasien dan karyawan memiliki data yang berbeda, meskipun ada beberapa yang sama. Berikut adalah data dan formatnya: </p>
a. Pasien

| field   | tipe | keterangan |
|-|-|-|
|id |string |id unik pengidentifikasi pasien |
|nama |string |nama pasien |
|jenis_kelamin |string |jenis kelamin pasien |
|umur |int |umur pasien |
|alamat |string |alamat tempat tinggal pasien |
|telepon |string |nomor telepon pasien yang bisa dihubungi |
|riwayat |string |penyakit yang diderita pasien |
|asuransi |string |asuransi kesehatan yang dimiliki pasien |
|alergi |string |alergi yang diidap pasien |
|golongan_darah|string |golongan darah pasien |

b. Karyawan (Dokter dan Perawat)
| field   | tipe | keterangan |
|-|-|-|
|id |string |id unik pengidentifikasi dokter/perawat <br>•id dokter Dx <br>•id perawat Nx |
|nama |string |nama karyawan |
|keahlian |string |bidang keahlian atau spesialisasi karyawan |
|lama_mengabdi |int |pengalaman berapa lama tahun karyawan sudah mengabdi |
|jenis_kelamin |string |jenis kelamin karyawan |
|umur |int |umur karyawan | 

3. **Ketentuan API:**
### 1. CREATE (Menambahkan Data Pasien atau Karyaawan)

a. Pasien
- **Endpoint**: `/pasien`
- **Method**: `POST`
- **Body Request**:
    ```json
    {
    "nama": "string",
    "jenis_kelamin": "string",
    "umur": int,
    "alamat": "string",
    "telepon": "string",
    "riwayat": "string",
    "asuransi": "string",
    "alergi": "string",
    "golongan_darah": "string"
    },
    ```
- **Response**:
    - **Sukses**:
        - Status: `201 Created`
        - Pesan: `"Pasien berhasil ditambahkan!"`
        - Data:
        ```json
        "pasien": {
          "id": "string",
          "nama": "string",
          "jenis_kelamin": "string",
          "umur": int,
          "alamat": "string",
          "telepon": "string",
          "riwayat": "string",
          "asuransi": "string",
          "alergi": "string",
          "golongan_darah": "string"
      }
        ```
    - **Gagal**:

      ***Salah penulisan sintaks dan atribut***:
        - Status: `400 Bad Request`
        - Pesan: `"Semua atribut pasien harus diisi! Pastikan juga umur diisi dengan angka yang valid."`
     
      ***Input umur bukan bilangan bulat, tetapi string***:
        - Status: `400 Bad Request`
        - Pesan: `"Umur harus berupa angka yang valid!"`

b. Karyawan
- **Endpoint**: `/karyawan/dokter` atau `/karyawan/perawat`
- **Method**: `POST`
- **Body Request**:
    ```json
    {
    "id": "string",
    "nama": "string",
    "keahlian": "string",
    "lama_mengabdi": int,
    "jenis_kelamin": "string",
    "umur": int
  },
    ```
- **Response**:
    - **Sukses**:
        - Status: `201 Created`
        - Pesan: `"Dokter berhasil ditambahkan!"` atau `"Perawat berhasil ditambahkan!"`
        - Data:
        ```json
        "dokter": {
          "id": "string",
          "nama": "string",
          "keahlian": "string",
          "lama_mengabdi": int,
          "jenis_kelamin": "string",
          "umur": int
      }
        ```
        atau
      ```json
      "perawat": {
        "id": "string",
        "nama": "string",
        "keahlian": "string",
        "lama_mengabdi": int,
        "jenis_kelamin": "string",
        "umur": int
      }
      ```
    - **Gagal**:

      ***Salah penulisan sintaks dan atribut***:
      - Status: `400 Bad Request`
      - Pesan: `"Semua atribut dokter harus diisi! Cek kemungkinan salah penulisan atribut!"` atau `"Semua atribut perawat harus diisi! Cek kemungkinan salah penulisan atribut!"`
     
      ***ID sudah digunakan***:
      - Status: `400 Bad Request`
      - Pesan: `"ID sudah digunakan! Mohon gunakan ID yang berbeda."`
     
### 2. READ (Melihat Data Pasien, Karyawan, atau Perawat)

a. Semuanya
- **Endpoint**: `/`
- **Method**: `GET`
- **Response**:
    - **Ada Data**:
        - Status: `200 OK`
        - Data:
        ```json
        {
        "pasien": [
            {
                "id": "string",
                "nama": "string",
                "jenis_kelamin": "string",
                "umur": int,
                "alamat": "string",
                "telepon": "string",
                "riwayat": "string",
                "asuransi": "string",
                "alergi": "string",
                "golongan_darah": "string"
            }
          ],
          "dokter": [
            {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
            }
          ],
          "karyawan": [
            {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
            }
          ]
        }
    - **Tidak Ada Data**:
        - Status: `200 OK`
        - Data:
        ```json
        {
          "pasien": [],
          "karyawan": []
        }

b. Pasien (Semua, By Id, By Gender)
- **Endpoint**: `/pasien` atau `/pasien/:id` atau `/pasien/gender/:jenis_kelamin`
- **Method**: `GET`
- **Response**:
    - **Ada Data**:
        - Status: `200 OK`
        - Pesan: `-` atau `"Pasien ditemukan!"` atau `"Data pasien dengan jenis kelamin laki-laki berhasil ditampilkan!"` atau `"Data pasien dengan jenis kelamin perempuan berhasil ditampilkan!"`
        - Data:
        ```json
        {
        "pasien": [
            {
                "id": "string",
                "nama": "string",
                "jenis_kelamin": "string",
                "umur": int,
                "alamat": "string",
                "telepon": "string",
                "riwayat": "string",
                "asuransi": "string",
                "alergi": "string",
                "golongan_darah": "string"
            }
          ]
        }
    - **Tidak Ada Data**:
        - Status: `404 Not Found`
        - Pesan: `"Tidak ada pasien yang terdaftar."` atau `"Pasien tidak ditemukan"`

c. Semua Karyawan
- **Endpoint**: `/karyawan` atau 
- **Method**: `GET`
- **Response**:
    - **Ada Data**:
        - Status: `200 OK`
        - Data:
        ```json
        {
        "karyawan": [
            {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
            }
          ]
        }
    - **Tidak Ada Data**:
        - Status: `404 Not Found`
        - Pesan: `"Tidak ada karyawan yang terdaftar."`

d. Dokter atau Perawat (Dokter saja, Perawat saja, By Id)
- **Endpoint**: `/karyawan/dokter` atau `/karyawan/perawat` atau `/karyawan/:id`
- **Method**: `GET`
- **Response**:
    - **Ada Data**:
        - Status: `200 OK`
        - PesanL `-` atau `-` atau `"Dokter ditemukan!"` atau `"Perawat ditemukan!"`
        - Data:
        ```json
        {
        "dokter": [
            {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
            }
          ]
        }
        ```
        atau
        ```json
        {
        "perawat": [
            {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
            }
          ]
        }
        ```
  
    - **Tidak Ada Data**:
        - Status: `404 Not Found`
        - Pesan: `"Tidak ada karyawan yang terdaftar."` atau `"Tidak ada dokter yang terdaftar."` atau `"Tidak ada perawat yang terdaftar."`
     
### 3. UPDATE (Mengubah Data Pasien atau Karyawan)

a. Pasien
- **Endpoint**: `/pasien/:id`
- **Method**: `PUT`
- **Body Request**:
    ```json
        "pasien": {
          "id": "string",
          "nama": "string",
          "jenis_kelamin": "string",
          "umur": int,
          "alamat": "string",
          "telepon": "string",
          "riwayat": "string",
          "asuransi": "string",
          "alergi": "string",
          "golongan_darah": "string"
      }
    ```
- **Response**:
    - **Berhasil**:
        - Status: `200 OK`
        - Pesan: `"Data pasien berhasil diperbarui!"`
        - Data:
          ```json
                "pasien": {
                "id": "string",
                "nama": "string",
                "jenis_kelamin": "string",
                "umur": int,
                "alamat": "string",
                "telepon": "string",
                "riwayat": "string",
                "asuransi": "string",
                "alergi": "string",
                "golongan_darah": "string"
                }
          ```
    - **Gagal**:
  
      ***Pasien tidak ditemukan***:
        - Status: `404 Not Found`
        - Pesan: `"Pasien tidak ditemukan"`
  
      ***Ada kesalahan penulisan***:
        - Status: `400 Bad Request`
        - Pesan: `"Atribut tidak valid: :${atribut yang salah ketik}"`
     
b. Karyawan (Dokter atau Perawat)
- **Endpoint**: `/karyawan/dokter/:id` atau `/karyawan/perawat:id`
- **Method**: `PUT`
- **Response**:

    - **Berhasil**:
        - Status: `200 OK`
        - Pesan: `"Data dokter berhasil diperbarui!"` atau `"Data perawat berhasil diperbarui!"`
        - Data:
          ```json
                "dokter": {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
          }
          ```
          atau
          ```json
                "perawat": {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
          }
          ```
      - **Gagal**:
  
      ***Karyawan tidak ditemukan***
        - Status: `404 Not Found`
        - Pesan: `"Dokter tidak ditemukan!"` atau `"Perawat tidak ditemukan!"`
      
       ***Ada kesalahan penulisan***
        - Status: `400 Bad Request`
        - Pesan: `"Atribut tidak valid: :${atribut yang salah ketik}"`

### 4. DELETE (Menghapus Data Pasien atau Karyawan)

a. Pasien
- **Endpoint**: `/pasien/:id`
- **Method**: `DELETE`
- **Response**:
    - **Berhasil**:
        - Status: `200 OK`
        - Pesan: `"Pasien berhasil dihapus!"`
        - Data:
          ```json
                "pasien": {
                "id": "string",
                "nama": "string",
                "jenis_kelamin": "string",
                "umur": int,
                "alamat": "string",
                "telepon": "string",
                "riwayat": "string",
                "asuransi": "string",
                "alergi": "string",
                "golongan_darah": "string"
                }
          ```
      - **Gagal**:
  
      ***Karyawan tidak ditemukan***
        - Status: `404 Not Found`
        - Pesan: `"Pasien tidak ditemukan!"`

b. Karyawan
- **Endpoint**: `/karyawan/dokter/:id` atau `/karyawan/perawat:id`
- **Method**: `DELETE`
- **Response**:
    - **Berhasil**:
        - Status: `200 OK`
        - Pesan: `Dokter berhasil dihapus!"` atau `"Perawat berhasil dihapus!"`
        - Data:
          ```json
                "dokter": {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
          }
          ```
          atau
          ```json
                "perawat": {
                "id": "string",
                "nama": "string",
                "keahlian": "string",
                "lama_mengabdi": int,
                "jenis_kelamin": "string",
                "umur": int
          }
          ```   
      - **Gagal**:
  
      ***Karyawan tidak ditemukan***
        - Status: `404 Not Found`
        - Pesan: `Dokter tidak ditemukan!` atau `Perawat tidak ditemukan!`

