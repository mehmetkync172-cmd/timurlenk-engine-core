# Timurlenk ↔ Persona — Sonraki Oturum Devir Notu

**Güncelleme:** 16 Ekim 2026  
**Bu notun amacı:** Persona araştırma çalışması başka oturumlarda olgunlaşırken Timurlenk durumunun yanlış anlaşılmasını engellemek.

## Karar

Persona'yı bu Timurlenk deposundan yönetmiyoruz. Persona için oluşturulmuş iki ayrı depo bağımsız geliştirme hattı olarak kalacak. Bu iki depo yeterli olgunluğa geldiğinde, hangi bileşenlerin Timurlenk ile ilişkilendirileceği ayrı mimari/araştırma kararıyla ele alınacak.

Şu an repo birleştirme, Persona kaynağını Timurlenk içine kopyalama veya çalışma zamanı bağımlılığı kurma yapılmamalı.

## Mevcut sistemleri ayır

### Timurlenk motor içi Persona

- C++ içindeki `Apex::PersonaLayer` / `PersonaType` profilleri ve Psyche değeri oyun arama/değerlendirme davranışlarını etkiler.
- Üç sınırlı özel arama politikası (Aşina/Vezüv, Erlik/Karanlık Derinlik, Umay/Kalkan) dokümantasyon ve hedef regresyonları ile kapsanmıştır.
- Bu, genel amaçlı bir konuşma ajanı veya ayrı Persona araştırma sisteminin kendisi değildir.

### Ayrı Persona araştırma sistem(ler)i

- Persona kodu ve araştırması kendi depolarında, kendi yol haritası ve olgunluk kapılarıyla geliştirilecek.
- Timurlenk bu çalışmayı yönetmez, onun kaynak kodunu yayınlamaz ve ona bağımlı olmadan build/test edilmeye devam eder.
- Hiçbir Persona modelinin eğitildiği, doğrulandığı veya Timurlenk'e bağlandığı, ayrı kanıt bulunmadan varsayılmaz.

## Timurlenk tarafındaki mevcut veri kanalı

Özel motor deposunun `engine-v7/docs/PERSONA_RESEARCH_CHANNELS.md` belgesi ve `engine-v7/docs/schemas/timurlenk.experiment.v4.schema.json` dosyası güncel başlangıç kaynaklarıdır.

- `ExperimentLog` isteğe bağlı yerel JSONL kaydıdır; varsayılan olarak kapalıdır.
- v4, kullanılan açılış kitabının gerçek yol/hash/status alanlarını ekler; v1-v3 geçmiş şemaları korunur.
- `external_persona` şu an `null` değerindedir.
- Recorder dış Persona reposunu çağırmaz, yüklemez veya değiştirmez.
- Kayıtlar analiz adayı deney verisidir; model kalitesi veya oyun gücünün kanıtı değildir.

## Gelecekte olası entegrasyon sırası

1. İki Persona deposunun ilgilendirilecek alt sistemleri olgunlaşır; hangi problem çözüleceği ve hangi çıktının faydalı olacağı belirlenir.
2. Veri şeması, lisans/provenance, gizlilik ve kullanıcı verisi sınırları değerlendirilir.
3. Salt okunur importer/validator prototipi kurulur; şema, kaynak commit'i, model/book hash'i ve deney yapılandırması doğrulanır.
4. Küçük bir küratörlü veri kümesi Persona tarafında analiz edilir. Bu aşamada motor ayarlarını değiştiren otomasyon yoktur.
5. Yarar netse ayrı bir adapter sözleşmesi tanımlanır, gerçek uçtan uca veri transferi test edilir ve başarısız durumda güvenli durma doğrulanır.
6. Motor parametresi önerme/geri besleme ancak deney hipotezi, versiyonlama, geri alınabilirlik, ablation ve renk değiştirmeli maçlarla doğrulama sonrası tartışılır.

**Etkin entegrasyon olarak duyurma kapısı:** gerçek schema exchange + gerçek veriyle uçtan uca test + hata durumlarının güvenli ele alınması + tekrar üretilebilir doğrulama kanıtı.

## ELO / oyun gücü

ELO ve gerçek oyun gücü doğrulaması, Persona entegrasyonundan bağımsız araştırma hattıdır. Entegrasyon beklerken ELO araştırma planı, benchmark veri kalitesi ve motor regresyonları ilerleyebilir. Güncel plan: [ELO_VALIDATION_PLAN.md](ELO_VALIDATION_PLAN.md).

## Kaynak senkronizasyon uyarısı

Yüklenen 10 Ekim V7 ZIP'i GitHub özel `main` ile byte-byte aynı değil. ZIP içinde `engine-v7-source/` yerel paket kopyası ve v1-v3 şema dosyaları bulunuyordu; güncel GitHub `main`'de `engine-v7/`, şema v4 ve sonradan alınan değişiklikler var. Güncel kod için özel `main` dalı esas alınmalı.

Denetim notu: [PROJECT_STATUS.md](PROJECT_STATUS.md).
