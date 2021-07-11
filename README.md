# tugas8SBD.19.B1

Nama : Nisa Madani

index

<!DOCTYPE html>
<html>
<head>
	<title>Kampus</title>
</head>
	<body>
		<! –– Form buat pemilihan tabel, dengan metode get, aksinya menjalankan showtabel.php yang ada pada folder ––>
		<form method="get" action="showtabel.php">
			<select name="tabel">
				<option>Pilih tabel</option>
				<! –– Query buat ngambil data tabel yang ada ––>
			  <?php 
			    require_once ('koneksi.php');
			    $tablist="SHOW tables";
			    $result = mysqli_query($koneksi,$tablist);
			    while($row = mysqli_fetch_row($result)){ ?>
			    	<option value="<?php echo $row[0];?>"><?php echo $row[0];}?></option>
			    	<option value="TampilSemua">Tampilkan semua tabel</option>
			    	<input type="submit" value="Tampilkan"></input>
			</select>
		</form>
	</body>
</html>


KONEKSI


<?php 
//ini variable $koneksi yang berisikan query buat koneksi ke database, dimana urutannya "host", "username", "password", "nama database"
$koneksi = mysqli_connect("localhost","root","","Kampus"); 

// Check connection kalo koneksi ke databasenya berhasil atau engga, kalo error nanti ada notif "koneksi database gagal"
if (mysqli_connect_errno()){
	echo "Koneksi database gagal" . mysqli_connect_error();
}


TABEL


<!DOCTYPE html>
<html>
<head>
	<title>Tampilkan tabel</title>
