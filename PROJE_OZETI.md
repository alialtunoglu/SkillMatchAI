# SkillMatchAI - Proje Özeti

## 📋 Genel Bakış

**SkillMatchAI** (Mikro Eğitim Planı Platformu), kullanıcıların kişiselleştirilmiş öğrenme planları oluşturmasına ve takip etmesine yardımcı olan bir mikro-öğrenme platformudur. Platform, **yapay zeka destekli** içerik üretimi ile öğrenme deneyimini kişiselleştirir ve adaptif öğrenme yöntemleri kullanır.

## 🎯 Projenin Temel Amacı

Bu platform, kullanıcıların:
- Kendi öğrenme hedeflerini belirlemelerine
- Günlük zaman ayırabilecekleri süreyi planlamalarına
- Öğrenme stillerine (görsel, işitsel, pratik, okuma) göre özelleştirilmiş içerik almalarına
- Modüler ve aşamalı bir öğrenme yolu izlemelerine
- İlerlemelerini takip etmelerine ve değerlendirmelerine

olanak sağlar.

## 🤖 LLM (Large Language Model) Kullanımı

### ✅ EVET, LLM Kullanılıyor

Proje, **Google Gemini AI** modellerini yaygın şekilde kullanmaktadır:

#### Kullanılan Modeller:
1. **Gemini 2.5 Flash** - Ana model (hızlı yanıtlar için)
2. **Gemini 2.5 Pro** - Yedek model (flash başarısız olursa)
3. **Gemini 1.5 Flash** - İçerik üretimi için

#### LLM Kullanım Alanları:

##### 1. **Öğrenme Planı Oluşturma** (`/api/generate-plan`)
- Kullanıcının hedeflerine göre kişiselleştirilmiş öğrenme planı üretir
- Modül sayısı, zorluk seviyesi ve öğrenme stiline göre özelleştirilir
- Örnek: "Python öğrenmek istiyorum, 4 hafta sürem var" → AI tam bir eğitim programı oluşturur

##### 2. **Modül İçerik Üretimi** (`/api/generate-module-content`)
Her modül için 4 farklı bölümde AI içerik üretir:

- **Giriş ve Temel Kavramlar**: AI, konuyu sıfırdan öğretecek şekilde giriş hazırlar
- **Detaylı Açıklamalar**: Tarihsel gelişim, metodolojiler, örnekler ve video önerileri
- **Uygulamalı Görevler**: Pratik görevler, adım adım talimatlar ve tamamlanma kriterleri
- **Özet ve Değerlendirme**: Kapsamlı özet, değerlendirme soruları ve performans göstergeleri

##### 3. **Öğrenci Değerlendirme** (`/api/evaluate-student-progress`)
- Öğrencinin cevaplarını analiz eder
- Anlama seviyesini (1-5 arası) belirler
- Güçlü ve zayıf yönleri tespit eder
- Bir sonraki modülün zorluk seviyesini adaptif olarak ayarlar (daha kolay/aynı/daha zor)
- Detaylı geri bildirim ve öneriler sağlar

#### Teknik Detaylar:
```typescript
// Örnek AI Çağrısı
const { text } = await generateText({
  model: google('gemini-2.5-flash'),
  prompt: prompt,
  maxOutputTokens: 8192,
  temperature: 0.0-0.7, // Tutarlılık için düşük sıcaklık
  topP: 0.1
});
```

## 🔍 RAG (Retrieval-Augmented Generation) Kullanımı

### ❌ HAYIR, RAG Kullanılmıyor

Proje şu anda **RAG (Retrieval-Augmented Generation)** teknolojisi kullanmamaktadır.

#### RAG Nedir?
RAG, büyük dil modellerinin bilgi tabanlarından (vektör veritabanları) ilgili bilgileri çekerek daha doğru ve güncel cevaplar üretmesini sağlayan bir tekniktir.

#### Projede RAG Olmamasının Nedenleri:
1. **Doğrudan LLM Kullanımı**: İçerikler doğrudan Gemini modelinin kendi bilgisinden üretiliyor
2. **Vektör Veritabanı Yok**: Pinecone, Weaviate, Qdrant gibi vektör veritabanı kullanımı yok
3. **Embedding İşlemi Yok**: Metin embedding veya similarity search yapılmıyor
4. **Harici Bilgi Kaynağı Yok**: Model, external kaynaklardan veri çekmiyor

#### RAG Eklenebilir mi?
Evet, gelecekte şu şekillerde RAG eklenebilir:
- Eğitim materyalleri bir vektör veritabanına yüklenebilir
- Kullanıcı soruları için ilgili dökümanlar çekilip LLM'e context olarak verilebilir
- Video içerikleri, makaleler ve kaynak belgeler indexlenebilir
- Böylece daha güncel ve spesifik bilgiler üretilebilir

## 🛠️ Teknoloji Stack

