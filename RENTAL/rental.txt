/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package retal;



import java.io.*;
import java.sql.*;
public class Retal
{
    public static void main(String args[]) throws Exception {
        Class.forName("org.sqlite.JDBC");
        Connection conn = DriverManager.getConnection("jdbc:sqlite:rental.db");
        Statement stat = conn.createStatement();
        
        InputStreamReader istream = new InputStreamReader(System.in);
        BufferedReader bufRead = new BufferedReader(istream);
        
        System.out.println("========SELAMAT DATANG DI RENTAL MOBIL DYRAN========");
        System.out.println("Masukkan pilihan Anda :");
        System.out.println("1. Lanjut ke menu selanjutnya");
        System.out.println("2. Keluar");
        String baca = bufRead.readLine();
        int baca1 = Integer.parseInt(baca);
        


        if(baca1==1){
            boolean ulang = true;
            while(ulang) {
            System.out.println("1. Data Pelanggan");
            System.out.println("2. Data Transaksi Penyewaan");
            System.out.println("3. Keluar Program");
            String baca2 = bufRead.readLine();
            
            if(baca2.equals("1")){
                PreparedStatement prep = conn.prepareStatement("insert into data_pelanggan values(?,?,?,?,?);");
                
                System.out.println("1. Masukkan Data");
                System.out.println("2. Mengganti Data");
                System.out.println("3. Menghapus Data");
                System.out.println("4. Menampilkan Data");
                System.out.println("5. Keluar");
                System.out.println("Masukkan pilihan anda [1-4] :");
                String baca3 = bufRead.readLine();
                if(baca3.equals("1")){
                    System.out.println("Masukkan jumlah data yang ingin diinput");
                    String inp = bufRead.readLine();
                    int bnyk = Integer.parseInt(inp);
                    
                    for (int i=0; i<bnyk; i++){
                        System.out.println("Masukkan Kode Booking");
                        String kode = bufRead.readLine();
                        System.out.println("Masukkan Nama Anda");
                        String nama = bufRead.readLine();
                        System.out.println("Masukkan No.Tlp Anda");
                        String tlp = bufRead.readLine();
                        System.out.println("Masukkan Alamat Anda");
                        String alamat = bufRead.readLine();
                        System.out.println("Masukkan Email Anda");
                        String email = bufRead.readLine();
                        prep.setString(1, kode);
                        prep.setString(2, nama);
                        prep.setString(3, tlp);
                        prep.setString(4, alamat);
                        prep.setString(5, email);
                        prep.addBatch();
                    }
                    conn.setAutoCommit(false);
                    prep.executeBatch();
                    conn.setAutoCommit(true);
                    ResultSet anuan = stat.executeQuery("select * from data_pelanggan;");
                    System.out.println("Kode Booking \t\t Nama \t\t No.Tlp \t\t Alamat \t\t Email");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" +anuan.getString("nama"));
                        System.out.print("\t" + anuan.getString("tlp"));
                        System.out.print("\t" + anuan.getString("alamat"));
                        System.out.println("\t" + anuan.getString("email"));
                    }
                    anuan.close();
                    //conn.close();
                    System.out.println();
                    System.out.println("--------------------------------------------------");
                    System.out.println("Masukkan pilihan Anda :");
                    System.out.println("1. Lanjut ke menu sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                } else if(baca3.equals("2")){
                    ResultSet anuan = stat.executeQuery("select * from data_pelanggan;");
                    System.out.println("Kode Booking \t\t Nama \t\t No.Tlp \t\t Alamat \t\t Email");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("nama"));
                        System.out.print("\t" + anuan.getString("tlp"));
                        System.out.print("\t" + anuan.getString("alamat"));
                        System.out.println("\t" + anuan.getString("email"));
                    }
                    anuan.close();
                    
                    PreparedStatement update = conn.prepareStatement("update data_pelanggan set nama = ? where tlp = ?");
                    System.out.println("Masukkan nama yang ingin diganti :");
                    String nama = bufRead.readLine();
                    System.out.println("Masukkan No.Tlp yang ingin diubah :");
                    String tlp = bufRead.readLine();
                    update.setString(1, nama);
                    update.setString(2, tlp);
                    update.addBatch();
                    conn.setAutoCommit(false);
                    update.executeBatch();
                    conn.setAutoCommit(true);
                    ResultSet anu = stat.executeQuery("select * from data_pelanggan;");
                    System.out.println("Kode Booking \t\t Nama \t\t No.Tlp \t\t Alamat \t\t Email");
                    while (anu.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("nama"));
                        System.out.print("\t" + anuan.getString("tlp"));
                        System.out.print("\t" + anuan.getString("alamat"));
                        System.out.println("\t" + anuan.getString("email"));
                    }
                    anu.close();
                    //conn.close();
                    System.out.println();
                    
                    System.out.println("-------------------------------------------------");
                    System.out.println("1. Lanjut ke menu sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                }
                else if(baca3.equals("3")){
                    ResultSet anuan = stat.executeQuery("select * from data_pelanggan;");
                    System.out.println("Kode Booking \t\t Nama \t\t No.Tlp \t\t Alamat \t\t Email");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("nama"));
                        System.out.print("\t" + anuan.getString("tlp"));
                        System.out.print("\t" + anuan.getString("alamat"));
                        System.out.println("\t" + anuan.getString("email"));
                    }
                    anuan.close();
                    
                    PreparedStatement delete = conn.prepareStatement("delete from data_pelanggan where nama = ?;");
                    System.out.println("Masukkan nama yang ingin dihapus :");
                    String nama = bufRead.readLine();
                    delete.setString(1, nama);
                    delete.addBatch();
                    conn.setAutoCommit(false);
                    delete.executeBatch();
                    conn.setAutoCommit(true);
                    
                    ResultSet anu = stat.executeQuery("select * from data_pelanggan;");
                    System.out.println("Kode Booking \t\t Nama \t\t No.Tlp \t\t Alamat \t\t Email");
                    while (anu.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("nama"));
                        System.out.print("\t" + anuan.getString("tlp"));
                        System.out.print("\t" + anuan.getString("alamat"));
                        System.out.println("\t" + anuan.getString("email"));
                    }
                    anu.close();
                    //conn.close();
                    System.out.println();
                    
                    System.out.println("Masukkan pilihan anda :");
                    System.out.println("1. Lanjut ke menu sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                }
                else if (baca3.equals("4")){
                    ResultSet anuan = stat.executeQuery("select * from data_pelanggan;");
                    System.out.println("Kode Booking \t\t Nama \t\t No.Tlp \t\t Alamat \t\t Email");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("nama"));
                        System.out.print("\t" + anuan.getString("tlp"));
                        System.out.print("\t" + anuan.getString("alamat"));
                        System.out.println("\t" + anuan.getString("email"));
                    }
                    anuan.close();
                    //conn.close();
                    System.out.println();
                    
                    System.out.println("---------------------------------------------");
                    System.out.println("1. Lanjut ke menu Sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                }
            }
            if(baca2.equals("2")){
                PreparedStatement prep2 = conn.prepareStatement("insert into data_trans values(?,?,?,?,?,?,?,?,?,?);");
                
                System.out.println("1. Masukkan Data");
                System.out.println("2. Mengganti Data");
                System.out.println("3. Menghapus Data");
                System.out.println("4. Menampilkan Data");
                System.out.println("Masukkan pilihan anda [1-4] :");
                String baca3b = bufRead.readLine();
                if(baca3b.equals("1")){
                    System.out.println("Masukkan jumlah data yang ingin diinput");
                    String inp = bufRead.readLine();
                    int bnyk = Integer.parseInt(inp);
                    
                    for (int i=0; i<bnyk; i++){
                        System.out.println("Masukkan Kode Booking");
                        String kode = bufRead.readLine();
                        System.out.println("Masukkan Merk Mobil");
                        String merk = bufRead.readLine();
                        System.out.println("Masukkan Tipe Mobil");
                        String tipe = bufRead.readLine();
                        System.out.println("Masukkan No.Plat");
                        String plat = bufRead.readLine();
                        System.out.println("Masukkan Warna Mobil");
                        String warna = bufRead.readLine();
                        System.out.println("Masukkan Lama Peminjaman");
                        String lama = bufRead.readLine();
                        System.out.println("Masukkan Tanggal Pinjam");
                        String tanggal = bufRead.readLine();
                        System.out.println("Masukkan Tanggal Pengembalian");
                        String kembali = bufRead.readLine();
                        System.out.println("Masukkan Harga");
                        int harga = Integer.parseInt(bufRead.readLine());
                        System.out.println("Masukkan Total Yang Harus di Bayar");
                        int total = Integer.parseInt(bufRead.readLine());
                        
                        
                        prep2.setString(1, kode);
                        prep2.setString(2, merk);
                        prep2.setString(3, tipe);
                        prep2.setString(4, plat);
                        prep2.setString(5, warna);
                        prep2.setString(6, lama);
                        prep2.setString(7, tanggal);
                        prep2.setString(8, kembali);
                        prep2.setInt(9, harga);
                        prep2.setInt(10, total);
                        prep2.addBatch();
                    }
                    conn.setAutoCommit(false);
                    prep2.executeBatch();
                    conn.setAutoCommit(true);
                    ResultSet anuan = stat.executeQuery("select * from data_trans;");
                    System.out.println("Kode Booking \t\t Merk Mobil \t\t Tipe Mobil \t\t No.Plat \t\t Warna Mobil \t\t Lama Pinjam \t\t Tanggal Pinjam \t\t Tanggal Kembali \t\t Harga \t\t Total");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("merk"));
                        System.out.print("\t" + anuan.getString("tipe"));
                        System.out.print("\t" + anuan.getString("plat"));
                        System.out.print("\t" + anuan.getString("warna"));
                        System.out.print("\t" + anuan.getString("lama"));
                        System.out.print("\t" + anuan.getString("tanggal"));
                        System.out.print("\t" + anuan.getString("kembali"));
                        System.out.print("\t" + anuan.getInt("harga"));
                        System.out.println("\t" + anuan.getInt("total"));
                    }
                    anuan.close();
                    //conn.close();
                    System.out.println();
                    
                    System.out.println("--------------------------------------------------------------------------------------------------------------------------------------");
                    System.out.println("Masukkan pilihan anda :");
                    System.out.println("1. Lanjut ke menu Sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                }
                else if(baca3b.equals("2")){
                    ResultSet anuan = stat.executeQuery("select * from data_trans;");
                    System.out.println("Kode Booking \t\t Merk Mobil \t\t Tipe Mobil \t\t No.Plat \t\t Warna Mobil \t\t Lama Pinjam \t\t Tanggal Pinjam \t\t Tanggal kembali \t\t Harga \t\t Total");
                    while(anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("merk"));
                        System.out.print("\t" + anuan.getString("tipe"));
                        System.out.print("\t" + anuan.getString("plat"));
                        System.out.print("\t" + anuan.getString("warna"));
                        System.out.print("\t" + anuan.getString("lama"));
                        System.out.print("\t" + anuan.getString("tanggal"));
                        System.out.print("\t" + anuan.getString("kembali"));
                        System.out.print("\t" + anuan.getInt("harga"));
                        System.out.println("\t" + anuan.getInt("total"));
                    }
                    anuan.close();
                    
                    PreparedStatement update = conn.prepareStatement("update data_trans set merk = ? where kode =?");
                    System.out.println("Masukkan Merk yang ingin diganti :");
                    String merk = bufRead.readLine();
                    System.out.println("Masukkan Kode Booking yang ingin diubah merknya :");
                    String warna = bufRead.readLine();
                    update.setString(1, merk);
                    update.setString(2, warna);
                    update.addBatch();
                    conn.setAutoCommit(false);
                    update.executeBatch();
                    conn.setAutoCommit(true);
                    
                    ResultSet anu = stat.executeQuery("select * from data_trans;");
                    System.out.println("Kode Booking \t\t Merk Mobil \t\t Tipe Mobil \t\t No.Plat \t\t Warna Mobil \t\t Lama Pinjam \t\t Tanggal Pinjam \t\t Tanggal Kembali \t\t Harga \t\t Total");
                    while (anu.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("merk"));
                        System.out.print("\t" + anuan.getString("tipe"));
                        System.out.print("\t" + anuan.getString("plat"));
                        System.out.print("\t" + anuan.getString("warna"));
                        System.out.print("\t" + anuan.getString("lama"));
                        System.out.print("\t" + anuan.getString("tanggal"));
                        System.out.print("\t" + anuan.getString("kembali"));
                        System.out.print("\t" + anuan.getInt("harga"));
                        System.out.println("\t" + anuan.getInt("total"));
                    }
                    anu.close();
                   // conn.close();
                    System.out.println();
                    
                    System.out.println("-------------------------------------------------------------------------------------------------------------------------------------");
                    System.out.println("Masukkan pilihan anda :");
                    System.out.println("1. Lanjut ke menu Sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                }
                else if (baca3b.equals("3")){
                    ResultSet anuan = stat.executeQuery("select * from data_trans;");
                    System.out.println("Kode Booking \t\t Merk Mobil \t\t Tipe Mobil \t\t No.Plat \t\t Warna Mobil \t\t Lama Pinjam \t\t Tanggal Pinjam \t\t Tanggal Kembali \t\t Harga \t\t Total");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("merk"));
                        System.out.print("\t" + anuan.getString("tipe"));
                        System.out.print("\t" + anuan.getString("plat"));
                        System.out.print("\t" + anuan.getString("warna"));
                        System.out.print("\t" + anuan.getString("lama"));
                        System.out.print("\t" + anuan.getString("tanggal"));
                        System.out.print("\t" + anuan.getString("kembali"));
                        System.out.print("\t" + anuan.getInt("harga"));
                        System.out.println("\t" + anuan.getInt("total"));
                    }
                    anuan.close();
                    
                    PreparedStatement delete2 = conn.prepareStatement("delete from data_trans where kode = ?;");
                    System.out.println("Masukkan kode booking yang ingin dihapus :");
                    String kode = bufRead.readLine();
                    delete2.setString(1, kode);
                    delete2.addBatch();
                    conn.setAutoCommit(false);
                    delete2.executeBatch();
                    conn.setAutoCommit(true);
                    
                    ResultSet anu = stat.executeQuery("select * from data_trans;");
                    System.out.println("Kode Booking \t\t Merk Mobil \t\t Tipe Mobil \t\t No.Plat \t\t Warna Mobil \t\t Lama Pinjam \t\t Tanggal Pinjam \t\t Tanggal Kembali \t\t Harga \t\t Total");
                    while (anu.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("merk"));
                        System.out.print("\t" + anuan.getString("tipe"));
                        System.out.print("\t" + anuan.getString("plat"));
                        System.out.print("\t" + anuan.getString("warna"));
                        System.out.print("\t" + anuan.getString("lama"));
                        System.out.print("\t" + anuan.getString("tanggal"));
                        System.out.print("\t" + anuan.getString("kembali"));
                        System.out.print("\t" + anuan.getInt("harga"));
                        System.out.println("\t" + anuan.getInt("total"));
                    }
                    anu.close();
                   // conn.close();
                    System.out.println();
                    
