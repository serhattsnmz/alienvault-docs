## Kolerasyon Yazılması

- Ossimde korelasyon kuralı oluşturmak için Web arayüzünden `Configuration >> Threat Intelligence >> Directives` sekmesi açılarak `New Directive` butonuna basılır.

- Korelasyonun için isim yazılır ve Intent, Stragegy, Method ve Priority değeri belirlenir.

<p align="center">
    <img src="assets/21.png" style="max-height:450px">
</p>

- Korelasyonu tetikleyecek olan ilk kuralın ismi yazılır.

<p align="center">
    <img src="assets/22.png" style="max-height:450px">
</p>

- Event tipi seçilir.

<p align="center">
    <img src="assets/23.png" style="max-height:450px">
</p>

- İlgili alt event seçilir

<p align="center">
    <img src="assets/24.png" style="max-height:450px">
</p>

- Kaynak ve hedef adresler belirlenir.

<p align="center">
    <img src="assets/25.png" style="max-height:450px">
</p>

- Reliability değer seçilir.

**NOT!** : AlienVaultta risk hesaplaması `priority * reliability * asset_value / 25` olarak hesaplanır. Sonuç 1 ‘den büyükse alarm üretilir.

- Risk kategorileri :
    - 0,1,2 = Low
    - 3,4 = Precaution
    - 5,6 = Elevated
    - 7,8 = High
    - 9,10 = Very High

<p align="center">
    <img src="assets/26.png" style="max-height:450px">
</p>

- Finish butonuna tıklanarak ilk kuralın oluşturulması tamamlanır.

<p align="center">
    <img src="assets/27.png" style="max-height:450px">
</p>

- İlk kural oluştuktan sonra oluşması beklenen ikinci kuralı tanımlamak için Action sekmesindeki + butonuna tıklanır.

<p align="center">
    <img src="assets/28.png" style="max-height:450px">
</p>

- İkinci kuralın adı girilir.

<p align="center">
    <img src="assets/29.png" style="max-height:450px">
</p>

- Event tipi seçilir.

<p align="center">
    <img src="assets/30.png" style="max-height:450px">
</p>

- İlgili alt event seçilir

<p align="center">
    <img src="assets/31.png" style="max-height:450px">
</p>

- Kaynak ve hedef adresler seçilir. Bir önceki kuraldaki kaynak ve hedef ile eşleşmesi isteniyorsa “From a parent rule” kısmından aşağıdaki görüntüdeki gibi seçim yapılır.

<p align="center">
    <img src="assets/32.png" style="max-height:450px">
</p>

- Reliability değeri seçilir.

<p align="center">
    <img src="assets/33.png" style="max-height:450px">
</p>

- Kuralın oluşturulması tamamlanır.

<p align="center">
    <img src="assets/34.png" style="max-height:450px">
</p>

- İlk kural oluştuktan sonra ikinci kuralın oluşması için beklenilecek süre belirlenir.

<p align="center">
    <img src="assets/35.png" style="max-height:450px">
</p>

- İlk kural oluştuktan sonra ikinci kuralın kaç kez oluşması gerektiği belirlenir.

<p align="center">
    <img src="assets/36.png" style="max-height:450px">
</p>

- İşlemler tamamlandıktan sonra “Restart Server” butonuna basılır. (restart etmeden önce “test directives” butonuna basarak oluşturduğunuz korelasyok kurallarında hata olup olmadığını test edebilirsiniz.)


<p align="center">
    <img src="assets/37.png" style="max-height:450px">
</p>
 

#### Kuralın Test Edilmesi

- `Analysis >> Alarms` bölümünden  oluşan alarmlar takip edilir.

- İlk kuralın tetiklenmesi sağlanır. (nmap ile tarama yapılarak oluşturulabilir)

- İlk tarama sonrası alarmın oluştuğu ve risk seviyesinin 1 olduğu gözlemlenir.

<p align="center">
    <img src="assets/38.png" style="max-height:450px">
</p>

- 1 dakika içerisinde 2 adet başarısız ssh erişimi aktivitesi yapılarak korelasyonun çalışması ve risk değerinin 2 ‘ye yükselmesi gözlemlenir.

<p align="center">
    <img src="assets/39.png" style="max-height:450px">
</p>

- Ayrıca yapılan bu işlemlerin tamamına Analysis >> SIEM bölümünden ulaşılabilir.

<p align="center">
    <img src="assets/40.png" style="max-height:450px">
</p>