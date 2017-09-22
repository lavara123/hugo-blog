+++
date = "2017-09-19 19:55:00"
draft = false
title = "C++ Pointers (Göstericiler)"
tags = ["C++", "Pointers"]
categories = ["C++"]
+++
## Pointer
Kısaca bir hafıza hücresinin ADRESİNİ tutmak için kullanılan değişkenlerdir. Adrsini tuttuğumuz alanda her türlü değişikliği yapabiliriz yani o adresteki veriyi çekebilir veya değiştirebiliriz.
gösterici olduğunu bildiren işaret: <span style="color:green">*</span>

>Tek bir adres 1 byte lik bir alana sahiptir.


Kullanımı:
```C++
tür* isim;
```

Örnek:
```C++
int dene = 15;
int deg = 10;

int* po = &dene;
```

yukarda dene değişkeni için için hafızada 4 byte lik bir alan bulunur ve dene o alana tahsis edilir artık orayı derleyici int olarak kabul eder.

<span style="color:green">int* po</span> dediğimizde derleyici int türünden olduğu için hafızada 4 byte lik bir alan arar ve bulduğunda orayı 4 bytlik adres tutan bir alan kabul eder.

<span style="color:green">&</span> işareti bir değişkenin soluna konduğunda o değişkenin tutulduğu adresini bize verir ve bu adresi göstericiler tutabilir.

<span style="color:green">&dene</span> dediğimiz o değişkenin adresini verir yani:

```C++
// çıktısı '0028F960' gibi bir bellek adresi
cout << &dene;
```

& işareti olmadan yapsaydık o adrsteki veriyi bize getirecekti yani:
```C++
// çıktısı: 15
cout << dene;
```

yukardakini biz göstericimizle göstermek işteseydik:
```C++
// çıktısı: 15
cout << *po;
```

gördüğümüz gibi artık `po` göstericimiz `dene` değişkeninin adresini tutuyordu yani `dene` değişkenine istediğini yapar

gelin birde `po` göstericimizle `dene` değişkeninin parametresini değiştirelim:
```C++
*po = 256;

cout << "dene..: "  << dene << endl; // 256

cout << "*po..: " << *po << endl; //256
```

gördüğümüz gibi `dene` değişkenin parametresini değiştirdik

hafızada nasıl olduğu:
![text](http://i.hizliresim.com/El3VRz.png "")

yukarda derleyici Örnek kodumuz için:

*   Derlenme yukardan aşağıya olur
*    ilk önce deneye hafıza adrestlerinden küçükten büyüğe doğru bir tarama yapar ve 4 byte lik uygun bulduğu yere dene değişkenini yerleştir.
*   sonra po göstericisine gelir po int türünden bir gösterici olduğu için 4 bytelik bir alana yerleştirir

yukardaki bu yerleştirmeler stack(yığın) hafıza alanında gerçekleşir bu hafıza yerleştirme türü derleyicinin kontrolündedir ilerde daha ayrıntılı anlatacağım stack ve heap hafıza alanlarını

şimdi bir örnek yapalım
bir fonksiyonla main içindeki 2 değişkeninin parametreleri yer değiştirsin.
```C++
#include <iostream>

using namespace std;

//yer değiştirmeyi yapacak fonksiyonumuz
void degistir(int* a, int* b)
{
    // geçici bir değişken oluşturduk ve
    // a göstericisinin tuttuğu adresteki veriye eşitledik
    int temp = *a;
    
    // b göstericisinin tuttuğu adrsteki degeri a göstericisinin degerine eşitledik
    *a = *b;
    
    // tem içindeki değeri b göstericisine eşitledik
    *b = temp;
}

int main()
{
    int sayi1 = 15;
    int sayi2 = 34;

    cout << ":..degistir fonksiyonundan once..:" << endl;
    cout << "sayi1..: " << sayi1 << endl;
    cout << "sayi2..: " << sayi2 << endl;
    
    degistir(&sayi1, &sayi2);
    
    cout << "\n:..degistir fonksiyonundan sonra..:" << endl;
    cout << "sayi1..: " << sayi1 << endl;
    cout << "sayi2..: " << sayi2 << endl;

    system("PAUSE");
    return 0;
}
```

yukarda sayi1 in degeri 15 sayi2 nin degeri 34'tü degistri fonksiyonundan sonra sayi1'in degeri 34 sayi2'nin degeri 15 oldu.