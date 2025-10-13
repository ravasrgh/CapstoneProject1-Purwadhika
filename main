"""
CAPSTONE PROJECT MODULE 1 - PURWADHIKA
Sistem Manajemen Data Karyawan Perusahaan
Dibuat oleh: Rava Khoman Tuah Saragih
JCDSAHSR-004

Deskripsi Program:
Program ini adalah aplikasi manajemen data karyawan yang memiliki fitur CRUD lengkap
(Create, Read, Update, Delete) dengan validasi input yang ketat dan fitur tambahan
seperti export ke CSV, filter data, dan statistik karyawan.

Fitur Utama:
1. CREATE - Menambah data karyawan baru dengan validasi lengkap
2. READ - Menampilkan data dengan berbagai filter dan sorting
3. UPDATE - Mengubah data karyawan yang sudah ada
4. DELETE - Menghapus data karyawan dengan backup otomatis
5. EXPORT - Menyimpan data ke file CSV
6. STATISTIK - Menampilkan analisis data karyawan
"""

# Library yang dibutuhkan
import re
import csv
from datetime import datetime

# Data dummy karyawan
data_karyawan = [
    {
        "id_karyawan": "EMP001",
        "nama": "Rava Saragih",
        "departemen": "IT",
        "posisi": "Manager",
        "gaji": 30000000,
        "tanggal_masuk": "01-01-2020",
        "email": "rava.saragih@email.com",
        "telepon": "081234567890",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP002",
        "nama": "Joko Widodo",
        "departemen": "Finance",
        "posisi": "Staff",
        "gaji": 8000000,
        "tanggal_masuk": "15-03-2021",
        "email": "joko.widodo@email.com",
        "telepon": "081234567891",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP003",
        "nama": "Made Krisna",
        "departemen": "HR",
        "posisi": "Supervisor",
        "gaji": 12000000,
        "tanggal_masuk": "10-06-2019",
        "email": "made.krisna@email.com",
        "telepon": "081234567892",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP004",
        "nama": "Rina Kartika",
        "departemen": "Marketing",
        "posisi": "Staff",
        "gaji": 7500000,
        "tanggal_masuk": "20-08-2022",
        "email": "rina.kartika@email.com",
        "telepon": "081234567893",
        "status": "Kontrak"
    },
    {
        "id_karyawan": "EMP005",
        "nama": "Dedi Kurniawan",
        "departemen": "IT",
        "posisi": "Staff",
        "gaji": 9000000,
        "tanggal_masuk": "05-02-2021",
        "email": "dedi.kurniawan@email.com",
        "telepon": "081234567894",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP006",
        "nama": "Linda Wijaya",
        "departemen": "Finance",
        "posisi": "Manager",
        "gaji": 18000000,
        "tanggal_masuk": "10-05-2018",
        "email": "linda.wijaya@email.com",
        "telepon": "081234567895",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP007",
        "nama": "Darmawangsa Mahesa",
        "departemen": "Operations",
        "posisi": "Supervisor",
        "gaji": 11000000,
        "tanggal_masuk": "20-09-2020",
        "email": "darmawangsa.mahesa@email.com",
        "telepon": "081234567896",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP008",
        "nama": "Putri Amaliya",
        "departemen": "Marketing",
        "posisi": "Manager",
        "gaji": 16000000,
        "tanggal_masuk": "15-07-2019",
        "email": "putri.amaliya@email.com",
        "telepon": "081234567897",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP009",
        "nama": "Tom Setiawan",
        "departemen": "HR",
        "posisi": "Staff",
        "gaji": 7800000,
        "tanggal_masuk": "01-11-2021",
        "email": "tom.setiawan@email.com",
        "telepon": "081234567898",
        "status": "Kontrak"
    },
    {
        "id_karyawan": "EMP010",
        "nama": "Bintang Sari",
        "departemen": "IT",
        "posisi": "Supervisor",
        "gaji": 13000000,
        "tanggal_masuk": "25-04-2020",
        "email": "bintang.sari@email.com",
        "telepon": "081234567899",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP011",
        "nama": "Jayanagara Nugroho",
        "departemen": "Operations",
        "posisi": "Staff",
        "gaji": 6500000,
        "tanggal_masuk": "12-08-2022",
        "email": "jayanagara.nugroho@email.com",
        "telepon": "081234567800",
        "status": "Magang"
    },
    {
        "id_karyawan": "EMP012",
        "nama": "Guna Lestari",
        "departemen": "Finance",
        "posisi": "Supervisor",
        "gaji": 12500000,
        "tanggal_masuk": "30-01-2019",
        "email": "guna.lestari@email.com",
        "telepon": "081234567801",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP013",
        "nama": "Henry Gunawan",
        "departemen": "Marketing",
        "posisi": "Supervisor",
        "gaji": 11500000,
        "tanggal_masuk": "18-06-2020",
        "email": "henry.gunawan@email.com",
        "telepon": "081234567802",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP014",
        "nama": "Sinta Puspita",
        "departemen": "HR",
        "posisi": "Manager",
        "gaji": 17000000,
        "tanggal_masuk": "05-03-2017",
        "email": "sinta.puspita@email.com",
        "telepon": "081234567803",
        "status": "Tetap"
    },
    {
        "id_karyawan": "EMP015",
        "nama": "Adipati Suryaningrat",
        "departemen": "IT",
        "posisi": "Intern",
        "gaji": 4500000,
        "tanggal_masuk": "01-09-2023",
        "email": "adipati.suryaningrat@email.com",
        "telepon": "081234567804",
        "status": "Magang"
    }
]

