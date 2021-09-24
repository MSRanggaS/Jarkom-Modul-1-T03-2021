# Jarkom-Modul-1-T03-2021

### 1. Sebutkan webserver yang digunakan pada "ichimarumaru.tech"! 
### 2. Temukan paket dari web-web yang menggunakan basic authentication method!
### 3. Ikuti perintah di basic.ichimarumaru.tech! Username dan password bisa didapatkan dari file .pcapng!
### 4. Temukan paket mysql yang mengandung perintah query select!
### 5. Login ke portal.ichimarumaru.tech kemudian ikuti perintahnya! Username dan password bisa didapat dari query insert pada table users dari file .pcap!

### 6. Cari username dan password ketika melakukan login ke FTP Server!
Command yang dieksekusi -> ftp.request.command == "USER" || ftp.request.command == "PASS"
![image](https://user-images.githubusercontent.com/61416036/134688183-1098465a-6bec-4978-84ce-f0ee9d7803fd.png)

### 7. Ada 500 file zip yang disimpan ke FTP Server dengan nama 0.zip, 1.zip, 2.zip, ..., 499.zip. Simpan dan Buka file pdf tersebut. (Hint = nama pdf-nya "Real.pdf")
Command yang dieksekusi -> frame contains Real.pdf
![image](https://user-images.githubusercontent.com/61416036/134688460-4074787d-d2f3-486c-a0cc-f538f07cc45f.png)

Kemudian follow TCP stream -> show data as RAW -> save as .pdf
![image](https://user-images.githubusercontent.com/61416036/134688580-df72b294-1768-4bae-a25b-2b88fafe62a7.png)

![image](https://user-images.githubusercontent.com/61416036/134688614-e6a0534b-eea9-40d1-8195-530c19dace68.png)

### 8. Cari paket yang menunjukan pengambilan file dari FTP tersebut!
Command yang dieksekusi -> ftp.request.command == RETR
![image](https://user-images.githubusercontent.com/61416036/134688737-7716d351-10ca-4fd7-9e4c-862ccf75be14.png)

### 9. Dari paket-paket yang menuju FTP terdapat inidkasi penyimpanan beberapa file. Salah satunya adalah sebuah file berisi data rahasia dengan nama "secret.zip". Simpan dan buka file tersebut!
Command yang dieksekusi -> ftp.request.command == “STOR”
![image](https://user-images.githubusercontent.com/61416036/134688803-4994506f-2fdd-4b2e-b36e-adf59682da09.png)

Follow TCP stream secret.zip 
![image](https://user-images.githubusercontent.com/61416036/134688982-b1ee9c28-c63f-42c8-8ee7-d3f68883b1bc.png)

ubah stream jadi 10 -> show data as RAW -> save as .zip
![image](https://user-images.githubusercontent.com/61416036/134689163-44423ad6-c297-4f4e-a8ee-de861b8905cf.png)

zip membutuhkan password
![image](https://user-images.githubusercontent.com/61416036/134689258-b26a01de-5188-45fb-b7f7-b9cc330084b5.png)

### 10. Selain itu terdapat "history.txt" yang kemungkinan berisi history bash server tersebut! Gunakan isi dari "history.txt" untuk menemukan password untuk membuka file rahasia yang ada di "secret.zip"!
Follow TCP stream history.txt -> ada clue yang mengatakan bahwa kunci ada di baris terakhir bukanapaapa.txt
![image](https://user-images.githubusercontent.com/61416036/134689395-ccd17762-0917-4b15-8592-491555d09456.png)

Follow TCP stream bukanapaapa.txt, muncul password zip nya
![image](https://user-images.githubusercontent.com/61416036/134689682-728e2e2d-8ade-4834-a719-e9c082480845.png)

setelah di extract file zip nya maka muncul file wanted.pdf
![image](https://user-images.githubusercontent.com/61416036/134689902-0d5db486-9ad5-4c81-9545-1e72e2d78545.png)

### 11. Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80! 
Mengisi Capture Filter dengan : `src port 80`
![image](https://user-images.githubusercontent.com/73152464/134682802-f37903a1-efef-4803-b211-f53cbbbd6728.png)

Berikut adalah hasil ketika wireshark hanya mengambil paket yang berasal dari port 80:
![image](https://user-images.githubusercontent.com/73152464/134683150-4ab5ade4-e271-4669-8495-1287887a818d.png)

### 12. Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!
Mengisi Capture Filter dengan : `port 21`
![image](https://user-images.githubusercontent.com/73152464/134683760-53fb8612-9c2e-4c97-a0e1-8db925238278.png)

Berikut adalah hasil ketika wireshark hanya mengambil paket yang mengandung port 21:
![image](https://user-images.githubusercontent.com/73152464/134683872-8e686604-f528-4cc5-af3c-bac5d9a90245.png)
Note: Kami tidak membuat FTP server sehingga hasilnya adalah tidak ada paket dari port 21

### 13. Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!
Mengisi Capture Filter dengan : `dst port 443`
![image](https://user-images.githubusercontent.com/73152464/134684131-efe9fd55-86ea-4b63-9e6a-c0df5715a0ff.png)

Berikut adalah hasil ketika wireshark hanya menampilkan paket yang menuju port 443:
![image](https://user-images.githubusercontent.com/73152464/134684255-5446c571-57dc-4903-8ea5-2e0181339caf.png)

### 14. Filter sehingga wireshark hanya mengambil paket yang tujuannya ke kemenag.go.id!
Pertama, kami membuka website kemenag.go.id terlebih dahulu
![image](https://user-images.githubusercontent.com/73152464/134684463-b627c81b-06c5-44b1-844a-f8f4d351c51e.png)

Kedua, kami mengisi Capture Filter dengan : `host kemenag.go.id`
![image](https://user-images.githubusercontent.com/73152464/134684424-f98e912c-e4ab-4197-b9ad-1ecd2225364c.png)

Berikut adalah tampilan dari wireshark yang mengambil paket dengan tujuan kemenag.go.id:
![image](https://user-images.githubusercontent.com/73152464/134684633-d8c8a926-71e4-4419-abdc-131a4c11f07a.png)

### 15. Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!
Pertama, kami mencari ip komputer kami dengan membuka Command Prompt lalu mengetikkan ipconfig:
![image](https://user-images.githubusercontent.com/73152464/134684946-593e1fc1-f682-470b-871a-0cde2ac38af0.png)

Kedua, kami mengisi Capture Filter dengan : `src host 10.148.151.45`
![image](https://user-images.githubusercontent.com/73152464/134685263-d96cfce3-fbab-4f04-9a77-53c47e7f60e6.png)

Berikut adalah tampilan dari wireshark yang hanya mengambil paket dyang berasal dari IP kami:
![image](https://user-images.githubusercontent.com/73152464/134685299-4de13c22-f0e1-4afd-ae6d-22802d13e70d.png)
