1. Eksekusi Seluruh Profile

a. Edit file /etc/profile
Buka file /etc/profile menggunakan editor teks (seperti nano atau gedot/vim) dengan hak akses sudo, lalu tambahkan baris berikut di bagian akhir file:
echo "Profile dari /etc/profile"

b. Edit file profile user (Asumsi nama Anda stD02001)
Ganti /home/mahasiswa dengan direktori home Anda sendiri (misal /home/stD02001). Tambahkan instruksi echo di setiap file konfigurasi berikut:
•/home/stD02001/.bash_profile
echo "Profile dari .bash_profile"
•/home/stD02001/.bash_login
echo "Profile dari .bash_login"
•/home/stD02001/.profile
echo "Profile dari .profile"
•/home/stD02001/.bashrc
echo "Profile dari .bashrc"

c. Perbedaan su mahasiswa dan su - mahasiswa
su mahasiswa (Substitute User biasa): Berpindah user ke mahasiswa tetapi tetap menggunakan environment variable dan working directory dari user asal. File profil login (seperti .bash_profile atau .profile) tidak dieksekusi ulang.
su - mahasiswa (Login Shell): Berpindah user sekaligus memuat ulang seluruh environment variable dan profil login milik user mahasiswa (seolah-olah user tersebut baru saja melakukan login dari awal). File seperti /etc/profile, .bash_profile, dll., akan dieksekusi secara berurutan.

2. Prompt String (PS)

a. Mengganti prompt PS1
Edit file .bash_profile, lalu ubah dan export variabel PS1 agar dikenali oleh semua shell:  
PS1='> '
export PS1

b. Eksperimen hasil PS1
Masing-masing simbol escape backslash (\) pada PS1 merepresentasikan informasi sistem tertentu:  
PS1="\! > " \rightarrow Menampilkan nomor history perintah saat ini.  
PS1="\d > " \rightarrow Menampilkan tanggal hari ini (misal: Mon Sep 23).  
PS1="\t > " \rightarrow Menampilkan waktu saat ini dalam format 24-jam (HH:MM:SS).  
PS1="Saya=\u > " \rightarrow Menampilkan nama user yang sedang aktif (\u = username).  
PS1="\w > " \rightarrow Menampilkan direktori kerja saat ini secara penuh (absolute path).  
PS1="\h > " \rightarrow Menampilkan nama hostname komputer/server.  

3. Logout
Edit file .bash_logout di direktori home Anda dan tambahkan baris perintah berikut agar sistem menunggu 5 detik dan membersihkan layar sebelum sesi benar-benar tertutup:
Echo "Terima kasih atas sesi yang diberikan"
Sleep 5
clear

4. Bash Script

a. Isi ketiga script (p1.sh, p2.sh, p3.sh)
Buat tiga file terpisah dan berikan izin eksekusi (chmod +x p*.sh):  
•p1.sh:
#!/bin/bash
echo "Program p1"
ls -l
•p2.sh:
#!/bin/bash
echo "Program p2"
who
•p3.sh:
#!/bin/bash
echo "Program p3"
ps x

b. Cara menjalankan script dengan operator kontrol
./p1.sh ; ./p3.sh ; ./p2.sh \rightarrow Menjalankan perintah secara sekuensial (berurutan) satu demi satu, terlepas dari apakah perintah sebelumnya sukses atau gagal.  
./p1.sh & \rightarrow Menjalankan p1.sh di background secara asynchronous.  
./p1.sh $ ./p2.sh & ./p3.sh & \rightarrow Menjalankan p2.sh dan p3.sh di background, sementara p1.sh berjalan.  
(./p1.sh ; ./p3.sh ) & \rightarrow Menjalankan gabungan p1.sh dan p3.sh secara berurutan di dalam sebuah subshell di background.  

5. Jobs

a. Script pwaktu.sh
Buat file pwaktu.sh dengan isi sebagai berikut:  
#!/bin/bash
while [ true ]
do
    date >> hasil
    sleep 10
done

b. Menjalankan di Background
Gunakan perintah berikut untuk melihat dan menjalankan proses:  
jobs
find / -print > files 2>/dev/null &
jobs

c. Foreground dan Background (fg & bg)
Untuk menarik job nomor 1 ke foreground, lalu mengirimkannya kembali ke background menggunakan kombinasi tombol Ctrl + Z (^Z):  
fg %1
# (Tekan Ctrl + Z di keyboard)
bg

d. Menghentikan proses background dengan kill
Cek daftar proses beserta PID-nya, lalu hentikan menggunakan kill:  
ps x
kill [Nomor PID]

6. History

a. Mengubah HISTSIZE menjadi 20 dan melihat history:
HISTSIZE=20
h

b. Mengedit instruksi baris ke-5 dari instruksi terakhir:
! -5

c. Mengulang instruksi terakhir (atau navigasi ^P/^N):
!!

d. Mengulang instruksi pada nomor history 150:
!150

e. Mengulang instruksi berdasarkan awalan (prefix) tertentu:
!ls

!!