# Data untuk menyimpan karyawan yang dihapus (backup)
data_karyawan_dihapus = []

# Fungsi Validasi input
def validasi_id_karyawan(id_karyawan):
    pattern = r'^EMP\d{3}$'
    return bool(re.match(pattern, id_karyawan))

def validasi_nama(nama):
    return bool(nama) and all(char.isalpha() or char.isspace() for char in nama)

def validasi_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))

def validasi_telepon(telepon):
    pattern = r'^08\d{8,11}$'
    return bool(re.match(pattern, telepon))

def validasi_tanggal(tanggal):
    try:
        datetime.strptime(tanggal, "%d-%m-%Y")
        return True
    except ValueError:
        return False

def validasi_gaji(gaji_str):
    try:
        gaji = int(gaji_str)
        return gaji > 0
    except ValueError:
        return False

# Fungsi pembantu
def generate_id_baru():
    if not data_karyawan:
        return "EMP001"
    
    # Ambil semua nomor ID yang sudah ada
    nomor_ids = []
    for karyawan in data_karyawan:
        nomor = int(karyawan["id_karyawan"][3:])
        nomor_ids.append(nomor)
    
    # Generate ID baru dengan nomor terbesar + 1
    nomor_baru = max(nomor_ids) + 1
    return f"EMP{nomor_baru:03d}"

def cari_karyawan_by_id(id_karyawan):
    for karyawan in data_karyawan:
        if karyawan["id_karyawan"] == id_karyawan:
            return karyawan
    return None

def format_rupiah(angka):
    return f"Rp {angka:,}".replace(",", ".")

def tampilkan_tabel_karyawan(list_karyawan):
    if not list_karyawan:
        print("\n[!] Tidak ada data karyawan yang ditampilkan.")
        return
    
    print("\n" + "="*150)
    print(f"{'ID':<10} {'Nama':<20} {'Departemen':<12} {'Posisi':<15} {'Gaji':<18} {'Tgl Masuk':<12} {'Status':<10}")
    print("="*150)
    
    for karyawan in list_karyawan:
        print(f"{karyawan['id_karyawan']:<10} {karyawan['nama']:<20} {karyawan['departemen']:<12} "
              f"{karyawan['posisi']:<15} {format_rupiah(karyawan['gaji']):<18} "
              f"{karyawan['tanggal_masuk']:<12} {karyawan['status']:<10}")
    
    print("="*150)

def tampilkan_detail_karyawan(karyawan):
    print("\n" + "="*60)
    print("DETAIL DATA KARYAWAN")
    print("="*60)
    print(f"ID Karyawan      : {karyawan['id_karyawan']}")
    print(f"Nama Lengkap     : {karyawan['nama']}")
    print(f"Departemen       : {karyawan['departemen']}")
    print(f"Posisi           : {karyawan['posisi']}")
    print(f"Gaji             : {format_rupiah(karyawan['gaji'])}")
    print(f"Tanggal Masuk    : {karyawan['tanggal_masuk']}")
    print(f"Email            : {karyawan['email']}")
    print(f"Telepon          : {karyawan['telepon']}")
    print(f"Status           : {karyawan['status']}")
    print("="*60)

def konfirmasi_aksi(pesan):
    while True:
        konfirmasi = input(f"\n{pesan} (Y/N): ").upper()
        if konfirmasi == 'Y':
            return True
        elif konfirmasi == 'N':
            return False
        else:
            print("[!] Input tidak valid! Masukkan Y atau N.")

