---
layout: post
title: ListView'e Bir Örnek
---
## ListView 

Bu örnekte içinde öğrencilerin bulunduğu listemiz olacak, herbir öğrencinin isim, soyisim ve okul ismi listView içerisinde ayrı satırlarda görüntülenecek.

1. Öncelikle varsayılan ayarlarda bir proje oluşturalım ve activity_main.xml içerisine bir ListView ekleyip id olarak 'myList' verelim.
2. MainActivity.java sınıfımızdaki onCreate() metodu içerisinde az önce oluşturduğumuz myList adındaki ListView öğemizi findViewById() yardımıyla çekelim.
3. MainActivity.java sınıfının bulunduğu düzeyde 'Ogrenci' adında bir sınıf oluşturalım. Bu sınıfta öğrencinin yapısını oluşturacağız. String tipinde isim, soyisim ve okul değişkenleri oluşturalım. Ardından sınıfa ait bir constructor oluşturalım(Sağ tık > Generate > Constructor > tüm değişkenler seçili). Constructor'dan yine Generate üzerinden değişkenlerimize ait Getter-Setter metodlarını otomatik olarak oluşturalım. En son olarak bize listView a çekmek için örnek birkaç öğrenci lazım. Gerçek hayatta bu datayı veritabanından veya json yapılarından çekeriz ancak burada örnek amaçlı kendimiz oluşturalım. ArrayList<Ogrenci> yapısında bir sampleData() metodu oluşturalım. Bu metod bize yine kendi içinde oluşturacağımız örnek ögrencilerin listesini döndürecek.
4. Mantıken listemizin her satırı birbiriyle aynı tasarıma sahip olacak, ancak  her bir satırın içerisindeki öğeler birbirlerinden farklı değerlere sahip olacak. O zaman ListView içerisindeki satırlara ait sabit bir tasarım kalıbı oluşturalım. ~res/layout/ içerisinde yeni bir 'Layout resource file' oluşturalım ve adına 'list_row' verelim.
5. list_row.xml içerisinde satırımızda neler bulunmasını istiyorsak o öğeleri istediğimiz düzende yerleştirmemiz gerekiyor. En başta belirttiğimiz gibi içerisinde öğrenciye ait isim, soyisim ve okul ismi yanyana sıralı halde bulunacak bizim satırlarımızın. Buraya üç adet TextView ekleyelim ve id'lerini nameText, surNameText ve schoolText olarak verelim. Yanyana gelecek şekilde hizaya getirelim(orientation:horizontal). list_row ile işimiz bitti.
6. Az önce oluşturduğumuz sampleData() metodundan gelecek olan ArrayList'i MainActivity.java içerisinde kullanacağız. Bunun için MainActivity içerisinde ArrayList<Ogrenci> tipinde bir liste oluşturalım ve Ogrenci.sampleData(); metoduna eşitleyelim(Örneğin ismi 'ogrenciler' olsun).
7. Artık geriye kalan tek şey CustomAdapter adındaki adapter sınıfımızı oluşturup kullanacak hale getirmek. Bu sınıfımız BaseAdapter sınıfına extends edecek. En başta Context tipinde bir context değişkeni oluşturuyoruz. Daha sonra bir constructor oluşturuyoruz. BaseAdapter'den override etmemiz gereken 4 adet metod var. Bunlar getCount(), getItem(), getItemId() ve getView() metodları. Bu metodlardan biraz bahsedelim:
getCount(): ListView içerisinde gösterileccek satır sayısını döndürür. Genelde elimizdeki listenin boyutu kadar döndürülür.
getItem(): O anda satıra yansıyan liste öğresini döndürür.
getItemId(): O anda satıra yansıyan liste öğesinin id'sini döndürür.
getView(): Bu metod aslında tüm adaptörün işlevinin görüldüğü yerdir. Örnek listemizin View yapısını alıp içinde değişiklikler yapıp tekrar döndürmemize yarar. Daha basit anlatacak olursak, list_row.xml de oluşturduğumuz satır yapısını burada çekeriz, içini örnek bilgilerimizle doldurup döndürürüz.
8. getView() metoduna gelelim ve bir adet View tipinde myView değişkeni oluşturalım. Ogrenci sınıfımızdan myOgrenci nesnesi oluşturalım. Bu nesne bizim örnek datamızdan gelecek olan listenin içindeki öğrencileri tek tek alıp myView'a atmamızı sağlayacak. Bunun için şu kod parçası işe yarayacaktır:

```java
myOgrenci = ogrenciler.get(position);
```

Şimdi de list_row.xml satırımızı inflate etmemiz gerekiyor. Yani az önce oluşturduğumuz list_row yapımızı myView yapımıza aktarmamızı sağlayalım. Bunu da şu kod parçası ile yapıyoruz:

```java
LayoutInflater layoutInflater = LayoutInflater.from(myContext);
myView = layoutInflater.inflate(R.layout.list_row, null);
```
Artık geriye kalan işlemler basit. list_row'u myView öğesine aktarabildiğimize göre, önceden  list_row içinde oluşturduğumuz 3 adet TextView öğelerini findViewById metodu ile çekelim:

```java
TextView nameText = myView.findViewById(R.id.nameTextViewId);
TextView surNameText = myView.findViewById(R.id.surNameTextViewId);
TextView schoolNameText = myView.findViewById(R.id.schoolNameTextViewId);
```

Şimdi de bunların içini elimizdeki öğrencinin bilgileriyle doldurup en sonra myView'ı döndürelim:

```java
nameText.setText(myOgrenci.getName());
surNameText.setText(myOgrenci.getSurName());
schoolNameText.setText(myOgrenci.getSchool());

return myView;
```

getView() metodu ile işimiz bitti. Aynı zamanda CustomAdapter sınıfımızı da halletmiz olduk.

9. Son işlemimiz ise onCreate() metodu içerisinde, az önce yazdığımız CustomAdapter'den bir nesne oluşturup myList isimli listemize setAdapter() metodu ile uygulamak.

```java
CustomAdapter customAdapter = new CustomAdapter(this);
myList.setAdapter(customAdapter);	
```

