### Unit Test

Unit test, kodların "birim-birim" test edilmesidir. Bir birime verilen input sonucunda beklenen outputun alınıp alınmadığı test edilir. Anlatmak istediğim; birim testinin amacı sadece bir fonksiyonu test etmektir. Peki ya fonksiyon içerisinde fonksiyon çağırılıyorsa ?  
Bir backend uygulaması geliştirilirken elbette tek fonksiyon tüm işleri kapsamaz (db erişimi, validation vs.). Bunun için kodlar katmanlara bölünür. nonAsk için db erişimi, business logic, controller ayrı ayrı katmanlardır ve birbirlerini çağırırlar. Fakat bu, bir birim üzerinde çalışacağınız gerçeğini değiştirmiyor. Unit testlerde metot içerisinde çağırılan fonksiyonlar dışlanmalıdır. Bunu yapmanın yolu tabikide çağırılan metodu silmek değil, **çağırılan fonksiyonları sanki beklenen sonucu veriyormuş gibi sahteleştirilmektir.** Çağırılan metod (Jest için spyOn objesi ile) mock bir metoda dönüştürülür ve her zaman beklenen sonucu verecek şekilde konfigüre edilir, kısaca **bağımlılıklarından izole edilir** ve **sadece birim fonksiyona test yapılmış olur.**.

#### Özellikler
- ***Birime oluşan hataları saptar:*** Unit testleri, birimlerin izole edilmesiyle (bağımlılıkların kesinlikle doğru çalıştığı varsayımı ile yapılan) yapılan testlerdir. Bu nedenle, **sadece tek birime odaklanır ve tek birimdeki hataları saptar.** bu endpointe gelen bir istekte; bağımlılıkların tek tek debug edilmesi yerine seçilebilecek iyi bir yoldur.
- ***Kod karmaşasını saptar, kaliteyi artırır:*** Unit testi yapılacak birim eğer karmaşa içerisindeyse, [(spagetti kod)](https://medium.com/@mcccccc/be-careful-with-spaghetti-code-6260d77f2950) testi yazmak bir çileye dönüşecektir. **kötü kod zor test edilir.** Bunun nasıl mümkün olduğunu [Best Practice](#best-practice) bölümünde ele aldığımız "Cyclomatic Complexity" de kavrayacaksınız.
- ***Özellik ekleme / çıkarma durumunda hataları önler:*** Testler birimlere yapıldığı için özellik ekleme / çıkarma durumlarında hatanın tespiti kolay yapılır ve koruma sağlar.
- ***Kod yazma hızını artırır:*** Bütün bir uygulama 1 birimdeki 1 hata neticesinde crash olabilir. Birimlere yapılan testler sayesinde **uygulamanın crash olması beklenmeden, hatanın oluştuğu kod bloğu hızlı bir şekilde tespit edilebilir**. Debug süresinin çok daha küçük bir oranında vaktinizi alacak test yazma süresi, kod yazma hızını büyük oranda artırır.  
> Yapılan araştırmalara göre unit testler; production`da ki ürünün hata oranını %40 - %80 azaltıyor.

#### Best Practices
1. ***Testler yavaş olmamalı:*** Mocha 75 ms`den uzun süren testleri yavaş olarak kabul eder. Eğer testler yavaş olursa; geliştiricinin testleri çalıştırması gerekenden daha az çalıştırmasına sebep olur. Bu da testin amacını zedeler. Testlerin hızını aşağıdaki 3 yöntem ile artırabilirsiniz:
   - Testleri basit tutarak,
   - Diğer testlere bağımlılık oluşmasını engelleyerek,
   - Mock ile bağımlılıkları izole ederek.
2. ***Testler basit olmalı:*** Testlerin basit olması gerektiğini 1. maddede belirtmiştik ama, basitlik kıstasımızı belirtmemiştik.Ne yazık ki, testler göz ve izan ile basit tutulmuyor. Bunun için bir tanımımız var: [Cyclomatic Complexity (Döngüsel Karmaşıklık)](https://blog.ploeh.dk/2019/12/09/put-cyclomatic-complexity-to-good-use/). Cyclomatic complexity, sizin algoritmanızın karmaşıklığını ölçen bir kod metriğidir. Aynı zamanda sizin **en az** kaç farklı kombinasyonda teste ihtiyaç duyacağınızı hesaplamanıza yardımcı olur. Yani eğer cyclomatic complexity = 4 ise bunun anlamı sizin en az 4 adet unit test yazmanız gerekiyor.  
Neden en az ? Fonksiyonlarınızın spesifik durumlarda ekstradan teste tabi tutulması gerekebilir. Döngüsel karmaşıklık sayısı kadar test yazdığınızda fonksiyonunuz sağlıklı bir şekilde test edilsede, fonksiyon içerisinde bulunan spesifik bir durum beklenmedik sonuçlara neden olabilir. 

**Unit testin faydalarında kod karmaşasını saptadığını yazmıştık. Bunun temelinde yine cyclomatic complexity** yatıyor. Cyclomatic complexity sizin daha insalcıl kodlar yazmasınızı sağlar. Eğer yazdığınız kodun karmaşası 10`dan küçükse bu temiz ve insancıl bir algoritmanızın olduğu anlamına gelir. Bazı geliştiriciler bu değerin 6 +- 2 olması gerektiğini düşünüyork. Yinede biraz merhamet edip 10 değerini baz aldığımızda, test yazmak (üstüne spesifik durumlarda dahil olursa) işkence haline gelecektir.
  

[Sayfa 3 - Test Tipleri](./TEST-TIPLERI.md)
[Sayfa 5 - Integration Test](./INTEGRATION-TEST.md)