# FITUR 1: CREATE (MENAMBAH DATA)
def input_data_karyawan():
    print("\n" + "="*60)
    print("TAMBAH DATA KARYAWAN BARU")
    print("="*60)
    print("[INFO] Tekan 'q' pada input apapun untuk membatalkan")
    
    id_baru = generate_id_baru()
    print(f"\n[AUTO] ID Karyawan: {id_baru}")
    
    # Input Nama dengan validasi
    while True:
        nama = input("\nMasukkan Nama Lengkap: ").strip().title()
        if nama.lower() == 'q':
            return None
        if validasi_nama(nama):
            break
        print("[!] Nama tidak valid! Gunakan huruf dan spasi saja.")
    
    # Input Departemen
    departemen_list = ["IT", "Finance", "HR", "Marketing", "Operations"]
    print(f"\nDepartemen yang tersedia: {', '.join(departemen_list)}")
    while True:
        departemen = input("Masukkan Departemen: ").strip()
        if departemen.lower() == 'q':
            return None
        
        if departemen.upper() == "IT":
            departemen = "IT"
        elif departemen.upper() == "HR":
            departemen = "HR"
        else:
            departemen = departemen.title()
            
        if departemen in departemen_list:
            break
        print(f"[!] Departemen tidak valid! Pilih dari: {', '.join(departemen_list)}")
    
    # Input Posisi
    posisi_list = ["Manager", "Supervisor", "Staff", "Intern"]
    print(f"\nPosisi yang tersedia: {', '.join(posisi_list)}")
    while True:
        posisi = input("Masukkan Posisi: ").strip().title()
        if posisi.lower() == 'q':
            return None
        if posisi in posisi_list:
            break
        print(f"[!] Posisi tidak valid! Pilih dari: {', '.join(posisi_list)}")
    
    # Input Gaji
    while True:
        gaji_input = input("\nMasukkan Gaji (angka saja): ").strip()
        if gaji_input.lower() == 'q':
            return None
        if validasi_gaji(gaji_input):
            gaji = int(gaji_input)
            break
        print("[!] Gaji tidak valid! Masukkan angka positif.")
    
    # Input Tanggal Masuk
    while True:
        tanggal_masuk = input("\nMasukkan Tanggal Masuk (DD-MM-YYYY): ").strip()
        if tanggal_masuk.lower() == 'q':
            return None
        if validasi_tanggal(tanggal_masuk):
            break
        print("[!] Format tanggal tidak valid! Gunakan DD-MM-YYYY.")
    
    # Input Email
    while True:
        email = input("\nMasukkan Email: ").strip().lower()
        if email.lower() == 'q':
            return None
        if validasi_email(email):
            break
        print("[!] Format email tidak valid!")
    
    # Input Telepon
    while True:
        telepon = input("\nMasukkan Nomor Telepon (08xxxxxxxxxx): ").strip()
        if telepon.lower() == 'q':
            return None
        if validasi_telepon(telepon):
            break
        print("[!] Format telepon tidak valid! Mulai dengan 08 dan 10-13 digit.")
    
    # Input Status
    if posisi == "Intern":
        status = "Magang"
        print(f"\n[AUTO] Status: {status} (Otomatis untuk posisi Intern)")
    else:
        status_list = ["Tetap", "Kontrak", "Magang"]
        print(f"\nStatus yang tersedia: {', '.join(status_list)}")
        while True:
            status = input("Masukkan Status: ").strip().title()
            if status.lower() == 'q':
                return None
            if status in status_list:
                break
            print(f"[!] Status tidak valid! Pilih dari: {', '.join(status_list)}")
    
    # Buat dictionary karyawan baru
    karyawan_baru = {
        "id_karyawan": id_baru,
        "nama": nama,
        "departemen": departemen,
        "posisi": posisi,
        "gaji": gaji,
        "tanggal_masuk": tanggal_masuk,
        "email": email,
        "telepon": telepon,
        "status": status
    }
    
    return karyawan_baru

def create_data():
    karyawan_baru = input_data_karyawan()
    
    if karyawan_baru is None:
        print("\n[BATAL] Penambahan data dibatalkan.")
        return
    
    # Tampilkan preview data
    print("\n[PREVIEW] Data yang akan ditambahkan:")
    tampilkan_detail_karyawan(karyawan_baru)
    
    # Konfirmasi
    if konfirmasi_aksi("Apakah Anda yakin ingin menambahkan data ini?"):
        data_karyawan.append(karyawan_baru)
        print(f"\n[SUKSES] Data karyawan {karyawan_baru['nama']} berhasil ditambahkan!")
    else:
        print("\n[BATAL] Penambahan data dibatalkan.")

