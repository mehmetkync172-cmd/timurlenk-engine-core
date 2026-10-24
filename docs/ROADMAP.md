# Araştırma Yol Haritası

**Durum görüntüsü:** 24 Ekim 2026  
**İlke:** Bu yol haritası hedef ve kapıları tanımlar; planlanan işi tamamlanmış iş gibi göstermez.

## Aşama 0 — Kaynağı ve iddiaları sabitle

**Amaç:** Tek bir güncel kaynak doğruluk noktası kullanmak.

- Özel motorun son kontrol edilen engine-code commit'i `6e936104d54f42407925ea6717e98f67a5e97718`; sonraki commit'ler manuel workflow ve dokümantasyon kayıtlarını güncelledi. Her teknik oturumda canlı dal başı, PR durumu ve CI koşuları yeniden okunur. 24 Ekim kontrolünde açık PR listesi boştu.
- V7 handoff ZIP'i ile `engine-v7/` arasındaki sürüm farkı korunur ve belgelenir.
- V1–V4 deney kayıtları tarihsel şemaları bozmadan doğrulanır.
- Tarihî kural spesifikasyonu, uygulama davranışı ve kaynak yorumları ayrı izlenir.

**Çıkış kapısı:** Hangi commit'in hangi test/raporla desteklendiği açıkça izlenebilir.

## Aşama 1 — Motor güvenilirliği

- PR #11 geçmişte birleştirilmiş; kalan doğrulama, güncel ana dal ve raporlarla yeniden karşılaştırılmalı.
- Skaler ve optimize NNUE yolları için aynı model/konum çiftlerinde diferansiyel testleri sürdür.
- Kural regresyonları, perft ve model manifest kontrolünü düzenli çalıştır.
- PR #7 geçmiş durum olarak kapalı; güncel main'de açılış kitabı köken testi ve v4 alanlarının varlığını kaynak/test üzerinden doğrula.
- Strength harness araştırma dalı `research/strength-measurement-v1-clean` içinde kaldı. CI, GitHub Actions harcama limiti nedeniyle job başlamadan bloklandı; limit yenilenince harness testlerini çalıştırmadan bu dalı birleştirme.

**Çıkış kapısı:** Ana dal üzerinde gerekli job'lar başarılı; deney veri kayıtları gerçek UCI çıktısına ve doğru artefakt hash'ine dayanıyor.

## Aşama 2 — Araştırma ve performans ölçümleri

- Sürümü sabitlenmiş, açıklamalı sabit-konum kümesini genişlet.
- Arama kalitesi/ablation testlerini oyun gücü iddiasından ayrı raporla.
- Aynı makine, derleyici, motor commit'i, model ve ayarlarla NPS/süre regresyonlarını ölç.
- Renk değişimli eşleştirilmiş oyunlar ve istatistiksel güven aralığı için [ELO doğrulama planını](ELO_VALIDATION_PLAN.md) izle.

**Çıkış kapısı:** Her iddia protokol, ham veri, konfigürasyon, hash manifesti ve yorum sınırlarıyla birlikte yayımlanabilir.

## Aşama 3 — Persona entegrasyonu (bilinçli olarak sonraya bırakıldı)

- Persona araştırma depoları ayrı yürütülür; bu repo onları yönetmez veya kodlarını kopyalamaz.
- Her iki Persona reposunun ilgili parçaları yeterli olgunluğa ulaştığında veri şeması ve kullanım amacı gözden geçirilir.
- İlk bağlantı motor içinde Persona üretimi değil, deney verisini okuyan/doğrulayan salt okunur bir importer prototipi olmalıdır.
- Schema, hash, kaynak bağlamı ve veri kalitesi doğrulanmadan hiçbir sonuç kullanılmaz.
- Gerçek API/değişim ve uçtan uca test geçmeden entegrasyon etkin olarak belgelenmez.
- Parametre geri beslemesi ancak ayrı kontrollü deney, geri alınabilirlik ve maç tabanlı doğrulama ile ele alınır.

**Çıkış kapısı:** Ayrı reposu olan Persona sistemlerinden gelen veriler için sürümlü sözleşme, güvenli test seti, gerçek end-to-end kanıtı ve geri dönüş planı var.

## Aşama 4 — Kamuya açık yayın

- Her artefakt için telif, lisans, provenance, boyut, gizlilik ve teknik iddia kontrolü yap.
- Kaynak kodu veya model yayımlamak zorunlu hedef değildir; bu karar ayrıca alınır.
- Vitrin deposunu motorun birebir kopyasına dönüştürme; sadece gözden geçirilmiş kamusal materyali seç.
- Lisans kararı ve katkı yönergeleri netleştirilmeden açık katkı/reuse garantisi verme.

**Çıkış kapısı:** Yayın politikası kontrol listesi tamamlanmış, kaynak sürümü ve doğrulama kapsamı açık.
