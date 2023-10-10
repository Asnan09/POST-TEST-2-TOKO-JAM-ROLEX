# POST-TEST-2-TOKO-JAM-ROLEX

```
#Nama  : Asnan Fadjri Wahyudi
#Nim   : 2309116094
#Kelas : Sistem informasi


import random
import string
from prettytable import PrettyTable  

class JamRolex:
    def __init__(self, nama, model, harga, stok):
        self.nama = nama
        self.model = model
        self.harga = harga
        self.stok = stok

    def tampilkan_informasi(self):
        print(f"Nama: {self.nama}")
        print(f"Model: {self.model}")
        print(f"Harga: ${self.harga}")
        print(f"Stok Tersedia: {self.stok}")

class TokoJamRolex:
    def __init__(self):
        self.daftar_jam = []

    def tambah_jam(self, jam):
        self.daftar_jam.append(jam)
        print(f"Jam {jam.nama} ({jam.model}) telah ditambahkan ke stok.")

    def hapus_jam(self, nama):
        for jam in self.daftar_jam:
            if jam.nama == nama:
                self.daftar_jam.remove(jam)
                print(f"Jam {nama} ({jam.model}) telah dihapus dari stok.")
                return
        print(f"Jam dengan nama {nama} tidak ditemukan dalam stok.")

    def ubah_harga(self, nama, harga_baru):
        for jam in self.daftar_jam:
            if jam.nama == nama:
                jam.harga = harga_baru
                print(f"Harga jam {nama} telah diubah menjadi ${harga_baru}.")
                return
        print(f"Jam dengan nama {nama} tidak ditemukan dalam stok.")

    def tampilkan_daftar_jam(self):
        table = PrettyTable()
        table.field_names = ["No", "Nama", "Model", "Harga", "Stok"]
        for i, jam in enumerate(self.daftar_jam, start=1):
            table.add_row([i, jam.nama, jam.model, f"${jam.harga}", jam.stok])
        print(table)

def generate_random_name(length=8):
    letters = string.ascii_lowercase
    return ''.join(random.choice(letters) for _ in range(length))

def menu_admin(toko):
    while True:
        print(32*'=')
        print("Menu Admin:")
        print(32*'=')
        print("Pilih opsi:")
        print("1. Tambahkan Jam ke Stok")
        print("2. Hapus Jam dari Stok")
        print("3. Ubah Harga Jam")
        print("4. Lihat Daftar Jam")
        print("5. Keluar")
        print(32*'=')

        pilihan = input("Masukkan nomor pilihan: ")

        if pilihan == "1":
            nama = generate_random_name()
            model = input("Masukkan model jam: ")
            harga = float(input("Masukkan harga jam: $"))
            stok = int(input("Masukkan jumlah stok: "))
            jam_baru = JamRolex(nama, model, harga, stok)
            toko.tambah_jam(jam_baru)
        elif pilihan == "2":
            nama = input("Masukkan nama jam yang ingin dihapus: ")
            toko.hapus_jam(nama)
        elif pilihan == "3":
            nama = input("Masukkan nama jam yang harga ingin diubah: ")
            harga_baru = float(input("Masukkan harga baru: $"))
            toko.ubah_harga(nama, harga_baru)
        elif pilihan == "4":
            toko.tampilkan_daftar_jam()
        elif pilihan == "5":
            print("Keluar dari menu admin.")
            break
        else:
            print("Pilihan tidak valid. Silakan masukkan nomor yang benar.")

def menu_pembeli(toko):
    while True:
        print(32*'=')
        print("Menu Pembeli:")
        print(32*'=')
        print("Pilih opsi:")
        print("1. Lihat Daftar Harga dan Model")
        print("2. Beli Jam")
        print("3. Keluar")
        print(32*'=')

        pilihan = input("Masukkan nomor pilihan: ")

        if pilihan == "1":
            toko.tampilkan_daftar_jam()
        elif pilihan == "2":
            nama = input("Masukkan nama jam yang ingin Anda beli: ")
            jumlah = int(input("Masukkan jumlah jam yang ingin Anda beli: "))
            beli_jam(nama, jumlah, toko)
        elif pilihan == "3":
            print("Keluar dari menu pembeli.")
            break
        else:
            print("Pilihan tidak valid. Silakan masukkan nomor yang benar.")

def beli_jam(nama, jumlah, toko):
    for jam in toko.daftar_jam:
        if jam.nama == nama:
            if jam.stok >= jumlah:
                total_harga = jam.harga * jumlah
                print(f"Anda telah membeli {jumlah} {jam.model} dengan total harga ${total_harga} Terima Kasih telah berbelanja di Toko kami2")
                jam.stok -= jumlah
            else:
                print(f"Stok {jam.model} tidak mencukupi.")
            return
    print(f"Jam dengan nama {nama} tidak ditemukan dalam stok.")

if __name__ == "__main__":
    toko = TokoJamRolex()

    # nama-nama jam rolex dan model besertaharga
    jam1 = JamRolex("Air King", "Air king A", 5000, 2)
    jam2 = JamRolex("GMT Master II", "GMT Master II Model B", 8000, 2)
    jam3 = JamRolex("Lady Datejust", "Lady Datejust Model C", 10000, 2)
    jam4 = JamRolex("Oyster Perpetual", "Oyster Perpetual Model D", 3500, 2)
    jam5 = JamRolex("Day Date", "Day Date Model E", 9000, 2)


    toko.daftar_jam.extend([jam1, jam2, jam3, jam4, jam5])

    # menu awal login di toko jam rolex
    while True:
        print(32*'=')
        print("Selamat datang di Toko Jam Rolex")
        print(32*'=')
        print("Pilih Login:")
        print("1. Admin")
        print("2. Pembeli")
        print("3. Keluar")
        print(32*'=')
        peran = input("Anda sebagai apa: ")

        if peran == "1":
            password_admin = "cumabisaliatkmdarijauh"  # kata sandi admin jika ingin login sebagai admin
            login_admin = input("Masukkan kata sandi admin: ")
            if login_admin == password_admin:
                menu_admin(toko)
            else:
                print("Kata sandi admin salah.")
        elif peran == "2":
            menu_pembeli(toko)
        elif peran == "3":
            print("Terima kasih telah berkunjung ke Toko Jam Rolex kami.")
            break
        else:
            print("Peran tidak valid. Silakan masukkan nomor yang benar.")

```

![1](https://github.com/Asnan09/POST-TEST-2-TOKO-JAM-ROLEX/assets/146003481/9d3a781d-e090-4bda-b3cb-0557870749b0)

![2](https://github.com/Asnan09/POST-TEST-2-TOKO-JAM-ROLEX/assets/146003481/c71e38bb-4a02-4337-b769-ad7cfcf8d334)

![3](https://github.com/Asnan09/POST-TEST-2-TOKO-JAM-ROLEX/assets/146003481/12179273-0782-4d89-ac0f-00445eb77945)

![4](https://github.com/Asnan09/POST-TEST-2-TOKO-JAM-ROLEX/assets/146003481/4683fc4c-0187-4842-942e-7b7c39ef0194)

![5](https://github.com/Asnan09/POST-TEST-2-TOKO-JAM-ROLEX/assets/146003481/fb53b08f-b6d8-4c9b-818c-1bae6525da41)

![Diagram Tanpa Judul drawio](https://github.com/Asnan09/POST-TEST-2-TOKO-JAM-ROLEX/assets/146003481/edd80e23-3223-485e-8212-185471e5296a)