# FITUR 2: READ
def read_data():
    if not data_karyawan:
        print("\n[!] Tidak ada data karyawan.")
        return
    
    while True:
        print("\n" + "="*60)
        print("MENU TAMPILKAN DATA KARYAWAN")
        print("="*60)
        print("1. Tampilkan Semua Data")
        print("2. Tampilkan Berdasarkan Departemen")
        print("3. Tampilkan Berdasarkan Status")
        print("4. Cari Berdasarkan ID")
        print("5. Cari Berdasarkan Nama")
        print("6. Urutkan Berdasarkan Gaji (Terendah)")
        print("7. Urutkan Berdasarkan Gaji (Tertinggi)")
        print("8. Urutkan Berdasarkan Tanggal Masuk (Terlama)")
        print("9. Kembali ke Menu Utama")
        
        pilihan = input("\nPilih menu (1-9): ").strip()
        
        if pilihan == '1':
            # Tampilkan semua data
            tampilkan_tabel_karyawan(data_karyawan)
            
        elif pilihan == '2':
            # Filter berdasarkan departemen
            departemen_list = ["IT", "Finance", "HR", "Marketing", "Operations"]
            print(f"\nDepartemen yang tersedia: {', '.join(departemen_list)}")
            departemen = input("Masukkan Departemen: ").strip()
            
            if departemen.upper() == "IT":
                departemen = "IT"
            elif departemen.upper() == "HR":
                departemen = "HR"
            else:
                departemen = departemen.title()
            
            hasil = [k for k in data_karyawan if k["departemen"] == departemen]
            if hasil:
                tampilkan_tabel_karyawan(hasil)
            else:
                print(f"\n[!] Tidak ada karyawan di departemen {departemen}.")
                
        elif pilihan == '3':
            # Filter berdasarkan status
            status = input("\nMasukkan Status (Tetap/Kontrak/Magang): ").strip().title()
            hasil = [k for k in data_karyawan if k["status"] == status]
            if hasil:
                tampilkan_tabel_karyawan(hasil)
            else:
                print(f"\n[!] Tidak ada karyawan dengan status {status}.")
                
        elif pilihan == '4':
            # Cari berdasarkan ID
            id_cari = input("\nMasukkan ID Karyawan: ").strip().upper()
            karyawan = cari_karyawan_by_id(id_cari)
            if karyawan:
                tampilkan_detail_karyawan(karyawan)
            else:
                print(f"\n[!] Karyawan dengan ID {id_cari} tidak ditemukan.")
                
        elif pilihan == '5':
            # Cari berdasarkan nama
            nama_cari = input("\nMasukkan Nama Karyawan: ").strip().lower()
            hasil = [k for k in data_karyawan if nama_cari in k["nama"].lower()]
            if hasil:
                tampilkan_tabel_karyawan(hasil)
            else:
                print(f"\n[!] Tidak ada karyawan dengan nama yang mengandung '{nama_cari}'.")
                
        elif pilihan == '6':
            # Sort berdasarkan gaji terendah
            data_sorted = sorted(data_karyawan, key=lambda x: x["gaji"])
            tampilkan_tabel_karyawan(data_sorted)
            
        elif pilihan == '7':
            # Sort berdasarkan gaji tertinggi
            data_sorted = sorted(data_karyawan, key=lambda x: x["gaji"], reverse=True)
            tampilkan_tabel_karyawan(data_sorted)
            
        elif pilihan == '8':
            # Sort berdasarkan tanggal masuk terlama
            data_sorted = sorted(data_karyawan, key=lambda x: datetime.strptime(x["tanggal_masuk"], "%d-%m-%Y"))
            tampilkan_tabel_karyawan(data_sorted)
            
        elif pilihan == '9':
            break
            
        else:
            print("\n[!] Pilihan tidak valid!")
        
        # Tanya apakah ingin export data yang ditampilkan
        if pilihan in ['1', '2', '3', '6', '7', '8']:
            if konfirmasi_aksi("\nApakah Anda ingin export data ini ke CSV?"):
                # Tentukan data yang akan di-export
                if pilihan == '1':
                    data_export = data_karyawan
                elif pilihan == '2':
                    data_export = hasil
                elif pilihan == '3':
                    data_export = hasil
                else:
                    data_export = data_sorted
                
                export_to_csv(data_export)

