**Menu Dan Promo**

Aplikasi ini digunakan untuk simulasi pembelian makanan/minuman yang sederhana dengan menggunakan Voucher/Promo.

**Fungsi**

- Pengguna dapat melihat daftar menu makanan, minuman, dan voucher atau promo 
- Pengguna dapat memasukkan atau menghapus list makanan, minuman, dan voucher atau promo
- Pengguna hanya dapat menggunakan satu voucher
- Pengguna dapat melihat total harga beserta potongannya

**How Does it works?**

Aplikasi simulasi ini mengguankan 4 buah model dan 3 buah controller yang berfungsi agar program tersebut bisa dijalankan

Fungsi pada beberapa kode:

`Penawaran.xaml.cs` digunakan untuk menampilkan daftar makanan minuman dalam listbox

#
private void generateContentPenawaran()
        {
            Item coffeLate = new Item("Coffe Late", 30000);
            Item blackTea = new Item("BlackTea", 20000);
            Item milkShake = new Item("Milk Shake", 15000);
            Item watermelonJuice = new Item("Watermelon Juice", 25000);
            Item lemonSquash = new Item("Lemon Squash", 30000);
            Item pizza = new Item("Pizza", 75000);
            Item friedRice = new Item("Fried Rice Special", 45000);

            Penawarancontroller.addItem(coffeLate);
            Penawarancontroller.addItem(blackTea);
            Penawarancontroller.addItem(milkShake);
            Penawarancontroller.addItem(watermelonJuice);
            Penawarancontroller.addItem(lemonSquash);
            Penawarancontroller.addItem(pizza);
            Penawarancontroller.addItem(friedRice);

            listPenawaran.Items.Refresh();
        }

`PilihVoucher.xaml.cs` Untuk menampilkan daftar voucher dalam list box
#
private void generateListVoucher()
        {
            Model.Voucher awalTahun = new Model.Voucher(title: "Promo Awal Tahun Diskon 25%", discInPercent: 25);
            Model.Voucher tebusMurah = new Model.Voucher(title: "Promo Tebus Murah Diskon 30% atau max. 30.000", discInPercent: 30);
            Model.Voucher promoNatal = new Model.Voucher(title: "Promo Natal Potongan 10000", disc: 10000);

            voucherController.addItem(awalTahun);
            voucherController.addItem(tebusMurah);
            voucherController.addItem(promoNatal);

            DaftarVoucher.Items.Refresh();
        }

`MainWindow.xaml.cs` Digunakan untuk inisialisasi dan membuat beberapa instance untuk digunakan kedalam list
#
public MainWindow()
        {
            InitializeComponent();

            payment = new Payment(this);

            KeranjangBelanja keranjangBelanja = new KeranjangBelanja(payment, this);

            controller = new MainWindowController(keranjangBelanja);

            listBoxPesanan.ItemsSource = controller.getSelectedItems();
            listBoxPakaiVoucher.ItemsSource = controller.getSelectedVouchers();

            initializeView();
