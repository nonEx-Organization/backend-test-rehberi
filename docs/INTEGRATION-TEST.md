### Integration Test
Integration test, kod birimlerinin birlikte test edilmesi ile yapılan testtir. Daha öncesinde birim testten bahsederken; test edilecek birimlerin (fonksiyonların), birbirlerinden izole edilmesini ve test esnasında bağımlılıkların yerini sahte bağımlılıklar ile değiştirmemiz gerektiğini belirtmiştim. Integration test, birimlerin doğru çalışmasına değil, birimlerin birbirleriyle olan bağımlılıklarının doğru çalışmasına bakar. **Yani integration test esnasında birim testleri kadar hata saptamayı beklememeliyiz.** Integration testler, bağımlılıkların testi olduğu için; geliştirme, çalıştırma zamanı ve sistem açısından maliyetli testlerdir. Bu nedenle bir integration test planlamasının detaylı bir şekilde QA Lead / Manager tarafından yapılması gerekir. [Bununla ilgili daha detaylı bilgilere bu bağlantıdan ulaşabilirsiniz](https://www.softwaretestinghelp.com/how-to-write-test-plan-document-software-testing-training-day3/). Ayrıca entegrasyon testi veri tabanı ve diğer servislerle etkileşim halindedir. Bunun anlamı; testler yapılmadan önce bir test ortamı oluşturulması gerekmektedir.   
Integration testler kompleksliğin yanında yeni yaklaşımlarda getiriyor. Bunlar:
- [Top-Down](#top-down)
- [Big Bang](#big-bang)
- Sandwich
- [Bottom-Up](#bottom-up)

![Integration Test Yaklaşımları](https://fortegrp.com/wp-content/uploads/2020/10/diagram-768x436.jpg)

#### Yaklaşımlar

##### Top Down

Henüz entegre edilmemiş alt seviye modüllerin davranışlarını simüle etmek için kullanılan bir yaklaşımdır. Bu testte, testler yukarıdan aşağı doğru gerçekleşir. Önce yüksek seviyeli modüller test edilir ardından düşük seviyeli modüller ve son olarak sistemin amaçladığı gibi çalıştığından eöin olmak için düşül seviyeli modüller yüksek seviyedekilere entegre edilir.

###### Avantajlar

- Modüller ayrı ayrı debug edilebilir.
- Çok az sayıda sürcü modül oluşturulması gerekir ya da hiç gerekmez.
- Tüm sistem göz önüne alındığında, daha tutarlı ve doğru sonuçlar verir.

###### Dezavantajlar

- Bir çok taslağa ihtiyaç duyar
- Alt seviye modüller yetersiz test edilir.

##### Big Bang

En basit integration test yaklaşımıdır. Basit bir anlatımla; sistemin tüm modülleri bir araya getirilir ve test edilir. Bu yaklaşım sadece çok küçük sistemler için uygundur. Test esnasında bulunan bir hatanın nereden kaynaklandığını tespit etmek; entegre edilen herhangi bir modülden kaynaklanabileceği için oldukça zordur. Bu nedenle hata ayıklamak oldukça pahalıdır.

###### Avantajlar

- Küçük sistemler için uygundur.

###### Dezavantajlar

- Tüm modüllerin entegre edilmesi gerektiği için uzun süre gecikme olacaktır.
- Tüm modüller aynı anda test edildiği için kritik modüller izole edilmez ve öncelikli olarak test edilmez.

##### Bottom Up

Bottom-Up yaklaşımında tüm modüller test edilene kadar, daha düşük seviyedeki her modül, daha yüksek seviyedeki modüllerle test edilir. Bu yaklaşımın birincil amacı, her bir alt sistemin, alt sistemini oluşturan çeşitli modüller arasındaki arayüzleri test etmektir. Bu test, uygun verileri sürmek ve alt seviye modüllere iletmek için test sürücülerini kullanır.

###### Avantajlar

- Bir kaç ayrık alt sistemin aynı anda test edilebilmesini sağlar.

###### Dezavantajlar

- Sürücü modülleri oluşturulmalıdır.
- Eğer sistemde çok fazla sayıda alt sistem bulunuyorsa, bu test yaklaşımında karmaşıklık oluşur.

#### Özellikler

- ***İleri aşamalarda çözülmesi maliyetli olacak hataların erken tespitini sağlar:*** Integration test geliştirmenin ilk aşamasında gerçekleşir ve bu nedenle sonraki aşamalarda düzeltilmesi maliyetli olacak hataların tespinin yapılması ve önlenmesini sağlar. Kod değişiklikleri sonrası Integration test yapılması önemlidir.
- ***Modüller arası bağımlılıkları denetler:*** Buna daha öncesinde [Integration Test](#integration-test) içerisinde değinildiği için tekrar etmiyorum.

#### Best Practices

1. ***Test verisine doğru karar verilmeli:*** Test verisine doğru karar vermek ilerleyen dönemlerde ilişkili yeni testlerin yazılması durumunda, verilerin tekrar kullanılabilmesi için önemlidir.
2. ***Test verileri doğru zamanda hazırlanmalı:*** Test verilerine, senaryoların yazılmasına paralele olarak ya da en azından yürütme öncesinde karar verilmesi gerekmektedir.
3. ***Kritik birimlere öncelik verilmeli:*** Test sırasında öncelik verilecek kritik birimler belirlenmelidir.
4. ***Önce Unit Test:*** Integration testi sadece geliştirici takımı unit testleri bitirdikten sonra başlatın.
5. ***Kritik unsurlar eksik bırakılmamalı:*** İş açısından kritik tüm unsurlar test esnasında ele alınmış olmalı.