</head>
<body>
<?php 
require_once ('koneksi.php');
    if(isset($_GET['tabel'])){
	$tblname = $_GET['tabel'];
	}
	echo "Menampilkan tabel ", $tblname;
    ?>
    <?php if ($tblname=="dosen"): ?>  
    <! –– TABEL DOSEN ––>
    <table border="1" cellspacing="0" width="500" style="margin-top: 25px;">
    	<tr>
    		<td colspan="5" align="center">Dosen</td>
    	</tr>
    	<tr>
            <! –– Field pertama pada tabel ––>
            <td align="center">no</td>
    		<td align="center">nid</td>
    		<td align="center">nama dosen</td>
    		<td align="center">alamat</td>
    		<td align="center">email</td>
    	</tr>
        <tr>
            <! –– Query buat looping dan ambil data dari tabel ––>
    		<?php
    			$dosen = "dosen";
    			$showdosen = "select*from $dosen";
    			$querydosen = mysqli_query($koneksi,$showdosen);
                $nodo = 1;
    			while($dosenrow = mysqli_fetch_assoc($querydosen)){
    		?>
    	    <td align="center"><?php echo $nodo++ ?></td>
    		<td align="center"><?php echo $dosenrow['nid'];?></td>
    		<td align="center"><?php echo $dosenrow['nama_dosen'];?></td>
    		<td align="center"><?php echo $dosenrow['alamat'];?></td>
    		<td align="center"><?php echo $dosenrow['email'];?></td>
    	</tr><?php } ?>
    </table>
    <?php elseif($tblname=="mahasiswa"): ?>
    <! –– TABEL MAHASISWA ––>
    <table border="1" cellspacing="0" width="500" style="margin-top: 25px;">
    	<tr>
    		<td colspan="5" align="center">Mahasiswa</td>
    	</tr>
    	<tr>
            <td align="center">no</td>
    		<td align="center">nid</td>
    		<td align="center">nama dosen</td>
    		<td align="center">alamat</td>
    		<td align="center">email</td>
    	</tr>
    		<?php
    			$mhs = "mahasiswa";
    			$showmhs = "select*from $mhs";
    			$querymhs = mysqli_query($koneksi,$showmhs);
                $nomhs = 1;
    			while($mhsrow = mysqli_fetch_assoc($querymhs)){
    		?>
    	<tr>
            <td align="center"><?php echo $nomhs++ ?></td>
    		<td align="center"><?php echo $mhsrow['nim'];?></td>
    		<td align="center"><?php echo $mhsrow['nama'];?></td>
    		<td align="center"><?php echo $mhsrow['kelas'];?></td>
    		<td align="center"><?php echo $mhsrow['email'];?></td>
    	</tr><?php } ?> 
    </table>
    <?php elseif($tblname=="matakuliah"): ?>
    <! –– TABEL MATAKULIAH ––>
    <table border="1" cellspacing="0" width="500" style="margin-top: 25px;">
    	<tr>
    		<td colspan="4" align="center">Matakuliah</td>
    	</tr>
    	<tr>
            <td align="center">no</td>
    		<td align="center">kode matkul</td>
    		<td align="center">matakuliah</td>
    		<td align="center">jumlah sks</td>
    	</tr>
    		<?php
    			$matkul = "matakuliah";
    			$showmatkul = "select*from $matkul";
    			$querymatkul = mysqli_query($koneksi,$showmatkul);
                $nomk = 1;
    			while($matkulrow = mysqli_fetch_assoc($querymatkul)){
    		?>
    	<tr>
            <td align="center"><?php echo $nomk++ ?></td>
    		<td align="center"><?php echo $matkulrow['kode_matkul'];?></td>
    		<td align="center"><?php echo $matkulrow['matakuliah'];?></td>
    		<td align="center"><?php echo $matkulrow['sks'];?></td>
    	</tr><?php } ?> 
    </table>
    <?php elseif($tblname=="TampilSemua"): ?>
    <! –– TAMPILKAN SEMUA TABEL ––>
    <table border="1" cellspacing="0" width="500" style="margin-top: 25px;">
        <tr>
            <td colspan="5" align="center">Dosen</td>
        </tr>
        <tr>
            <td align="center">no</td>
            <td align="center">nid</td>
            <td align="center">nama dosen</td>
            <td align="center">alamat</td>
            <td align="center">email</td>
        </tr>
        <tr>
            <?php
                $dosen = "dosen";
                $showdosen = "select*from $dosen";
                $querydosen = mysqli_query($koneksi,$showdosen);
                $nodo = 1;
                while($dosenrow = mysqli_fetch_assoc($querydosen)){
            ?>
            <td align="center"><?php echo $nodo++ ?></td>
            <td align="center"><?php echo $dosenrow['nid'];?></td>
            <td align="center"><?php echo $dosenrow['nama_dosen'];?></td>
            <td align="center"><?php echo $dosenrow['alamat'];?></td>
            <td align="center"><?php echo $dosenrow['email'];?></td>
        </tr><?php } ?>
    </table>
    <table border="1" cellspacing="0" width="500" style="margin-top: 25px;">
        <tr>
            <td colspan="5" align="center">Mahasiswa</td>
        </tr>
        <tr>
            <td align="center">no</td>
            <td align="center">nid</td>
            <td align="center">nama dosen</td>
            <td align="center">alamat</td>
            <td align="center">email</td>
        </tr>
            <?php
                $mhs = "mahasiswa";
                $showmhs = "select*from $mhs";
                $querymhs = mysqli_query($koneksi,$showmhs);
                $nomhs = 1;
                while($mhsrow = mysqli_fetch_assoc($querymhs)){
            ?>
        <tr>
            <td align="center"><?php echo $nomhs++ ?></td>
            <td align="center"><?php echo $mhsrow['nim'];?></td>
            <td align="center"><?php echo $mhsrow['nama'];?></td>
            <td align="center"><?php echo $mhsrow['kelas'];?></td>
            <td align="center"><?php echo $mhsrow['email'];?></td>
        </tr><?php } ?> 
    </table>
    <table border="1" cellspacing="0" width="500" style="margin-top: 25px;">
        <tr>
            <td colspan="4" align="center">Matakuliah</td>
        </tr>
        <tr>
            <td align="center">no</td>
            <td align="center">kode matkul</td>
            <td align="center">matakuliah</td>
            <td align="center">jumlah sks</td>
        </tr>
            <?php
                $matkul = "matakuliah";
                $showmatkul = "select*from $matkul";
                $querymatkul = mysqli_query($koneksi,$showmatkul);
                $nomk = 1;
                while($matkulrow = mysqli_fetch_assoc($querymatkul)){
            ?>
        <tr>
            <td align="center"><?php echo $nomk++ ?></td>
            <td align="center"><?php echo $matkulrow['kode_matkul'];?></td>
            <td align="center"><?php echo $matkulrow['matakuliah'];?></td>
            <td align="center"><?php echo $matkulrow['sks'];?></td>
        </tr><?php } ?> 
    </table>
    <?php endif?>
    <br><br>
    <form action="index.php">
        <input type="submit" value="Kembali" />
    </form>
</body>
</html>

?>