# FITUR 3: UPDATE 
def update_data():
    if not data_karyawan:
        print("\n[!] Tidak ada data karyawan.")
        return
    
    print("\n" + "="*60)
    print("UPDATE DATA KARYAWAN")
    print("="*60)
    
    # Tampilkan semua data
    tampilkan_tabel_karyawan(data_karyawan)
    
    # Input ID karyawan yang akan diupdate
    id_update = input("\nMasukkan ID Karyawan yang akan diupdate (atau 'q' untuk batal): ").strip().upper()
    if id_update.lower() == 'q':
        print("\n[BATAL] Update data dibatalkan.")
        return
    
    # Cari karyawan
    karyawan = cari_karyawan_by_id(id_update)
    if not karyawan:
        print(f"\n[!] Karyawan dengan ID {id_update} tidak ditemukan.")
        return
    
    # Tampilkan data karyawan yang akan diupdate
    print("\n[INFO] Data karyawan saat ini:")
    tampilkan_detail_karyawan(karyawan)
    
    # Menu pilihan field yang akan diupdate
    while True:
        print("\n" + "="*60)
        print("PILIH FIELD YANG AKAN DIUPDATE")
        print("="*60)
        print("1. Nama")
        print("2. Departemen")
        print("3. Posisi")
        print("4. Gaji")
        print("5. Tanggal Masuk")
        print("6. Email")
        print("7. Telepon")
        print("8. Status")
        print("9. Selesai Update")
        
        pilihan = input("\nPilih field (1-9): ").strip()
        
        if pilihan == '1':
            # Update nama
            while True:
                nama_baru = input("\nMasukkan Nama Baru: ").strip().title()
                if validasi_nama(nama_baru):
                    karyawan["nama"] = nama_baru
                    print("[SUKSES] Nama berhasil diupdate!")
                    break
                print("[!] Nama tidak valid!")
                
        elif pilihan == '2':
            # Update departemen
            departemen_list = ["IT", "Finance", "HR", "Marketing", "Operations"]
            print(f"\nDepartemen: {', '.join(departemen_list)}")
            while True:
                departemen_baru = input("Masukkan Departemen Baru: ").strip()
                
                # Handle case khusus untuk IT dan HR
                if departemen_baru.upper() == "IT":
                    departemen_baru = "IT"
                elif departemen_baru.upper() == "HR":
                    departemen_baru = "HR"
                else:
                    departemen_baru = departemen_baru.title()
                    
                if departemen_baru in departemen_list:
                    karyawan["departemen"] = departemen_baru
                    print("[SUKSES] Departemen berhasil diupdate!")
                    break
                print("[!] Departemen tidak valid!")
                
        elif pilihan == '3':
            # Update posisi
            posisi_list = ["Manager", "Supervisor", "Staff", "Intern"]
            print(f"\nPosisi: {', '.join(posisi_list)}")
            while True:
                posisi_baru = input("Masukkan Posisi Baru: ").strip().title()
                if posisi_baru in posisi_list:
                    karyawan["posisi"] = posisi_baru
                    
                    if posisi_baru == "Intern":
                        karyawan["status"] = "Magang"
                        print("[INFO] Status otomatis diubah ke 'Magang' karena posisi Intern")
                    
                    print("[SUKSES] Posisi berhasil diupdate!")
                    break
                print("[!] Posisi tidak valid!")
                
        elif pilihan == '4':
            # Update gaji
            while True:
                gaji_baru = input("\nMasukkan Gaji Baru: ").strip()
                if validasi_gaji(gaji_baru):
                    karyawan["gaji"] = int(gaji_baru)
                    print("[SUKSES] Gaji berhasil diupdate!")
                    break
                print("[!] Gaji tidak valid!")
                
        elif pilihan == '5':
            # Update tanggal masuk
            while True:
                tanggal_baru = input("\nMasukkan Tanggal Masuk Baru (DD-MM-YYYY): ").strip()
                if validasi_tanggal(tanggal_baru):
                    karyawan["tanggal_masuk"] = tanggal_baru
                    print("[SUKSES] Tanggal masuk berhasil diupdate!")
                    break
                print("[!] Format tanggal tidak valid!")
                
        elif pilihan == '6':
            # Update email
            while True:
                email_baru = input("\nMasukkan Email Baru: ").strip().lower()
                if validasi_email(email_baru):
                    karyawan["email"] = email_baru
                    print("[SUKSES] Email berhasil diupdate!")
                    break
                print("[!] Format email tidak valid!")
                
        elif pilihan == '7':
            # Update telepon
            while True:
                telepon_baru = input("\nMasukkan Telepon Baru: ").strip()
                if validasi_telepon(telepon_baru):
                    karyawan["telepon"] = telepon_baru
                    print("[SUKSES] Telepon berhasil diupdate!")
                    break
                print("[!] Format telepon tidak valid!")
                
        elif pilihan == '8':
            # Update status
            if karyawan["posisi"] == "Intern":
                print("\n[INFO] Posisi Intern hanya bisa memiliki status 'Magang'")
                print("[INFO] Jika ingin mengubah status, ubah posisi terlebih dahulu")
            else:
                status_list = ["Tetap", "Kontrak", "Magang"]
                print(f"\nStatus: {', '.join(status_list)}")
                while True:
                    status_baru = input("Masukkan Status Baru: ").strip().title()
                    if status_baru in status_list:
                        karyawan["status"] = status_baru
                        print("[SUKSES] Status berhasil diupdate!")
                        break
                    print("[!] Status tidak valid!")
                
        elif pilihan == '9':
            # Tampilkan data setelah update
            print("\n[INFO] Data karyawan setelah update:")
            tampilkan_detail_karyawan(karyawan)
            print("\n[SUKSES] Update data selesai!")
            break
            
        else:
            print("\n[!] Pilihan tidak valid!")

