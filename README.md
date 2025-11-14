
# list untuk menyimpan data nilai siswa
data_nilai_siswa = []

def tampilan_menu():
    print("\n===Menu Pilihan===")
    print("1. Tambah Data Nilai Siswa")
    print("2. Tampilkan Data Nilai Siswa")
    print("3. cari siswa berdasarkan kriteria")
    print("4. hapus data nilai siswa")
    print("5. ubah data siswa")
    print("6. peringkat siswa")
    print("7. Keluar")

def hitung_grade(nilai_rata_rata):
    if nilai_rata_rata >= 85:
        return "A"
    elif nilai_rata_rata >= 75:
        return "B"
    elif nilai_rata_rata >= 65:
        return "C"
    elif nilai_rata_rata >= 55:
        return "D"
    else:
        return "E"
    
def validasi_menu(isi):
    while True:
        pilihan = input(isi).strip().lower()
        if pilihan.lower() == 'exit':
            return None
        try:
            pilihan = int(pilihan)
            if 1 <= pilihan <= 7:
                return pilihan
            print("pilihan anda salah, silahkan coba lagi!")
        except ValueError:
            print("input yang anda masukkan salah, silahkan coba lagi!")

def tambah_data_nilai_siswa():
    while True:
        nama = input("Masukkan Nama Siswa: ").strip().title()
        nilai_ipa = int(input("Masukkan Nilai IPA: "))
        nilai_ips = int(input("Masukkan Nilai IPS: "))
        nilai_mtk = int(input("Masukkan Nilai Matematika: "))
        nilai_binggris = int(input("Masukkan Nilai Bahasa Inggris: "))
        nilai_bindonesia = int(input("Masukkan Nilai Bahasa Indonesia: "))
        nilai_rata_rata = (nilai_ipa + nilai_ips + nilai_mtk + nilai_binggris + nilai_bindonesia) / 5
        grade = hitung_grade(nilai_rata_rata)
        data_nilai_siswa.append({"nama": nama, "nilai": nilai_rata_rata, "grade": grade})
        print("\nData nilai", nama, "berhasil ditambahkan!")
        tambah_lagi = input("\nApakah ingin menamah data nilai siswa lagi? (ya/tidak): ").strip().lower()
        if tambah_lagi not in ["ya", "y"]:
            break

def lihat_data_nilai_siswa():
    if not data_nilai_siswa:
        print("\nData nilai siswa masih kosong!")
    else:
        print("\n===Data Nilai Siswa===")
        for i, siswa in enumerate(data_nilai_siswa, start=1):
            print(i, siswa['nama'], "- Nilai :", siswa['nilai'], siswa['grade'])

def cari_siswa():
    if not data_nilai_siswa:
        print("\nData nilai siswa masih kosong!")
    else:
        print("\n===Data Nilai Siswa===")
        print("1. Cari siswa berdasarkan nilai diatas rata-rata")
        print("2. Cari siswa berdasarkan nilai dibawah rata-rata")
        while True:
            pilihan = validasi_menu("masukkan pilihan: ")
            if pilihan == None:
                return
            if pilihan == 1:
                hasil = [siswa for siswa in data_nilai_siswa if siswa['nilai'] > 85]
                break
            elif pilihan == 2:
                hasil = [siswa for siswa in data_nilai_siswa if siswa['nilai'] < 85]
                break
            else:
                print("input yang anda masukkan salah! silahkan coba lagi.")
        if hasil:
            print("\n===Data Nilai Siswa===")
            for i, siswa in enumerate(hasil, start=1):
                print(i, siswa['nama'], "- Nilai :", siswa['nilai'], siswa['grade'])

def hapus_data_nilai_siswa():
    if not data_nilai_siswa:
        print("\nTidak ada data nilai siswa yang bisa dihapus!")
    else:
        lihat_data_nilai_siswa()
        while True:
            indeks = validasi_menu("\nMasukkan nomor siswa yang akan dihapus: ")
            if indeks == None:
                return
            if 0 <= indeks < len(data_nilai_siswa):
                siswa_dihapus = data_nilai_siswa.pop(indeks)
                print("data nilai siswa", siswa_dihapus['nama'], "berhasil dihapus!")
            else:
                print("Data nilai siswa tidak ditemukan!")

def ubah_data():
    if not data_nilai_siswa:
        print("\nData nilai siswa masih kosong!")
    else:
        lihat_data_nilai_siswa()
        indeks = validasi_menu("\nMasukkan nomor siswa yang akan diubah: ")
        if indeks == None:
            return
        if 0 <= indeks < len(data_nilai_siswa):
            nama = input("Masukkan Nama Siswa: ").strip().title()
            nilai_ipa = int(input("Masukkan Nilai IPA: "))
            nilai_ips = int(input("Masukkan Nilai IPS: "))
            nilai_mtk = int(input("Masukkan Nilai Matematika: "))
            nilai_binggris = int(input("Masukkan Nilai Bahasa Inggris: "))
            nilai_bindonesia = int(input("Masukkan Nilai Bahasa Indonesia: "))

            nilai_rata_rata = (nilai_ipa + nilai_ips + nilai_mtk + nilai_binggris + nilai_bindonesia) / 5
            grade = hitung_grade(nilai_rata_rata)

            data_nilai_siswa[indeks] = {"nama": nama, "nilai": nilai_rata_rata, "grade":grade}
            print("\nData nilai", nama, "Berhasil diubah!")
        else:
            print("Data nilai siswa tidak ditemukan!")
    
def peringkat_siswa():
    if not data_nilai_siswa:
        print("\nData nilai siswa masih kosong!")
    else:
        data_nilai_siswa_sorted = sorted(data_nilai_siswa, key=lambda x: x['nilai'], reverse=True) 
        print("\n===Peringkat Siswa===")
        for i, siswa in enumerate(data_nilai_siswa_sorted, start=1):
            print(i, siswa['nama'], "- Nilai :", siswa['nilai'], siswa['grade'])

while True:
    tampilan_menu()
    pilihan = int(input("Masukan pilihan : "))
    if pilihan == None:
        continue
    elif pilihan == 1:
        tambah_data_nilai_siswa()
    elif pilihan == 2:
        lihat_data_nilai_siswa()
    elif pilihan == 3:
        cari_siswa()
    elif pilihan == 4:
        hapus_data_nilai_siswa()
    elif pilihan == 5:
        ubah_data()
    elif pilihan == 6:
        peringkat_siswa()
    elif pilihan == 7:
        print("Keluar dari aplikasi. Semoga hari anda menyenangkan, Terimakasih!")
        break
    else:
        print("Input yang anda masukkan salah! Silahkan coba lagi.")
