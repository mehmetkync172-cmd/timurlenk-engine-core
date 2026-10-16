# Proje Durumu ve Kaynak Senkronizasyon Denetimi

**Gözden geçirme tarihi:** 16 Ekim 2026  
**Amaç:** Yeni bir çalışma oturumunun hangi kaynağı doğru kabul etmesi gerektiğini, nelerin birleştiğini ve bekleyen işlerin hangileri olduğunu netleştirmek.

## Kaynak doğruluk noktaları

| Öğe | İnceleme anındaki durum |
|---|---|
| Özel motor deposu | [timurlenk-engine-private](https://github.com/mehmetkync172-cmd/timurlenk-engine-private) |
| Motor kaynak dizini | `engine-v7/` |
| Ana dalın gözlenen HEAD'i | `d75d967344319376b0372a30fd8823836ddd8707` |
| Son ana dal commit mesajı | `docs/test: keep experiment schema version consistent` |
| Güncel deney şeması | `timurlenk.experiment.v4` |
| Kamuya açık vitrin | Bu depo; motor C++ uygulamasını ve modelleri içermez |
| Persona entegrasyonu | Çalışan API/veri hattı yok; sonraki faz olarak bekletiliyor |
| Mutlak ELO / oyun gücü | Belirlenmiş değil; araştırma planı hazırlanıyor |

## GitHub'da doğrulanan durum

16 Ekim 2026 tarihinde özel deponun `main` HEAD'ini kullanan aşağıdaki zamanlanmış iş akışları başarıyla tamamlandı:

- [Perft Test Suite #91](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/actions/runs/38900204750)
- [Gauntlet (NNUE vs HCE) #6](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/actions/runs/38850123591)
- [Benchmark Log #6](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/actions/runs/38845480649)

Bu başarılar ilgili iş akışlarının tamamlandığını gösterir. Tek başına tarihsel doğruluğu, mutlak ELO'yu, genel oyun gücünü veya her platformda çalışmayı kanıtlamaz. Ana dalın güncel `STATUS.md` dosyası C++20 Release build, CTest 12/12, UCI smoke 6/6, perft referansları ve 23 model/kitap artefaktı için manifest doğrulaması bildirir.

## Açık değişiklikler — kaynak kodu deposu

- [PR #7 — açılış kitabı köken kaydı uçtan uca testi](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/pull/7): açık; gerçek UCI araması sırasında seçilen kitap dosyası ve hash'inin doğrulanmasını hedefler.
- [PR #11 — motor sertleştirmesi ve PersonaBridge/Needle doğrulaması](https://github.com/mehmetkync172-cmd/timurlenk-engine-private/pull/11): açık taslak. NNUE yükleme, hamle/tahta geri alma, UCI ve zaman sınırı regresyonları ile sözleşme/validator çalışmaları içerir. PR'da başarılı CI bulunması, henüz ana dala birleştirilmiş olduğu anlamına gelmez.

Bu inceleme PR #7 ve #11'i birleştirmedi veya motor koduna yazma yapmadı.

## Yüklenen 10 Ekim V7 handoff ZIP'i ile fark

Yüklenen `TIMURLENK_ENGINE_V7_GITHUB_HANDOFF_2026-10-10.zip` paketi kendi talimatlarında kaynak ağacının yerel `TIMURLENK_PRIVATE_CORE_IMPORT_V7.zip` girdisinden türetildiğini ve GitHub `main` dalının birebir arşivi olmadığını açıkça belirtiyor.

- ZIP içindeki `engine-v7-source/` dizininde 166 kaynak/dokümantasyon dosyası sayıldı.
- ZIP içindeki şema dizini v1, v2 ve v3 dosyalarını içeriyor; güncel GitHub `main` üzerinde ayrıca `timurlenk.experiment.v4.schema.json` bulunuyor.
- GitHub'da ana dalda ayrıca bağımsız hamle gösterim/self-play katmanları, açılış kitabı kökeni için v4 kayıt alanları, kök dizindeki etkin CI yapılandırmaları ve eski x86-64 işlemciler için skaler NNUE derleme seçeneği bulunuyor.
- Bu nedenle ZIP, bağlam ve tarihsel kaynak referansı olarak kullanılabilir; güncel kaynak kodu yerine kopyalanmamalıdır.

**Kural:** Kod değiştirirken ilk iş güncel özel `main` HEAD'ini, açık PR'ları ve CI kanıtını yeniden kontrol etmek. ZIP'i veya eski sohbet notlarını güncel `main` ile eşdeğer varsaymamak.

## Neler birleştirildi, neler bekliyor?

Özel repodaki PR geçmişinde #1–#6 ile #8–#10 kapalı/birleştirilmiş; #7 açık ve #11 taslak olarak görünüyordu. Bu, ilgili çalışma paketlerinin büyük ölçüde ana dala aktarıldığına, ama bütün çalışma kollarının birleştirilmediğine işaret eder.

Bu çalışma alanında görünmeyen yerel dosyalar, başka makinelerdeki çalışma ağaçları veya başka sohbetlerde yapılmış ama henüz GitHub'a itilmemiş değişiklikler denetlenemez. Eksiksizlik kararı yalnızca yüklenen arşiv ve GitHub'da erişilen commit/PR/Actions kayıtları için geçerlidir.

## Sonraki oturum için başlangıç kontrolü

1. Özel motor reposundaki HEAD ve açık PR'ları yeniden oku.
2. PR #11'in yeni testlerini/dokümanlarını ana dalla karşılaştır; sözleşme/validator kodunu çalışan adaptör gibi tanımlama.
3. PR #7'nin güncel şema v4 ile gerçekten eksik olan bir uçtan uca kontrol ekleyip eklemediğine karar ver.
4. ELO planındaki kapılar sağlanmadan motor gücü iddiasında bulunma.
5. Persona depoları olgunlaşmadan runtime bağımlılığı, repo birleştirme veya otomatik geri-besleme hattı kurma.