# FITUR 4: DELETE (MENGHAPUS DATA)
def delete_data():
    if not data_karyawan:
        print("\n[!] Tidak ada data karyawan.")
        return
    
    print("\n" + "="*60)
    print("HAPUS DATA KARYAWAN")
    print("="*60)
    
    # Tampilkan semua data
    tampilkan_tabel_karyawan(data_karyawan)
    
    # Input ID karyawan yang akan dihapus
    id_hapus = input("\nMasukkan ID Karyawan yang akan dihapus (atau 'q' untuk batal): ").strip().upper()
    if id_hapus.lower() == 'q':
        print("\n[BATAL] Penghapusan data dibatalkan.")
        return
    
    # cari karyawan
    karyawan = cari_karyawan_by_id(id_hapus)
    if not karyawan:
        print(f"\n[!] Karyawan dengan ID {id_hapus} tidak ditemukan.")
        return
    
    # Tampilkan data yang akan dihapus
    print("\n[INFO] Data karyawan yang akan dihapus:")
    tampilkan_detail_karyawan(karyawan)
    
    # Konfirmasi penghapusan
    if konfirmasi_aksi("Apakah Anda yakin ingin menghapus data ini?"):
        # Backup data ke list karyawan yang dihapus
        data_karyawan_dihapus.append(karyawan.copy())
        
        # hapus dari list utama
        data_karyawan.remove(karyawan)
        
        print(f"\n[SUKSES] Data karyawan {karyawan['nama']} berhasil dihapus!")
        print("[INFO] Data telah dibackup ke riwayat penghapusan.")
    else:
        print("\n[BATAL] Penghapusan data dibatalkan.")

# fitur export ke csv
def export_to_csv(data_export=None):
    if data_export is None:
        data_export = data_karyawan
    
    if not data_export:
        print("\n[!] Tidak ada data untuk di-export.")
        return
    
    # Buat nama file dengan timestamp
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    nama_file = f"data_karyawan_{timestamp}.csv"
    
    try:
        with open(nama_file, 'w', newline='', encoding='utf-8') as file:
            # Ambil header dari keys dictionary pertama
            fieldnames = data_export[0].keys()
            writer = csv.DictWriter(file, fieldnames=fieldnames)
            
            # Tulis header dan data
            writer.writeheader()
            writer.writerows(data_export)
        
        print(f"\n[SUKSES] Data berhasil di-export ke file: {nama_file}")
        print(f"[INFO] Total {len(data_export)} data karyawan berhasil di-export.")
        
    except Exception as e:
        print(f"\n[ERROR] Gagal export data: {str(e)}")

