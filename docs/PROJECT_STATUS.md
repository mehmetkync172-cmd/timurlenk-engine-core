# Proje Durumu ve Kaynak Senkronizasyon Denetimi

**Gözden geçirme tarihi:** 24 Ekim 2026  
**Amaç:** Hangi kaynağın güncel olduğunu, doğrulanan test kanıtını ve bekleyen işleri ayırmak.

## Kaynak doğruluk noktaları

| Öğe | Güncel durum |
|---|---|
| Özel motor deposu | [timurlenk-engine-private](https://github.com/mehmetkync172-cmd/timurlenk-engine-private) |
| Motor kaynak dizini | `engine-v7/` |
| Son kontrol edilen motor-kod commit'i | [`6e936104d54f42407925ea6717e98f67a5e97718`](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/commit/6e936104d54f42407925ea6717e98f67a5e97718); sonraki özel-main commit'leri workflow/dokümantasyon kayıtlarıdır |
| Son `main` commit mesajı | `ci: expose manual strength harness workflow` |
| Güç ölçüm araştırma dalı | [`research/strength-measurement-v1-clean`](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/tree/research/strength-measurement-v1-clean) |
| Araştırma dalı HEAD'i | [`7cc39be650f82505f5647c51f34e9bf1085ad027`](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/commit/7cc39be650f82505f5647c51f34e9bf1085ad027) (son kontrol edilen) |
| Güncel deney şeması | `timurlenk.experiment.v4` |
| Kamuya açık vitrin | Bu depo; özel motor kodunu ve model dosyalarını içermez |
| Persona entegrasyonu | Çalışan API/veri hattı yok; sonraki aşamaya bırakıldı |
| Mutlak ELO / oyun gücü | Belirlenmiş değil |

## GitHub Actions ve test kanıtı — 24 Ekim 2026

- `strength-harness.yml` tek başına `main` dalına eklendi; commit: [`8ea25de`](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/commit/8ea25deb331be42306c0ecd7edf8faa7282569e5). Sonraki değişiklik, küçük smoke raporunun `rating_ready=false` olmasını doğrular ve çıktıları 14 gün saklanan Actions artefaktına yükler; bu ekleme ana dala [`1145bc3`](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/commit/1145bc3de6436e3ec7a17c2541dce43dfad54086), araştırma dalına [`7cc39be`](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/commit/7cc39be650f82505f5647c51f34e9bf1085ad027) commit'leriyle kaydedildi. Bu değişiklikler araştırma motor kodunu `main` ile birleştirmez.
- Manuel workflow tetiklendi ancak GitHub job'u çalıştırmadan şu nedenle engelledi: son hesap ödemeleri başarısız olabilir veya harcama limiti artırılmalıdır. Bu, derleme/test hatası değildir; Actions işi başlamadığı için güncel harness'in CI sonucu yoktur.
- Daha önceki yerel kaynak snapshot'ında CTest 12/12, model manifesti 23/23 ve UCI smoke 6/6 geçmişti. Bu snapshot güncel araştırma dalıyla birebir aynı değildir; bu sonuçlar yeni strength harness'i doğrulamaz.
- Önceki tanılama workflow'ları da özel depoda adımlar başlamadan başarısız olmuştu. GitHub Actions harcama limiti yenilenip erişim açılana kadar yeni CI sonucu beklemede.
- **Birleştirme kapısı:** Güncel strength harness'in testleri gerçekten çalışıp geçmeden araştırma dalı `main` ile birleştirilmemeli ve ELO/güç iddiası yayımlanmamalı.

## PR ve dal durumu

- [PR #13 — controlled engine strength measurement harness](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/pull/13): kapalı, birleştirilmedi. PR'ın head SHA'sı (`4d4a2f9...`) son kontrol edilen araştırma dalı HEAD'inden (`7cc39be...`) eski; bu nedenle PR mevcut dalın güncel bir temsili değildir.
- [PR #14 — hosted runner diagnostic](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/pull/14): tanılama tamamlandığı için kapalı, birleştirilmedi.
- PR #11 motor sertleştirmesi ve güvenli PersonaBridge/Needle doğrulama çalışması geçmişte birleştirilmiş olarak listeleniyor; açık PR olarak görünmüyor.
- PR #7, #11 için eski oturum notları artık güncel değildir; bu incelemede açık PR listesi boş döndü.
- Dal listesinde eski import, workflow, test ve refactor dalları var. Bunlar kullanılmıyor olabilir, ancak son commit ve referansları karşılaştırmadan silinmemelidir.

## Yüklenen 10 Ekim V7 handoff ZIP'i ile fark

Yüklenen `TIMURLENK_ENGINE_V7_GITHUB_HANDOFF_2026-10-10.zip` paketi kendi talimatlarında kaynak ağacının yerel `TIMURLENK_PRIVATE_CORE_IMPORT_V7.zip` girdisinden türetildiğini ve GitHub `main` dalının birebir arşivi olmadığını açıkça belirtiyor.

- ZIP içindeki `engine-v7-source/` dizininde 166 kaynak/dokümantasyon dosyası sayıldı.
- ZIP içindeki şema dizini v1, v2 ve v3 dosyalarını içeriyor; güncel GitHub `main` üzerinde ayrıca `timurlenk.experiment.v4.schema.json` bulunuyor.
- GitHub'da ana dalda ayrıca bağımsız hamle gösterim/self-play katmanları, açılış kitabı kökeni için v4 kayıt alanları, kök dizindeki etkin CI yapılandırmaları ve eski x86-64 işlemciler için skaler NNUE derleme seçeneği bulunuyor.
- Bu nedenle ZIP, bağlam ve tarihsel kaynak referansı olarak kullanılabilir; güncel kaynak kodu yerine kopyalanmamalıdır.

**Kural:** Kod değiştirirken ilk iş güncel özel `main` HEAD'ini, açık PR'ları ve CI kanıtını yeniden kontrol etmek. ZIP'i veya eski sohbet notlarını güncel `main` ile eşdeğer varsaymamak.

## Neler birleştirildi, neler bekliyor?

Bu bölüm 16 Ekim tarihli tarihsel kaydıdır. Güncel PR ve dal durumu için bu belgenin üstündeki 24 Ekim bölümünü esas al.

Bu çalışma alanında görünmeyen yerel dosyalar, başka makinelerdeki çalışma ağaçları veya başka sohbetlerde yapılmış ama henüz GitHub'a itilmemiş değişiklikler denetlenemez. Eksiksizlik kararı yalnızca yüklenen arşiv ve GitHub'da erişilen commit/PR/Actions kayıtları için geçerlidir.

## Sonraki oturum için başlangıç kontrolü

1. Özel motor reposundaki HEAD ve açık PR'ları yeniden oku.
2. PR #11'in yeni testlerini/dokümanlarını ana dalla karşılaştır; sözleşme/validator kodunu çalışan adaptör gibi tanımlama.
3. PR #7'nin güncel şema v4 ile gerçekten eksik olan bir uçtan uca kontrol ekleyip eklemediğine karar ver.
4. ELO planındaki kapılar sağlanmadan motor gücü iddiasında bulunma.
5. Persona depoları olgunlaşmadan runtime bağımlılığı, repo birleştirme veya otomatik geri-besleme hattı kurma.
