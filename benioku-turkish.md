# AI Kılavuzu

[![GitHub](https://img.shields.io/github/license/menesekinci/ai-senior-guide)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/menesekinci/ai-senior-guide)](https://github.com/menesekinci/ai-senior-guide/stargazers)

> **AI destekli yazılım geliştirme için üretim düzeyinde mühendislik standartları**

AI tarafından üretilen kodlardaki "sessiz hataları" önlemek için savaşta test edilmiş mimari desenler, güvenlik yönergeleri ve en iyi uygulamalar ile tasarlanmış kapsamlı bir kılavuz.

---

## 🎯 Bu Nedir?

**AI Kılavuzu**, yapay zeka kodlama asistanlarının üretim için hazır kod oluşturmak için başvurabileceği yapılandırılmış bir bilgi tabanıdır. **AI tarafından üretilen kodun %40-45'inin sessiz hatalar içerdiği** kritik boşluğu ele alır - testleri geçer ancak üretimde başarısız olur.

### Sessiz Hata Problemi

| Test Yakalar ✅ | Test Kaçırır ❌ |
|----------------|----------------|
| Sözdizimi hataları | Yarış koşulları |
| Çalışma zamanı istisnaları | Gizli güvenlik açıkları |
| Başarısız doğrulamalar | Performans düşüşü |
| | Mimari anti-desenler |
| | Eşzamanlılık anomalileri |

### 🧠 Bilişsel + Bellek Protokolü

Bu kılavuz devrimci iki aşamalı bir yaklaşım uygular:

**Aşama 1: Bilişsel Protokol (Uygulama Öncesi)**
AI, 5 Adımlı Derin Düşünme sürecini kullanarak kodlamadan önce derinlemesine düşünür:
1. Niyet Analizi (Ne & Neden)
2. Geleceğe Dayanıklılık (Sırada Ne Var)
3. Standartlaştırma (Doğrusu Nasıl Yapılır)
4. Sistemik Etki (Etkileşimler)
5. Doğrulama Stratejisi (Nasıl Doğrulanır)

**Aşama 2: Bellek Protokolü (Uygulama Sonrası)**
AI, `architecturehistory.md` aracılığıyla kalıcı bellek tutar:
- Mimari Karar Kayıtları (ADR)
- Bileşen bağımlılıkları
- Bilgi Tabanı referansları ile tasarım gerekçesi
- Bilinen teknik borç

**Sonuç:** AI, "kod yazıcı"dan kurumsal belleğe sahip "yazılım mimarı"na dönüşür.

### ⚠️ Aşırı Mühendislik Önleme

**Kritik:** Bu kılavuz aynı zamanda **aşırı mühendislik** problemini de önler. AI ajanları desenleri uygulamadan önce "Gerçekten ne kadarına ihtiyaç var?" diye sormalıdır.

**Referans:** `Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**Örnekler:**
- ❌ Kubernetes + Mikroservisler ile Todo uygulaması
- ✅ Monolit + SQLite ile Todo uygulaması

**YAGNI İlkesi:** Şu anda gerekli değilse, yapmayın.

---

## 🗃️ Proje Belleği: architecturehistory.md

Bu kılavuzu kullanan her proje, proje kökünde bir `architecturehistory.md` dosyası tutmalıdır. Bu, AI'nın oturumlar arasındaki "belleği" görevi görür.

### Şablon

```markdown
## [YYYY-AA-GG SS:DD] Değişiklik: [Özellik Adı]
- **Hedef:** [Neyin uygulandığı]
- **Karar:** [Seçilen mimari]
- **Gerekçe:** [Neden, KB referansları ile]
- **Bağımlılıklar:** [İlgili bileşenler]
- **Riskler/Borç:** [Bilinen sınırlamalar]
```

---

## 📖 Başlangıç: skill.md

**`skill.md` bu bilgi tabanının birincil giriş noktası ve indeksidir.**

Bu dosya şunları sağlar:
- **Ana indeks** - tüm 8 bilgi tabanı dosyası için
- **Anahtar kelime dizini** - hızlı konu arama
- **Çapraz referans kılavuzu** - ilgili konular için
- **Kullanım talimatları** - AI ajanları için

**AI Ajanları:** Bilgi tabanı yapısını anlamak ve anahtar kelimelere göre ilgili dosyaları bulmak için her zaman `skill.md` ile başlayın.

---

## 🗂️ Depo Yapısı

```
ai-senior-guide/
├── skill.md                                    # ⭐ BAŞLA - Ana indeks + Protokoller
├── knowledgeAI/                                # Bilgi tabanı dizini
│   ├── AI_Guardrail_Architecture_Knowledge_Base.md
│   ├── Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md
│   ├── Client_Side_Security_Architecture_Knowledge_Base.md
│   ├── Comprehensive_Architectural_Framework_Knowledge_Base.md
│   ├── Contextual_Architecture_Decision_Matrix_Knowledge_Base.md
│   ├── Defensive_UI_Engineering_Knowledge_Base.md
│   ├── End_to_End_Type_Safety_Knowledge_Base.md
│   └── Modern_Web_Performance_Engineering_Knowledge_Base.md
├── README.md                                   # Bu dosya
└── architecturehistory.md                      # 🧠 Proje belleği (proje başına)
```

---

## 📚 Mevcut Bilgi Dosyaları

### 1. AI Guardrail Mimarisi
**Dosya:** `/knowledgeAI/AI_Guardrail_Architecture_Knowledge_Base.md`

**Kapsamlı dağıtık sistemler ve güvenlik mimarisi**

**Anahtar kelimeler:** `distributed-systems`, `consistency`, `consensus`, `resilience`, `fault-tolerance`, `microservices`, `CAP-theorem`, `circuit-breaker`, `event-driven`, `SRE`, `observability`, `zero-trust`

---

### 2. Yüksek Bütünlüklü Sistemlerde Mimari Dayanıklılık
**Dosya:** `/knowledgeAI/Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md`

**Üretim iş yükleri için gelişmiş güvenilirlik desenleri**

**Anahtar kelimeler:** `observability`, `distributed-tracing`, `OpenTelemetry`, `chaos-engineering`, `rate-limiting`, `transactional-outbox`, `CDC`, `cache-stampede`, `kubernetes-hardening`

---

### 3. İstemci Tarafı Güvenlik Mimarisi
**Dosya:** `/knowledgeAI/Client_Side_Security_Architecture_Knowledge_Base.md`

**Modern web uygulaması güvenliği temelleri**

**Anahtar kelimeler:** `XSS`, `CSP`, `DOM-based-XSS`, `supply-chain-risk`, `JWT-storage`, `HttpOnly-cookies`, `BFF-pattern`, `DOMPurify`, `SRI`

---

### 4. Kapsamlı Mimari Çerçeve
**Dosya:** `/knowledgeAI/Comprehensive_Architectural_Framework_Knowledge_Base.md`

**Veritabanı eşzamanlılığı, performans ve güvenlik temelleri**

**Anahtar kelimeler:** `ACID`, `isolation-levels`, `dirty-read`, `phantom-read`, `N-plus-1`, `ORM`, `optimistic-locking`, `Redlock`, `BOLA`, `IDOR`

---

### 5. Bağlamsal Mimari Karar Matrisi
**Dosya:** `/knowledgeAI/Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**Aşırı mühendislikten kaçınma ve çözümleri doğru boyutlandırma**

**Anahtar kelimeler:** `overengineering`, `premature-optimization`, `YAGNI`, `Cynefin`, `ADR`, `right-sizing`, `monolith`, `microservices`, `architecture-astronaut`

---

### 6. Savunmacı UI Mühendisliği
**Dosya:** `/knowledgeAI/Defensive_UI_Engineering_Knowledge_Base.md`

**Dayanıklı kullanıcı arayüzü desenleri**

**Anahtar kelimeler:** `error-boundaries`, `graceful-degradation`, `retry-logic`, `skeleton-screens`, `optimistic-UI`, `a11y`, `ARIA-live`, `focus-management`

---

### 7. Uçtan Uca Tip Güvenliği
**Dosya:** `/knowledgeAI/End_to_End_Type_Safety_Knowledge_Base.md`

**Tip-güvenli tam yığın JavaScript geliştirme**

**Anahtar kelimeler:** `TypeScript`, `schema-sharing`, `OpenAPI`, `tRPC`, `Zod`, `runtime-validation`, `contract-testing`, `Pact`, `RTK-Query`

---

### 8. Modern Web Performans Mühendisliği
**Dosya:** `/knowledgeAI/Modern_Web_Performance_Engineering_Knowledge_Base.md`

**Core Web Vitals ve optimizasyon stratejileri**

**Anahtar kelimeler:** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `bundle-analysis`, `tree-shaking`, `code-splitting`, `SSR`, `SSG`, `hydration`

---

## 🔍 Hızlı Referans: Anahtar Kelime Eşleştirme

| Üzerinde Çalıştığınız Konu | Bu Dosyayı Okuyun |
|---------------------------|-------------------|
| API tasarımı, REST, gRPC, GraphQL | AI Guardrail Mimarisi |
| Veritabanı, işlemler, eşzamanlılık | Kapsamlı Mimari Çerçeve |
| CSP, XSS, güvenli depolama, JWT | İstemci Tarafı Güvenlik Mimarisi |
| İzleme, izleme, gözlemlenebilirlik | Mimari Dayanıklılık |
| Performans, paket, Core Web Vitals | Modern Web Performans Mühendisliği |
| Tip güvenliği, doğrulama, şema | Uçtan Uca Tip Güvenliği |
| Hata işleme, yükleme durumları | Savunmacı UI Mühendisliği |
| Mimari kararları, aşırı mühendislik | Bağlamsal Mimari Karar Matrisi |

---

## 🚀 Nasıl Kullanılır

### AI Ajanları İçin (LLM Bağlamı)

#### Adım 1: Bilişsel Protokol (Uygulama Öncesi)
Herhangi bir kod yazmadan önce 5 Adımlı Derin Düşünme'yi uygulayın.

#### Adım 2: Uygulama
1. **`skill.md` ile başlayın** - Ana indeksi okuyun
2. **`/knowledgeAI/` dizinine gidin** - Tüm bilgi dosyaları burada
3. Kullanıcının görevinden **anahtar kelimeleri belirleyin**
4. İlgili dosyaları bulmak için `skill.md` içindeki **anahtar kelime eşleştirmeyi kullanın**

#### Adım 3: Bellek Protokolü (Uygulama Sonrası)
1. **`architecturehistory.md` güncelleyin** - Kararı kaydedin
2. **Gerekçeyi belgeleyin** - Kullanılan Bilgi Tabanı dosyalarına referans verin

### Geliştiriciler İçin

1. Mevcut konuları anlamak için **`skill.md` göz atın**
2. Tüm dosyalar için **`/knowledgeAI/` dizinini kontrol edin**
3. İlgili bölümleri bulmak için **anahtar kelime araması yapın**
4. Kalite kontrol listesi olarak **kod incelemeleri sırasında referans verin**

---

## 📄 Lisans

MIT Lisansı - Detaylar için depoya bakın.

---

> **Unutmayın:** Amaç tüm hataları önlemek değil, üretimde önemli olan hataları önlemektir.