# fitur statistik
def tampilkan_statistik():
    if not data_karyawan:
        print("\n[!] Tidak ada data karyawan.")
        return
    
    print("\n" + "="*60)
    print("STATISTIK DATA KARYAWAN")
    print("="*60)
    
    # Total karyawan
    total = len(data_karyawan)
    print(f"\nTotal Karyawan: {total}")
    
    # Statistik berdasarkan departemen
    print("\n--- Berdasarkan Departemen ---")
    departemen_count = {}
    for karyawan in data_karyawan:
        dept = karyawan["departemen"]
        if dept in departemen_count:
            departemen_count[dept] += 1
        else:
            departemen_count[dept] = 1
    
    for dept, count in departemen_count.items():
        persentase = (count / total) * 100
        print(f"{dept:<15}: {count} orang ({persentase:.1f}%)")
    
    # Statistik berdasarkan status
    print("\n--- Berdasarkan Status ---")
    status_count = {}
    for karyawan in data_karyawan:
        status = karyawan["status"]
        if status in status_count:
            status_count[status] += 1
        else:
            status_count[status] = 1
    
    for status, count in status_count.items():
        persentase = (count / total) * 100
        print(f"{status:<15}: {count} orang ({persentase:.1f}%)")
    
    # Statistik berdasarkan posisi
    print("\n--- Berdasarkan Posisi ---")
    posisi_count = {}
    for karyawan in data_karyawan:
        posisi = karyawan["posisi"]
        if posisi in posisi_count:
            posisi_count[posisi] += 1
        else:
            posisi_count[posisi] = 1
    
    for posisi, count in posisi_count.items():
        persentase = (count / total) * 100
        print(f"{posisi:<15}: {count} orang ({persentase:.1f}%)")
    
    # Statistik gaji
    print("\n--- Statistik Gaji ---")
    total_gaji = sum(k["gaji"] for k in data_karyawan)
    rata_rata_gaji = total_gaji / total
    gaji_tertinggi = max(k["gaji"] for k in data_karyawan)
    gaji_terendah = min(k["gaji"] for k in data_karyawan)
    
    print(f"Total Gaji Bulanan : {format_rupiah(total_gaji)}")
    print(f"Rata-rata Gaji     : {format_rupiah(int(rata_rata_gaji))}")
    print(f"Gaji Tertinggi     : {format_rupiah(gaji_tertinggi)}")
    print(f"Gaji Terendah      : {format_rupiah(gaji_terendah)}")
    
    # Karyawan dengan gaji tertinggi
    karyawan_gaji_tinggi = [k for k in data_karyawan if k["gaji"] == gaji_tertinggi]
    print(f"\nKaryawan dengan gaji tertinggi:")
    for k in karyawan_gaji_tinggi:
        print(f"  - {k['nama']} ({k['posisi']}) - {format_rupiah(k['gaji'])}")
    
    print("="*60)

# fitur riwayat penghapusan
def lihat_riwayat_penghapusan():
    if not data_karyawan_dihapus:
        print("\n[!] Tidak ada riwayat penghapusan data.")
        return
    
    print("\n" + "="*60)
    print("RIWAYAT DATA KARYAWAN YANG DIHAPUS")
    print("="*60)
    
    tampilkan_tabel_karyawan(data_karyawan_dihapus)
    
    # Tanya apakah ingin restore data
    if konfirmasi_aksi("\nApakah Anda ingin restore salah satu data?"):
        restore_data()

def restore_data():
    if not data_karyawan_dihapus:
        print("\n[!] Tidak ada data yang dapat di-restore.")
        return
    
    # Input ID yang akan di-restore
    id_restore = input("\nMasukkan ID Karyawan yang akan di-restore: ").strip().upper()
    
    # Cari data di riwayat penghapusan
    karyawan_restore = None
    for karyawan in data_karyawan_dihapus:
        if karyawan["id_karyawan"] == id_restore:
            karyawan_restore = karyawan
            break
    
    if not karyawan_restore:
        print(f"\n[!] Data dengan ID {id_restore} tidak ditemukan di riwayat penghapusan.")
        return
    
    # Cek apakah ID sudah ada di data aktif
    if cari_karyawan_by_id(id_restore):
        print(f"\n[!] ID {id_restore} sudah ada di data aktif.")
        print("[INFO] Akan generate ID baru untuk data ini.")
        id_baru = generate_id_baru()
        karyawan_restore["id_karyawan"] = id_baru
        print(f"[INFO] ID baru: {id_baru}")
    
    # Tampilkan data yang akan di-restore
    tampilkan_detail_karyawan(karyawan_restore)
    
    # Konfirmasi restore
    if konfirmasi_aksi("Apakah Anda yakin ingin restore data ini?"):
        # Tambahkan kembali ke data aktif
        data_karyawan.append(karyawan_restore.copy())
        
        # Hapus dari riwayat penghapusan
        data_karyawan_dihapus.remove(karyawan)
        
        print(f"\n[SUKSES] Data karyawan {karyawan_restore['nama']} berhasil di-restore!")
    else:
        print("\n[BATAL] Restore data dibatalkan.")

