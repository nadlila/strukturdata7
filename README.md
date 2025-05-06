//PENCARIAN DATA MAHASISWA//

import java.util.Scanner; //mengimpor kelas scanner untuk membaca input dari user//

class Mahasiswa { //mendeklarasikan class mahasiswa dengan 4 atribut//
    String nim; //atribut menggunakan variabel string yaitu berupa teks//
    String nama; //atribut menggunakan variabel string yaitu berupa teks//
    String jurusan; //atribut menggunakan variabel string yaitu berupa teks//
    double ipk; //atribut menggunakan variabel double yaitu menyimpan angka titik desimal//

    public Mahasiswa(String nim, String nama, String jurusan, double ipk) { //menginisialisasi//
        this.nim = nim;
        this.nama = nama;
        this.jurusan = jurusan;
        this.ipk = ipk;
    }

    @Override
    public String toString() { //mengatur tampilan saat dicetak agar ditampilkan secara rapi//
        return String.format("NIM: %s\nNama: %s\nJurusan: %s\nIPK: %.2f", nim, nama, jurusan, ipk);
    }
}

public class PencarianDataMahasiswa { //mendefinisikan class utama yang berisi metode main//
    public static void main(String[] args) { //titik awal eksekusi program//
        // Data mahasiswa
        Mahasiswa[] daftarMahasiswa = { //membuat array berisi objek mahasiswa sebagai data awal yang akan dicari//
            new Mahasiswa("2023001", "Budi Santoso", "Teknik Informatika", 3.75),
            new Mahasiswa("2023002", "Andi Wijaya", "Sistem Informasi", 3.50),
            new Mahasiswa("2023003", "Dewi Lestari", "Teknik Komputer", 3.90),
            new Mahasiswa("2023004", "Rina Maulana", "Teknik Informatika", 3.60),
            new Mahasiswa("2023005", "Doni Kusuma", "Manajemen Informatika", 3.25),
            new Mahasiswa("2023006", "Sinta Rahma", "Sistem Informasi", 3.85),
            new Mahasiswa("2023007", "Rudi Hermawan", "Teknik Komputer", 3.40)
        };

        Scanner scanner = new Scanner(System.in); //membuat objek scanner agar inputan user bisa dibaca dari keyboard// 

        System.out.println("=== SISTEM PENCARIAN DATA MAHASISWA ==="); //menampilkan pesan//
        System.out.print("Masukkan NIM Mahasiswa yang dicari: ");
        String nimCari = scanner.nextLine(); //membaca input NIM dari user//

        // Lakukan pencarian linear
        Mahasiswa hasilPencarian = cariMahasiswaByNIM(daftarMahasiswa, nimCari); //memanggil metode pencarian dan menyimpan hasil pencarian dalam hasilPencarian//

        System.out.println("\nHASIL PENCARIAN:"); //menampilkan hasil pencarian//
        if (hasilPencarian != null) {
            System.out.println("Mahasiswa ditemukan!");
            System.out.println(hasilPencarian);
        } else {
            System.out.println("Mahasiswa dengan NIM " + nimCari + " tidak ditemukan.");
        }

        scanner.close(); //menutup scanner//
    }

    public static Mahasiswa cariMahasiswaByNIM(Mahasiswa[] daftarMahasiswa, String nim) { //mencari mahasiswa berdasarkan NIM satu per satu//
        for (int i = 0; i < daftarMahasiswa.length; i++) {
            // Bandingkan NIM mahasiswa saat ini dengan NIM yang dicari
            if (daftarMahasiswa[i].nim.equals(nim)) { //jika tidak ditemukan//
                return daftarMahasiswa[i]; //dikembalikan//
            }
        }
        // Jika tidak ditemukan
        return null;
    }
}

//PENCARIAN PRODUK//

import java.util.ArrayList; //mengimpor kelas ArrayList agar bisa menggunakan struktur data dinamis berupa array yang ukurannya bisa berubah-ubah//
import java.util.Scanner; //mengimpor kelas scanner untuk membaca input dari user//

class Produk {
    String id;
    String nama;
    String kategori;
    double harga;
    int stok;

    public Produk(String id, String nama, String kategori, double harga, int stok) {
        this.id = id;
        this.nama = nama;
        this.kategori = kategori;
        this.harga = harga;
        this.stok = stok;
    }

    @Override
    public String toString() {
        return String.format("%-5s | %-25s | %-15s | Rp %.2f | Stok: %d",
                             id, nama, kategori, harga, stok);
    }
}

