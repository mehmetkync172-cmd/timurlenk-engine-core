# ELO ve Gerçek Oyun Gücü Doğrulama Planı

**Durum:** Plan / henüz yürütülmesi gereken araştırma  
**İlk taslak:** 16 Ekim 2026

Bu belge, gelecekteki güç ölçümleri için yöntemi sabitler. Mevcut sonuç değildir; bugün için Timurlenk'in mutlak veya dışarıyla karşılaştırılabilir ELO değeri **belirlenmiş değildir**.

## Neyi birbirinden ayıracağız?

1. **Fonksiyonel doğruluk:** Kurallar, yasal hamleler, tahta durumu, oyun sonları ve regresyonlar.
2. **Arama/pozisyon davranışı:** Sabit konumlardaki skor, bestmove, düğüm/süre ve taktik testler.
3. **Performans:** NPS, süre ve kaynak kullanımı; aynı makine/derleyici koşulları.
4. **Göreli oyun gücü:** Aynı kuralları uygulayan, ölçüme uygun rakip karşısında yeterli örneklemli maçlar.
5. **Mutlak/dış ELO eşlemesi:** Ancak uygun ortak rakip havuzu ve kalibre edilmiş referanslar varsa.

Bu kanıt sınıflarının sonuçları birbirinin yerine kullanılamaz. Perft, unit test, NNUE hash eşleşmesi veya kısa gauntlet tek başına ELO artışı kanıtı değildir.

## Faz A — Oyun kuralları ve ölçüm zemini

- Başlangıç konumu, hamle yasallığı, özel taşlar, terfi, citadel, swap ve oyun sonları için sürümlenmiş regresyon testleri.
- Kural spesifikasyonu ile kod arasındaki farklılıkları kaynak atfı ve açık karar kaydıyla çöz.
- Perft baseline'larını belirli commit ve kural sürümüne bağla.
- Test kümesinin çözülebilir, çözülemeyen ve tarihsel olarak tartışmalı pozisyonlarını etiketle.

**Kapı A:** Kritik kural/regresyon hatası yok; bilinen sınırlamalar belgeli.

## Faz B — Sabit konum kalitesi ve arama davranışı

- Her test pozisyonu için kaynak, amaç, beklenen taktik/stratejik özellik ve son gözden geçirme bilgisi tut.
- Aynı engine commit'i, model hash'i, arama ayarları ve tek-thread ayarı ile tekrar çalıştır.
- HCE, NNUE ve iç Persona policy A/B koşullarını birbirinden ayır; bir defada yalnızca ilgili değişkeni değiştir.
- Ham JSONL, CSV özet, konfigürasyon hash'i, source fingerprint ve kullanılan model/book hash'lerini sakla.
- Sabit-konum referansının gerçek bir oracle olmayabileceğini raporda belirt.

**Kapı B:** Koşular tekrar üretilebilir ve kalite sonuçlarının neyi ölçtüğü açık.

## Faz C — Performans deneyi

- Sabit donanım, OS, derleyici, build tipi, thread, hash boyutu ve zaman limitleri.
- Açılış kitabı, NNUE/HCE modu, kaynak commit'i ve model hash'i her koşuda kayıtlı.
- Birden çok tekrar ile medyan/dağılım, sıcak/soğuk çalıştırma ve CPU gürültüsü etkileri raporlanır.
- NPS artışını oyun gücü artışı olarak sunma.

**Kapı C:** Performans farkı bağımsız tekrarlarda görülüyor ve yapılandırmalar eşleşiyor.

## Faz D — Göreli oyun gücü maçı

### Karşılaştırma kurulumu

- İlk ölçüm, aynı kuralları doğru uygulayan Timurlenk sürümleri/ayarları arasında yapılır. Klasik 8×8 satranç motorlarının puanı, kuralları ve rakip havuzu farklı olan 11×10 varyanta doğrudan aktarılmaz.
- Her eşleşme aynı açılış konumunu iki renkle oynayacak şekilde eşleştirilir; renk sırası ve açılışlar dengelenir.
- Motor ikilisi, commit, derleyici, NNUE/açılış kitabı hash'i, ayarlar, seed, açılış, renk ve PGN/sonuç verisi kayıt altına alınır.
- Süre kontrolü, maksimum ply, tekrarlı pozisyon, oyun sonu adjudication ve kesilen maç kuralları maçlardan önce yazılır.
- Değişkenler: bir kezde yalnızca tek hedef değişken; ör. NNUE vs HCE veya `PersonaSearchPolicies` ON/OFF.

### Örneklem ve istatistik

- Önce küçük pilot, sonra önceden ilan edilmiş kurallara göre genişletilmiş maç partileri yürüt.
- W/D/L, puan oranı, tahmini rating farkı, %95 güven aralığı, toplam/çıkarılan maç sayısı ve çıkarma gerekçeleri birlikte raporlanır.
- Yalnızca güven aralığı yeterince daraldığında güçlü sonuç açıklanır. Planlama hedefi örneğin 95% aralığın yarı genişliğini ±30 Elo düzeyine indirmektir; gereken maç sayısı gerçek varyansa bağlıdır ve varsayılarak belirlenmez.
- Bütçe veya süre nedeniyle bu hassasiyet sağlanamazsa sonuç açıkça **ön sonuç / belirsiz** diye etiketlenir; nokta tahmini kesin ELO gibi sunulmaz.
- Gerekirse sonraki aşamada SPRT veya önceden belirlenmiş başka bir ardışık karar yöntemi seçilebilir; hipotez ve hata sınırları maç başlamadan sabitlenir.

**Kapı D:** Protokol önceden kayıtlı, maçlar renk/açılış bakımından dengeli, veri bütün ve güven aralığı yorumlanabilir.

## Faz E — ELO / referans havuzu

Mutlak veya dışa dönük bir ELO iddiası ancak varyant kuralları uyumlu bir referans havuzu, tekrarlanabilir maçlar ve kalibre edilebilir bağlantı noktaları mevcutsa verilir. Böyle bir havuz yoksa yalnızca belirtilen rakibe ve protokole göre ölçülmüş göreli performans yayımlanır.

## Yayınlanacak rapor şablonu

- Engine commit/build, model/book hash ve varyant-kural sürümü
- Rakip sürümü ve eşleştirme protokolü
- Donanım, OS, compiler, thread/time kontrolleri
- Pozisyon/açılış seti ve renk dengesi
- Oyun sayısı, W/D/L, kesilen/çıkarılan oyunlar ve nedenleri
- Rating tahmini, %95 güven aralığı ve yöntem
- Ham kayıt/PGN/manifest erişimi veya kamusal yayımlanmama gerekçesi
- Limitler, tekrar üretim komutları ve “bu sonuç neyi kanıtlamaz?” bölümü

## Bugünkü bilinen kısıtlar

Özel motor durum belgesindeki sekiz pozisyonluk sabit küme küçük bir araştırma setidir. Daha önceki 16 oyunluk Persona/Psyche pilotunda bütün oyunlar 12-ply sınırına ulaşmış ve berabere kaydedilmiştir; bu sadece iş akışı pilotudur. Bu verilerden oyun gücü/ELO iddiası çıkartılmamalıdır.