### Frontend:
- **Next.js 15.2.4** (React 19)
- **TypeScript**
- **Tailwind CSS** - Styling
- **Radix UI** - UI bileşenleri
- **Lucide React & React Icons** - İkonlar

### Backend & AI:
- **Next.js API Routes** - Backend API
- **Supabase** - Veritabanı ve Authentication
- **Google Gemini AI** (`@ai-sdk/google`, `@google/generative-ai`)
- **Vercel AI SDK** (`ai` paketi)

### Database (Supabase):
- `users` - Kullanıcı bilgileri
- `learning_plans` - Öğrenme planları
- `modules` - Modüller
- `module_contents` - AI tarafından üretilen içerikler
- `student_progress` - Öğrenci ilerlemeleri
- `practical_tasks` - Pratik görevler
- `task_submissions` - Görev gönderileri

## 🎓 Temel Özellikler

### 1. **Kişiselleştirilmiş Öğrenme**
- Öğrenme hedefi belirleme
- Günlük zaman planlaması (15 dk, 30 dk, 1 saat, 2 saat)
- Süre seçimi (2, 4, 8, 12 hafta)
- Öğrenme stili (görsel, işitsel, pratik, okuma)
- Hedef seviye (başlangıç, orta, ileri)

### 2. **AI Destekli İçerik Üretimi**
- Her modül için özgün içerik
- Öğrenme stiline uygun materyal
- Video önerileri ve kaynaklar
- İnteraktif görevler

### 3. **Adaptif Öğrenme**
- Öğrenci performansına göre zorluk ayarı
- Güçlü/zayıf yönlerin tespiti
- Kişiselleştirilmiş geri bildirim
- Sonraki modül önerileri

### 4. **Modüler Yapı**
- Aşamalı ilerleyen modüller
- Quiz ve exam modülleri
- Modül tamamlama takibi
- İlerleme göstergeleri

### 5. **Kullanıcı Yönetimi**
- Supabase Authentication
- Kullanıcı profilleri
- Çoklu plan desteği
- Plan aktif/pasif durumu

## 📊 Veri Akışı

```
Kullanıcı → Plan Oluştur → Gemini AI → Kişiselleştirilmiş Plan → Supabase

Modül Seç → İçerik Üret → Gemini AI → 4 Bölüm İçerik → Supabase

Değerlendirme → Cevaplar → Gemini AI → Performans Analizi → Adaptif Ayar
```

## 🚀 Öne Çıkan Noktalar

1. **Tam AI Entegrasyonu**: Sadece basit templat değil, her kullanıcı için özgün içerik
2. **Adaptif Sistem**: Öğrenci performansına göre dinamik ayarlama
3. **Kapsamlı Değerlendirme**: AI ile detaylı analiz ve geri bildirim
4. **Çok Yönlü İçerik**: Metin, video önerileri, pratik görevler, değerlendirmeler
5. **Modern Stack**: Next.js 15, React 19, TypeScript ile güncel teknolojiler

## 📈 Gelecek Geliştirme Fırsatları

### RAG Eklenmesi İçin:
1. **Vektör Veritabanı Entegrasyonu** (örn: Pinecone, Supabase Vector)
2. **Eğitim Materyali İndexleme**: YouTube videoları, makaleler, e-kitaplar
3. **Anlamsal Arama (Semantic Search)**: Kullanıcı sorularına en uygun kaynakları bulma
4. **Kaynak Gösterme**: Üretilen içerikte kaynak belirtme
5. **Güncel Bilgi**: Haber ve güncel gelişmeleri içerik üretimine dahil etme

### Diğer İyileştirmeler:
- Çoklu dil desteği
- Video içerik üretimi
- Sesli asistan
- Sosyal öğrenme özellikleri
- Oyunlaştırma (rozetler, liderlik tablosu)

## 🔐 Güvenlik ve Rate Limiting

- **Authentication**: Supabase Auth ile güvenli kullanıcı yönetimi
- **Rate Limiting**: IP bazlı rate limiting (örn: 5 istek/dakika)
- **Token Verification**: Her API çağrısında JWT token kontrolü
- **Authorization**: Kullanıcılar sadece kendi planlarına erişebilir

## 📝 Sonuç

**SkillMatchAI**, Google Gemini AI modellerini kullanarak kişiselleştirilmiş, adaptif bir mikro-öğrenme platformu sunmaktadır. **LLM kullanımı yaygın** şekilde plan oluşturma, içerik üretimi ve değerlendirme aşamalarında yer almaktadır. Ancak **RAG teknolojisi şu anda kullanılmamaktadır** - tüm içerikler LLM'in kendi bilgisinden üretilmektedir. Gelecekte RAG entegrasyonu ile daha güncel ve kaynak tabanlı içerik üretimi mümkün hale getirilebilir.

---

**Geliştirici**: Ali Altunoğlu  
**Platform**: Next.js + Supabase + Google Gemini AI  
**Deployment**: Vercel  
**Lisans**: Private
