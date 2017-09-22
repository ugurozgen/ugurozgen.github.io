---
layout: post
title:  "Golang Ducktyping"
date:   2017-09-22 08:44:01 +0300
categories: development golang 
published: true 
---

Ducktyping dinamik dillerde kullanılan bir terimdir. Amaç; herhangi bir objedeki var olan herhangi bir metodu invoke edebilmen için bir tipe ihtiyaç olmamasıdır. Metot objede tanımlanmışsa onu invoke edebilirsin. Bu  
> 
  Eğer bir ördek(duck) ördek gibi görünüyorsa ve ördek gibi vak vaklıyorsa, ördektir. 

ifadesinden gelmektedir.

Bu sayede bir interface'i deklaratif olarak implement etmek zorunda kalmazsınız. 

{% highlight golang %}
//yanlış kullanım
type Otomobil implements Arac
{% endhighlight %}

Eğer `Arac` diye bir interface var ise ve bu interface'in her metodu ayrı bir type da da mevcutsa, örneğin `Motosiklet` type'ı, bu; zaten `Motosiklet` type'ının da aynı zamanda bir `Arac` olduğunu gösterir. Bunu yukardaki gibi deklaratif olarak belli etmemize gerek yok.

{% highlight golang %}
type Arac interface{
  Hizlan()
}

type Motosiklet struct{}

func (m Motosiklet) Hizlan() {
  fmt.Println("hizlandi")
}

func main() {
  var motosiklet Motosiklet
  araciHizlandir(motosiklet)
}

func araciHizlandir(arac Arac) {
  arac.Hizlan()
}

// çıktı: hizlandi
{% endhighlight %}
[go playground'da git](https://play.golang.org/p/pDA7ruoefk)

Yukarıdaki örneğe bakacak olursak, `araciHizlandir` fonksiyonu `Arac` type'ından bir parametre bekliyordu fakat biz ona `Motosiklet` type'ından bir parametre geçtik ve sorunsuz çalıştı. Bu demek oluyor ki; aslında `Motosiklet` type'ı da bir `Arac`tır ve biz bunu kodta hiç belirtmedik.

Peki bunu Golang nasıl ve ne zaman anladı ve bunun faydası nedir?

Golang bunu çalışma zamanında algılayıp dinamik olarak bağladı. Bu sayede static dillerin derleme zamanında yaptığı deklare edilmiş type bağlamarını golang çalışma zamanında yapıp derleme süresini düşürdü. 
