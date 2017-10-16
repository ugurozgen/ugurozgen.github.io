---
layout: post
title:  "Effective Go"
date:   2017-09-22 08:44:01 +0300
categories: development golang 
published: true
---
Golang'i anlamak ve iyi bir Go kodu yazmak adına, Go'nun özelliklerini, deyimlerini, gelenek ve göreneklerini bilmek
önemlidir. Bu sayede diğer geliştiricilere temiz ve kolay anlaşılır bir program bırakmış oluruz.

##Format
`go fmt` tool'u herşeyi halleder rahatınıza bakın. "Hizalamayı" olayı tablarla halledilir ve bunu zaten `go fmt`
halleder. `Satır uzunluğu` yoktur. Go'da daha az `parantezler` vardır.

##Yorum
Golang `blok yorum(/**/)`ları ve `satır yorum(//)`larını destekler. Blok yorumları daha çok paketleri`(package)`
tanımlamak için yazılır.

`godoc` tool'u kaynak kodlari döküman olarak sunmaya yarar. Top-level tanımlamalardan önceki
yorumlar, ordaki maddeyi açıklamak için godoc tool'u tarafından kullanılır.

Her paketin `paket(*package*) yorumu` olmalı. Paketin altında birden fazla dosya olsa bile tek bir dosyaya yazılmalı ve
o paket hakkında giriş niteliğinde paketi bir bütün olarak tanıtmalı. Bu yorum *godoc* sayfasında ilk olarak gözükecek
ve takip eden ayrıntılı dökümanı oluşturacaktır.

Yorumlar düz metindir. *godoc* herhangi bir düzeltme yapmaz o yüzden cümle yapılarına, doğru yazım kurallarına,
noktalama işaretlerine ve cümle uzunluklarına dikkat edilmeli.

Paketteki her *export* edilen isimin önünde `doc comment` denilen döküman yorumu olması gerekir. *doc comment*'ler
*export* edilen isimle başlayıp tam bir cümle şeklinde özet niteliğindedir. Cümleye başlarken export edilen ismi
kullanırsanız bu arama yaparken daha net sonuçlar çıkarmanızı sağlar.
{% highlight bash %}
$ godoc regexp | grep -i parse
 Compile parses a regular expression and returns, if successful, a Regexp
    parsed. It simplifies safe initialization of global variables holding
    cannot be parsed. It simplifies safe initialization of global variables
{% endhighlight %}

Golang'e tanımlamaları gruplayıp onlara tek bir *doc comment* yazıp tanıtabiliriz.
{% highlight golang %}
//error codes
const(
    StatusOK = http.StatusOK
    BadRequest = http.BadRequest
)
{% endhighlight %}