                    System.out.println("--------------------------------------------------------------------------------------------------------------------------------------");
                    System.out.println("Masukkan pilihan anda :");
                    System.out.println("1. Lanjut ke menu Sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                }
                else if (baca3b.equals("4")){
                    ResultSet anuan = stat.executeQuery("select * from data_trans;");
                    System.out.println("Kode Booking \t Merk Mobil \t Tipe Mobil \t No.Plat \t Warna Mobil \t Lama Pinjam \t Tanggal Pinjam \t Tanggal Kembali \t Harga \t Total");
                    while (anuan.next()){
                        System.out.print(anuan.getString("kode"));
                        System.out.print("\t" + anuan.getString("merk"));
                        System.out.print("\t" + anuan.getString("tipe"));
                        System.out.print("\t" + anuan.getString("plat"));
                        System.out.print("\t" + anuan.getString("warna"));
                        System.out.print("\t" + anuan.getString("lama"));
                        System.out.print("\t" + anuan.getString("tanggal"));
                        System.out.print("\t" + anuan.getString("kembali"));
                        System.out.print("\t" + anuan.getInt("harga"));
                        System.out.println("\t" + anuan.getInt("total"));
                    }
                    anuan.close();
                    //conn.close();
                    System.out.println();
                    
                    System.out.println("--------------------------------------------------------------------------------------------------------------------------------------");
                    System.out.println("Masukkan pilihan anda :");
                    System.out.println("1. Lanjut ke menu Sebelumnya");
                    System.out.println("2. Keluar");
                    baca = bufRead.readLine();
                    baca1 = Integer.parseInt(baca);
                    
                }
            } else if(baca2.equals("3")) {
                
                    ulang = false;
                }
        } 
                
       }
    }
}


    
    
    

