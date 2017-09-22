+++
date = "2017-09-22 22:30:00"
draft = false
title = "C++ Pointers (Göstericiler) -2-"
tags = ["C++", "Pointers"]
categories = ["C++"]
+++

Şimdi de Dizilerde işaretçi kullanımını görelim:
```C++
#include <iostream>

using namespace std;

int main()
{
    int dizi[] = { 10, 20, 30, 40, 50 };

    // po işaretçimiz dizi'nin adresini gösteriyor
    int *po = dizi;

    // po'nun gösterdiği adresteki verileri ekrana yazdırıyoruz

    for (int i = 0; i < 5; i++)
        cout << po[i] << endl;

    system("PAUSE");
    return 0;
}
```


**Yukardaki Kodları Sırayla Açılayalım**

```C++
int dizi[] = { 10, 20, 30, 40, 50 };
```
*   Yukarda "dizi" adında int türünden bir dizi oluşturuyoruz bu dizinin içindeki elemanlar otomatik olarak aşağıdaki gibi "dizi" ye atanıyor

```C++
dizi[0] = 10;
dizi[1] = 20;
dizi[2] = 30;
dizi[3] = 40;
dizi[4] = 50;
```
yukardakilerin stack hafızada 20 bytelik bir alan kaplar bu alanı bir 5 katlı bir dolaba benzetelim dolabın en üst katında dizi[0] en alt katında dizi[4] vardır yani:
![text](http://i.hizliresim.com/XW9gQ7.png "")

yukarda görüldüğü gibi derleyici sıralı bir şekilde stack hafızada "dizi" yi yerleştirmiş bir önceki konuda demiştim değişkenlerimizi tanımladığımızda o değişkenleri derleyici stack hafızada yerleşimini yapar yani derleyicinin elindedir ne zaman bizim elimizde olur derseniz onu ileri konuda anlatmayı düşünüyorum.

>adresler niye 4'er 4'er artmış derseniz int DÖRT byte'lik bir tam sayı değişkenidir bir önceki konuda ne demiştim "tek bir adres 1 byte'lik alana sahiptir" bu durumda int'in saklanması için 4 adres alanı işgal edilecek ama o int çağrılırken 4 adresinden ilk adresi ile çağrılacak.


```C++
int* po = dizi;
```
*   Yukarıda po adında int türünden bir gösterici tanımladık ve bu göstericiye "dizi" yi eşitledik yani ne dedik "po sen git ve dizi'yi kontrolun altına al" bu durumda noluyor biz "dizi" nin her elemanına ulaşabiliyoruz ve onları değiştirebiliyoruz koddan ayrı bir örnek verelim:
mesela napsın gitsin dizi[3]'ü değiştirsin dizi[3]'te parametre olarak 40 vardı.

```C++
po[3] = 54;
cout << "dizi[3]..: " << dizi[3] << endl;
cout << "po[3]..: " << po[3] << endl;
```
yukarda gördüğünüz gibi po "dizi" yi gösterdiği için po[3]'e parametre atandığında dizi[3]'e atanmış oluyor yani dizi[3] artık 40 değil 54 olmuştur.

>po 4 byte'lik bir alanda durur o nun işi sadece göstermektir yani "dizi" toplam 20 byte alanda diye po'da 20 bytelik bir alandadır diye düşünmeyelim po anlık iş yapar yani bi nevi garson gibi bi o masya gider bi bu masaya


```C++
for(int i = 0; i < 5; i++)
        cout << po[i] << endl;
```
*   yukarıda for için i'yi 0'a eşitlemişiz; koşul olarak i küçük olduğu sürece 5'ten; i'yi 1 arttır
sonra po[i]'leri ekrana yazdır demişiz yani po neyi gösteriyordu dizi'yi bu durumda ne olması lazım:

```C++
10
20
30
40
50
```


>aşağıdaki kodlarda değişime uğramadan gidiyor gibi düşünün

```C++
po++;
```
*   böyle bi şey dediğimizde po nun gösterdiği ADRES 4 artar(neden 4 çünkü po int türünden) artık po dizi[1] gösterir yani gelip po[0]'ı ekranda göstermek istediğimizde ekrana dizi[1]'deki parametre çıkar
dize[0]'a po--; kulanmadığımız sürece erişme şansımız yoktur.



```C++
(*po)++;
```
*   böyle bi şey dediğimizde po nun gösterdiği adresteki VERİYİ 1 arttırır yani dizi[0]'daki değer 1 artar.

bir örnekle bu yazıyı bitirelim:

<span style="color:green">main içindeki iki dizi'yi yer değiştirsin yani dizi1'dekiler dizi2'ye dizi2'dekiler dizi'e geçsin:</span>
```C++
#include <iostream>

using namespace std;

void Hallet(int* d1, int* d2)
{
    int temp[5];

    for(int i = 0;i < 5;i++)
        temp[i] = d1[i];

    for(int i = 0;i < 5;i++)
        d1[i] = d2[i];

    for(int i = 0;i < 5;i++)
        d2[i] = temp[i];
}

int main()
{
    int dizi1[] = {10, 20, 30, 40, 50};
    int dizi2[] = {100, 200, 300, 400, 500};

    cout << "Hallet() Fonksiyonundan Once dizi1[]..: " << endl;
    for(int i = 0;i < 5;i++)
        cout << dizi1[i] << endl;

    cout << "\nHallet() Fonksiyonundan Once dizi2[]..: " << endl;
    for(int i = 0;i < 5;i++)
        cout << dizi2[i] << endl;

    Hallet(dizi1, dizi2);
    cout << endl;

    cout << "\nHallet() Fonksiyonundan Sonra dizi1[]..: " << endl;
    for(int i = 0;i < 5;i++)
        cout << dizi1[i] << endl;

    cout << "\nHallet() Fonksiyonundan Sonra dizi2[]..: " << endl;
    for(int i = 0;i < 5;i++)
        cout << dizi2[i] << endl;

    system("PAUSE");
    return 0;
}
```