# Fitur pencarian lanjutan
def pencarian_lanjutan():
    if not data_karyawan:
        print("\nTidak ada data karyawan!")
        return
    
    print("\n" + "="*60)
    print("PENCARIAN LANJUTAN")
    print("="*60)
    print("Tekan Enter untuk skip filter tertentu")
    
    hasil = data_karyawan.copy()
    
    # Filter departemen
    departemen_list = ["IT", "Finance", "HR", "Marketing", "Operations"]
    print(f"Departemen tersedia: {', '.join(departemen_list)}")
    departemen = input("\nFilter Departemen (Enter untuk skip): ").strip()
    if departemen:
        if departemen.upper() == "IT":
            departemen = "IT"
        elif departemen.upper() == "HR":
            departemen = "HR"
        else:
            departemen = departemen.title()
        hasil = [k for k in hasil if k["departemen"] == departemen]
    
    # Filter posisi
    posisi = input("Filter Posisi (Enter untuk skip): ").strip().title()
    if posisi:
        hasil = [k for k in hasil if k["posisi"] == posisi]
    
    # Filter status
    status = input("Filter Status (Enter untuk skip): ").strip().title()
    if status:
        hasil = [k for k in hasil if k["status"] == status]
    
    # Filter range gaji
    gaji_min = input("Filter Gaji Minimum (Enter untuk skip): ").strip()
    if gaji_min and validasi_gaji(gaji_min):
        hasil = [k for k in hasil if k["gaji"] >= int(gaji_min)]
    
    gaji_max = input("Filter Gaji Maximum (Enter untuk skip): ").strip()
    if gaji_max and validasi_gaji(gaji_max):
        hasil = [k for k in hasil if k["gaji"] <= int(gaji_max)]
    
    # Tampilkan hasil
    if hasil:
        print(f"\n[INFO] Ditemukan {len(hasil)} data karyawan yang sesuai:")
        tampilkan_tabel_karyawan(hasil)
        
        # Tanya export
        if konfirmasi_aksi("\nApakah Anda ingin export hasil pencarian ke CSV?"):
            export_to_csv(hasil)
    else:
        print("\n[!] Tidak ada data yang sesuai dengan kriteria pencarian.")

#MENU UTAMA
def tampilkan_menu_utama():
    print("\n" + "="*60)
    print("SISTEM MANAJEMEN DATA KARYAWAN PERUSAHAAN")
    print("="*60)
    print("1. Tambah Data Karyawan")
    print("2. Tampilkan Data Karyawan")
    print("3. Update Data Karyawan")
    print("4. Hapus Data Karyawan")
    print("5. Export Data ke CSV")
    print("6. Tampilkan Statistik")
    print("7. Pencarian Lanjutan")
    print("8. Riwayat Penghapusan Data")
    print("9. Keluar")
    print("="*60)

def main():
    print("\n" + "="*60)
    print("SELAMAT DATANG DI SISTEM MANAJEMEN DATA KARYAWAN")
    print("="*60)
    print("Program ini membantu Anda mengelola data karyawan perusahaan")
    print("dengan fitur CRUD lengkap dan berbagai fitur tambahan.")
    
    while True:
        tampilkan_menu_utama()
        
        pilihan = input("\nPilih menu (1-9): ").strip()
        
        if pilihan == '1':
            create_data()
            
        elif pilihan == '2':
            read_data()
            
        elif pilihan == '3':
            update_data()
            
        elif pilihan == '4':
            delete_data()
            
        elif pilihan == '5':
            if data_karyawan:
                print("\n[INFO] Export semua data karyawan...")
                export_to_csv()
            else:
                print("\n[!] Tidak ada data untuk di-export.")
                
        elif pilihan == '6':
            tampilkan_statistik()
            
        elif pilihan == '7':
            pencarian_lanjutan()
            
        elif pilihan == '8':
            lihat_riwayat_penghapusan()
            
        elif pilihan == '9':
            if konfirmasi_aksi("Apakah Anda yakin ingin keluar dari program?"):
                print("\n" + "="*60)
                print("Terima kasih telah menggunakan aplikasi ini!")
                print("="*60)
                break
            
        else:
            print("\n[!] Pilihan tidak valid! Silakan pilih menu 1-9.")

if __name__ == "__main__":
    main()
    
