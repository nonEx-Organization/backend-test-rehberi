![e2e-test](https://cdn-media-1.freecodecamp.org/images/l0ZO6o8ovUKrS5GgoqrXlNPFbX5dDfDWkgmj)

### e2e Test

e2e Test; bir uygulamanın başlangıçtan-bitişe olan akışını test eder. Bu testin temel amacı, sistem ve veri bütünlüğünün doğrulanması için gerçek kullanıcı senaryolarının çoğaltılmasıdır. Test, uygulamanın donanım, ağ bağlantısı, dış bağımlılıklar, veritabanları ve diğer uygulamalarla nasıl iletişim kurduğunu test etmek için uygulamanın gerçekleştirilebileceği her işlemi kapsar. Basit bir senaryo ele almak gerekirse; kullanıcının, uygulamaya giriş yapması ve yeni gelen bir maili açması birer test örneğidir. e2e testler (yaygın olarak) manuel şekilde yapılsada, otomatize şekilde de yapılabilir. Şuan da bir Backend API`ın testi üzerine konuştuğumuz için elimizde e2e testi gerçek kullanıcı senaryosunu bire bir canlandırabileceğimiz UI bulunmuyor. Bu nedenle otomatize yapılan e2e testleri üzerinde duracağız. (e2e testlerin UI'a sahip uygulamalarda da otomatize gerçekleştirilebileceğine dair kaynaklar mevcut lakin QA engineer olmadığım için bu konuya değinmeyeceğim).

![yaklaşımlar](https://static1.smartbear.co/smartbear/media/images/landingpages/testcomplete/end-to-end-graphic.png)

#### Yaklaşımlar

##### Horizontal e2e

Yatay yaklaşım oldukça yaygın bir yaklaşımdır. Yatay testler kullanıcının bakış açısını varsayarak sistemde güven oluşturabilir. Yatay yaklaşımda, kullanıcının uygulama içerisinde gezinip gezinemediği test edilir. İşlemlere bağlı alt işlemlerin doğru bir şekilde yapılıp yapılmadığından emin olunur. Örnek olarak bir e-ticaret uygulamasında ürün satın alınırken aynı anda ödeme işlemlerininde doğru bir şekilde yapıldığından emin olmak gibi.

##### Vertical e2e

Yatay yaklaşımın aksine dikey yaklaşım, uygulama içerisindeki katmanların ayrı ayrı test edilmesi ile yapılır. Yukarıda bulunan e-ticaret uygulaması üzerinden konuşursak, ürün satınalma ve ödeme işlemleri dikey yaklaşımda ayrı ayrı test edilir. 

> Vertical ve Horizontal yaklaşımları hakkında daha fazla bilgi edinmek için [bağlantıya](https://dzone.com/articles/what-is-end-to-end-testing-1) tıklayabilirsiniz.

#### Best Practices

***Kodsuz test otomasyonlarını kullanabilirsiniz:*** Unit yada integration testleri kod tabanlı testlerdir. [testim.io](https://www.testim.io/) gibi, uygulamanızı kod yazmadan test edebileceğiniz servislerden faydalanabilirsiniz. Otomasyonlar, geliştiricilere geri dönüş zamanını kısaltırken, uygulama geliştirme sürecini hızlandırmaktadır.

***Test öğlereini akıllı (kararlı) seçin:*** Öğlerin asenkron olarak yüklenmesi bir çok modern web uygulamasında bulunan bir özellik. Bu durum otomatize bir e2e testin henüz var olmayan bir öğeye erişmesine ve hata oluşturmasına sebep olabilir. Bunu engellemek izlenebilecek yollardan biri erişilmek istenen öğenin varlığını kontrol edip, öğeye erişene kadar beklenebilir.

***Exception testinden kaçının:*** e2e Testleri yaygın kullanıcı senaryolarını test etmek için yapılır. Exception testlerini integration ve unit testlerde yapmalısınız.

***Riske dayalı testlerden yararlanmalısınız:*** Test yaklaşımınızı uygulamaya başladığınızda her şeyi test etmek isteyebilirsiniz. Başlangıçta mantıklı gelen istek yerine daha efektif test yazmak için izleyebileceğiniz bir yaklaşım bulunmakta **Risk-Based Testing**. Tamamen ayrı bir QA konusu olduğu için bu başlığa rehber içerisinde değinmeyeceğim.

***Her zaman kullanıcıyı düşünmelisiniz:*** e2e Testi kullanıcı senaryoları üzerine yapılan bir test türüdür. Bu yüzden daima kullanıcı bazlı düşünmeli ve senaryoları kullanıcılara uygun olarak oluşturmalısınız.

|Integration Test|e2e Test|
|---|---|
|Uygulama birleşenlerinin doğru bir şekilde çalıştığından emin olur. |Ürünü bir kullanıcı olarak test eder |
|Birden çok bileşeni kapsayabilir ama tüm bileşenleri kapsamaz|Test kapsamı daha geniştir ve tüm uygulamayı kapsar|
|Birlikte çalışan bileşenler arası hataları tespit etmek için yapılır|Kullanıcı deneyimi hakkında fikir sahibi olmak için yapılır|
|Uygulaması daha az maliyetlidir|Uygulaması daha çok maliyetlidir|