# Tugas Pertemuan 5


Nama : Dhiya Ulhaq Ayyuasy
NIM : H1D021040
Shift Baru: D

## Screenshot

1. Login
![Login](3.png)
Menginputkan username dan password
  // Membuat Textbox email
  Widget _emailTextField() {
    return TextFormField(
      decoration: const InputDecoration(labelText: "Email"),
      keyboardType: TextInputType.emailAddress,
      controller: _emailTextboxController,
      validator: (value) {
        // Validasi harus diisi
        if (value!.isEmpty) {
          return 'Email harus diisi';
        }
        return null;
      },
    );
  }

  // Membuat Textbox password
  Widget _passwordTextField() {
    return TextFormField(
      decoration: const InputDecoration(labelText: "Password"),
      keyboardType: TextInputType.text,
      obscureText: true,
      controller: _passwordTextboxController,
      validator: (value) {
        // Jika karakter yang dimasukkan kurang dari 6 karakter
        if (value!.isEmpty) {
          return "Password harus diisi";
        }
        return null;
      },
    );
  }

  // Membuat Tombol Login
  Widget _buttonLogin() {
    return ElevatedButton(
      child: const Text("Login"),
      onPressed: () {
        var validate = _formKey.currentState!.validate();
        if (validate && !_isLoading) {
          _submit();
        }
      },
    );
  }

  Jika berhasil maka akan masuk ke halaman selanjutnya
  
2. Tambah Produk
   ProdukBloc.addProduk(produk: createProduk).then((value) {
  Navigator.of(context).push(
    MaterialPageRoute(
      builder: (BuildContext context) => const ProdukPage(),
    ),
  );
}, onError: (error) {
  showDialog(
    context: context,
    builder: (BuildContext context) => const WarningDialog(
      description: "Simpan gagal, silahkan coba lagi",
    ),
  );

penjelasan:
ProdukBloc.addProduk: Memanggil metode addProduk dari ProdukBloc untuk menambahkan produk baru ke database atau sumber data lainnya.
then: Jika penambahan berhasil, pengguna akan dinavigasi kembali ke halaman ProdukPage yang menampilkan daftar produk.
onError: Jika terjadi kesalahan selama penambahan, akan ditampilkan dialog peringatan dengan pesan "Simpan gagal, silahkan coba lagi".

3. Tampil Data
   // ignore: must_be_immutable
class ProdukDetail extends StatefulWidget {
  Produk? produk;

  ProdukDetail({Key? key, this.produk}) : super(key: key);

  @override
  _ProdukDetailState createState() => _ProdukDetailState();
}

penjelasan : ProdukDetail adalah widget stateful yang menampilkan detail sebuah produk.
produk: Properti opsional yang menerima objek Produk. Digunakan untuk menampilkan informasi produk spesifik.
@override createState: Membuat state untuk widget ini, yaitu _ProdukDetailState.


----------------------
Simpan dan delete
Widget _tombolHapusEdit() {
  return Row(
    mainAxisSize: MainAxisSize.min,
    children: [
      // Tombol Edit
      OutlinedButton(
        child: const Text("EDIT"),
        onPressed: () {
          Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => ProdukForm(
                produk: widget.produk!,
              ),
            ),
          );
        },
      ),

      // Tombol Hapus
      OutlinedButton(
        child: const Text("DELETE"),
        onPressed: () => confirmHapus(),
      ),
    ],
  );
}

Penjelasan : OutlinedButton (Edit):
Label: "EDIT".
onPressed: Navigasi ke halaman ProdukForm dengan membawa data produk yang ingin diedit.
OutlinedButton (Delete):
Label: "DELETE".
onPressed: Memanggil metode confirmHapus() untuk menampilkan dialog konfirmasi penghapusan.


-----------------
ProdukBloc.deleteProduk(id: widget.produk!.id!).then(
  (value) {
    Navigator.of(context).push(
      MaterialPageRoute(
        builder: (context) => const ProdukPage(),
      ),
    );
  },
  onError: (error) {
    showDialog(
      context: context,
      builder: (BuildContext context) => const WarningDialog(
        description: "Hapus gagal, silahkan coba lagi",
      ),
    );
  },
);

deleteProduk: Metode dalam ProdukBloc yang bertanggung jawab untuk menghapus produk dari database atau sumber data.
then: Jika penghapusan berhasil, pengguna akan dinavigasi kembali ke halaman daftar produk (ProdukPage).
onError: Jika terjadi kesalahan selama penghapusan, akan menampilkan dialog peringatan (WarningDialog) dengan pesan "Hapus gagal, silahkan coba lagi".