public class PencarianProduk {
    public static void main(String[] args) {
        // Data produk
        Produk[] daftarProduk = {
            new Produk("P001", "Laptop Asus VivoBook", "Elektronik", 8500000, 10),
            new Produk("P002", "Smartphone Samsung Galaxy", "Elektronik", 5000000, 15),
            new Produk("P003", "Kemeja Formal Pria", "Fashion", 250000, 50),
            new Produk("P004", "Sepatu Lari Nike", "Fashion", 1200000, 25),
            new Produk("P005", "Buku Pemrograman Java", "Buku", 150000, 30),
            new Produk("P006", "Mouse Gaming Logitech", "Elektronik", 350000, 20),
            new Produk("P007", "Novel Bumi Manusia", "Buku", 95000, 40),
            new Produk("P008", "Tas Ransel", "Fashion", 300000, 35)
        };

        Scanner scanner = new Scanner(System.in);

        System.out.println("=== SISTEM PENCARIAN PRODUK ===");
        System.out.println("Kategori tersedia: Elektronik, Fashion, Buku");
        System.out.print("Masukkan kategori produk: ");
        String kategoriCari = scanner.nextLine();

        System.out.print("Masukkan harga minimum: Rp ");
        double hargaMin = scanner.nextDouble();

        System.out.print("Masukkan harga maksimum: Rp ");
        double hargaMax = scanner.nextDouble();

        // Lakukan pencarian linear multi-kriteria
        ArrayList<Produk> hasilPencarian = cariProdukByKriteria(daftarProduk, kategoriCari, hargaMin, hargaMax);

        System.out.println("\nHASIL PENCARIAN:");
        System.out.println("===============================================================");
        System.out.printf("%-5s | %-25s | %-15s | %-10s | %-10s\n",
                          "ID", "Nama Produk", "Kategori", "Harga", "Stok");
        System.out.println("---------------------------------------------------------------");

        if (hasilPencarian.size() > 0) {
            for (Produk p : hasilPencarian) {
                System.out.println(p);
            }
        } else {
            System.out.println("Tidak ada produk yang sesuai dengan kriteria pencarian.");
        }
        System.out.println("===============================================================");

        scanner.close();
    }

    public static ArrayList<Produk> cariProdukByKriteria(Produk[] daftarProduk,
                                                         String kategori,
                                                         double hargaMin,
                                                         double hargaMax) {
        ArrayList<Produk> hasilPencarian = new ArrayList<>();

        for (int i = 0; i < daftarProduk.length; i++) {
            Produk produk = daftarProduk[i];

            // Periksa apakah produk memenuhi semua kriteria
            if (produk.kategori.equalsIgnoreCase(kategori) &&
                produk.harga >= hargaMin &&
                produk.harga <= hargaMax) {
                hasilPencarian.add(produk);
            }
        }

        return hasilPencarian;
    }
}


//PENCARIAN KATA//

import java.util.ArrayList;
import java.util.Scanner;

public class PencarianKata {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("=== SISTEM PENCARIAN KATA ===");
        System.out.print("Masukkan teks: ");
        String teks = scanner.nextLine();

        System.out.print("Masukkan kata yang dicari: ");
        String kataCari = scanner.nextLine();

        // Lakukan pencarian kata
        ArrayList<Integer> posisiDitemukan = cariKata(teks, kataCari);

        System.out.println("\nHASIL PENCARIAN:");
        if (posisiDitemukan.size() > 0) {
            System.out.println("Kata '" + kataCari + "' ditemukan sebanyak " +
                               posisiDitemukan.size() + " kali pada posisi:");

            for (int i = 0; i < posisiDitemukan.size(); i++) {
                System.out.println("- Indeks ke-" + posisiDitemukan.get(i) +
                                   " (karakter ke-" + (posisiDitemukan.get(i) + 1) + ")");
            }

            // Tampilkan teks dengan highlight kata yang ditemukan
            System.out.println("\nTeks dengan highlight:");
            tampilkanTeksHighlight(teks, kataCari, posisiDitemukan);
        } else {
            System.out.println("Kata '" + kataCari + "' tidak ditemukan dalam teks.");
        }

        scanner.close();
    }

    public static ArrayList<Integer> cariKata(String teks, String kata) {
        ArrayList<Integer> posisi = new ArrayList<>();

        // Konversi ke lowercase untuk pencarian case-insensitive
        String teksLower = teks.toLowerCase();
        String kataLower = kata.toLowerCase();

        int panjangKata = kataLower.length();
        int panjangTeks = teksLower.length();

        // Lakukan linear search
        for (int i = 0; i <= panjangTeks - panjangKata; i++) {
            // Periksa apakah substring dari posisi i sampai i+panjangKata sama dengan kata
            String potongan = teksLower.substring(i, i + panjangKata);

            if (potongan.equals(kataLower)) {
                posisi.add(i);

                // Optional: Skip ke akhir kata yang ditemukan untuk menghindari overlap
                // i += panjangKata - 1;
            }
        }

        return posisi;
    }

    public static void tampilkanTeksHighlight(String teks, String kata, ArrayList<Integer> posisi) {
        StringBuilder hasil = new StringBuilder(teks);

        // Tambahkan marker untuk highlight (dari posisi terjauh dulu untuk menghindari pergeseran indeks)
        for (int i = posisi.size() - 1; i >= 0; i--) {
            int pos = posisi.get(i);
            hasil.insert(pos + kata.length(), "]");
            hasil.insert(pos, "[");
        }

        System.out.println(hasil.toString());
    }
}

