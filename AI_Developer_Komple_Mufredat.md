# AI Developer Olma Yolculuğu — Komple Müfredat

> **Kime göre:** Bilgisayar mühendisi, temel Python/numpy/pandas bilgisi var, işi baştan
> sağlam temelle öğrenmek istiyor. Günde ~5 saat, süre baskısı yok, proje odaklı.
>
> **Felsefe:** Fine-tuning en sonda. Önce sağlam temel (Python + veri + SQL + matematik
> sezgisi), sonra LLM temelleri, sonra işin kalbi olan **RAG + Vektör Veritabanları**,
> sonra Agent'lar, en son fine-tuning ve production. Her fazın sonunda GitHub'a giren
> gerçek bir proje var — çünkü "AI Developer" ünvanını sana projeler kazandıracak.

---

## Yolculuğun Haritası (Kuşbakışı)

| Faz | Konu | Tahmini süre (günde 5 saat) | Faz Projesi |
|---|---|---|---|
| **0** | Ortam + araç kurulumu | 1 gün | Çalışan geliştirme ortamı |
| **1** | Python (AI için gereken kısımlar) | 3-4 gün | Veri işleyen CLI aracı |
| **2** | Veri: numpy, pandas, görselleştirme | 3-4 gün | Veri analizi mini-raporu |
| **3** | SQL + veri modelleme | 2-3 gün | Sorgu portföyü + Python entegrasyonu |
| **4** | Matematik sezgisi (lineer cebir, olasılık) | 2-3 gün | Elle embedding benzerlik hesabı |
| **5** | LLM temelleri + API + Prompt Engineering | 4-5 gün | Akıllı metin analiz aracı |
| **6** | Embedding + Vektör Veritabanları | 3-4 gün | Semantik arama motoru |
| **7** | RAG (işin kalbi) | 5-7 gün | **Kendi dokümanlarınla konuşan asistan** |
| **8** | AI Agents + Function Calling + MCP | 4-6 gün | Araç kullanan otonom agent |
| **9** | Fine-Tuning (LoRA/QLoRA) | 4-6 gün | Özelleştirilmiş küçük model |
| **10** | Evaluation, LLMOps, Deployment, Security | 4-5 gün | Canlıya alınmış RAG API'si |
| **11** | Bitirme projesi + portföy | 5-7 gün | Uçtan uca AI ürünü |

**Toplam:** kabaca 8-10 hafta (günde 5 saat, hafta içi). Acele yok — her fazı
"anladım + proje çalışıyor" seviyesine getirmeden geçme.

---

# FAZ 0 — Ortam ve Araçlar (1 gün)

**Amaç:** Bir daha kurulumla uğraşmamak. Tüm araçlar hazır.

### Kurulacaklar
- **Python 3.11+** ve `venv` (her proje için ayrı sanal ortam alışkanlığı)
- **VS Code** + eklentiler: Python, Jupyter, GitLens, Ruff (linter)
- **Git + GitHub hesabı** — repo: `ai-developer-yolculuk`, her faz için klasör
- **Anthropic API key** (console.anthropic.com) — ücretsiz başlangıç kredisiyle
- **Docker** (ileride vektör DB ve deployment için lazım olacak, şimdi sadece kur)

### Görevler
1. `ai-developer-yolculuk` reposunu aç, README'ye bu müfredatı özet olarak koy.
2. İlk `venv` oluştur, `anthropic` SDK'sini kur, "merhaba dünya" API isteği at.
3. Jupyter'da ilk notebook'u çalıştır.

**Faz çıktısı:** Terminalden `python -c "import anthropic"` hatasız çalışıyor ve ilk
commit GitHub'da.

---

# FAZ 1 — Python (AI İçin Gereken Kısımlar) (3-4 gün)

Sen zaten mühendissin, dilin sözdizimini biliyorsun. Bu faz "her şeyi baştan öğren"
değil, **AI/veri işinde sürekli kullanacağın Python kaslarını** keskinleştirmek.

### Mutlaka sağlam olması gerekenler
- **Veri yapıları:** list, dict, set, tuple — ne zaman hangisi, karmaşıklıkları
- **Comprehension'lar:** list/dict/set comprehension (veri dönüştürmede sürekli lazım)
- **Fonksiyonlar:** `*args`, `**kwargs`, default değerler, lambda
- **Iteratörler & generator'lar:** `yield`, büyük veri akışlarında bellek dostu işleme
- **Dosya işlemleri:** JSON, CSV, JSONL okuma/yazma (fine-tuning verisi JSONL!)
- **Hata yönetimi:** `try/except`, custom exception'lar (API çağrılarında kritik)
- **Type hints:** `def f(x: str) -> dict:` — modern AI kodunun standardı
- **Sınıflar & dataclass'lar:** `@dataclass` ile temiz veri modelleri
- **Async temeli:** `async/await` — API'lere paralel istek atarken çok işine yarayacak
- **Virtual environment & pip/requirements.txt** disiplini

### İzlenecek/okunacak kaynaklar
- **Real Python** (realpython.com) — konu konu, kaliteli, ücretsiz makaleler
- **Corey Schafer — Python Tutorials** (YouTube) — OOP, generator, decorator için net anlatım
- İleri: **Fluent Python** (kitap) — referans olarak, baştan sona değil

### Görevler
1. Bir JSONL dosyası oluştur, satır satır oku, her satırı dict'e çevir, filtrele, yeni
   JSONL olarak yaz (fine-tuning veri hazırlığının provası).
2. Bir generator yaz: büyük bir metin dosyasını satır satır, belleğe tümünü almadan işlesin.
3. `@dataclass` ile bir `Document` modeli tanımla (id, text, metadata) — Faz 7'de RAG'de
   bunu kullanacaksın.

**Faz projesi:** Komut satırından çalışan bir **veri temizleme aracı** — bir CSV alsın,
eksik/bozuk satırları ayıklasın, temiz çıktı üretsin, işlem özetini raporlasın.

---

# FAZ 2 — Veri Bilimi Temelleri: numpy, pandas, Görselleştirme (3-4 gün)

"Yapay zekada veri olmazsa sonuç olmaz" dedin — çok doğru. Bu faz o veri kasını kuruyor.
Veri bilimci kadar derin değil ama bir AI Developer'ın veriyi eline alıp anlayabilecek,
temizleyebilecek seviyesi.

### numpy (1 gün)
- ndarray, shape, dtype, broadcasting
- Vektör/matris işlemleri, `dot`, `matmul` — **embedding benzerliği bununla hesaplanır**
- Eksen (axis) mantığı, `mean/sum/argmax`
- Neden önemli: her embedding bir numpy vektörü, her benzerlik bir dot product

### pandas (1.5 gün)
- Series, DataFrame, indeksleme (`loc`, `iloc`)
- Eksik veri (`isna`, `fillna`, `dropna`) — gerçek veride en çok vakit alan kısım
- `groupby`, `merge`, `pivot` — veriyi anlamlandırma
- CSV/JSON/Parquet okuma-yazma
- Kaynak: **pandas resmi "10 minutes to pandas"** + **Kevin Markham / Data School** (YouTube)

### Görselleştirme (0.5 gün)
- matplotlib temel, seaborn ile hızlı grafikler
- Dağılım, korelasyon, eksik veri haritası görselleştirme

### Görevler
1. Gerçek bir dataset indir (Kaggle'dan örn. bir e-ticaret ya da film verisi), pandas ile
   yükle, eksik verileri raporla, temizle.
2. numpy ile iki cümlenin (elle verilmiş sahte embedding'lerle) kosinüs benzerliğini hesapla.
3. seaborn ile 3-4 anlamlı grafik çıkar.

**Faz projesi:** Bir veri setini baştan sona analiz eden **keşifsel veri analizi (EDA)
notebook'u** — yükle, temizle, görselleştir, 5 madde çıkarım yaz.

---

# FAZ 3 — SQL ve Veri Modelleme (2-3 gün)

SQL'in işine yarar dedin, kesinlikle. RAG'de metadata filtreleme, pgvector (Postgres
tabanlı vektör DB), analitik — hepsi SQL istiyor.

### Öğrenilecekler
- `SELECT, WHERE, ORDER BY, LIMIT`
- `JOIN` türleri (inner, left, right) — en kritik konu
- `GROUP BY, HAVING`, aggregate fonksiyonlar
- Alt sorgular (subquery), CTE (`WITH`)
- İndeksleme mantığı (neden sorgular hızlanır)
- **PostgreSQL** kur (ileride pgvector için zaten lazım)
- Python'dan SQL: `sqlite3`, `SQLAlchemy` temeli, `psycopg2`

### Kaynaklar
- **SQLBolt** (sqlbolt.com) — interaktif, ücretsiz, hızlı
- **Mode SQL Tutorial** — gerçek dünya senaryoları
- **PostgreSQL Exercises** (pgexercises.com) — pratik için

### Görevler
1. SQLite'ta küçük bir veritabanı kur (users, orders tabloları), JOIN'li sorgular yaz.
2. Python'dan bu veritabanına bağlan, sorgu sonucunu pandas DataFrame'e çek.
3. Bir CTE ile çok adımlı bir analitik sorgu yaz.

**Faz projesi:** Bir veri setini SQLite/Postgres'e yükleyen + 10 anlamlı analitik sorgu
içeren, Python'dan çalıştırılabilir bir **SQL portföyü**.

---

# FAZ 4 — Matematik Sezgisi (2-3 gün)

Sıfırdan matematik değil, **AI'yı anlamak için gereken sezgi**. Mühendis olduğun için
formülleri değil, "ne işe yaradığını" hedefliyoruz.

### Lineer cebir (1.5 gün)
- Vektör, matris, boyut (dimension)
- Nokta çarpım (dot product) ve **kosinüs benzerliği** — embedding'lerin kalbi
- Matris çarpımı sezgisi (neural network'ün temel işlemi)
- Vektör uzayı: "anlamca yakın = uzayda yakın" mantığı

### Olasılık & istatistik (0.5 gün)
- Olasılık dağılımı, softmax (LLM'in bir sonraki token'ı nasıl seçtiği)
- Ortalama, varyans, normalizasyon

### Kalkülüs (sadece sezgi, 0.5 gün)
- Türev = "eğim/değişim", gradyan (gradient) = "hatayı azaltma yönü"
- Gradient descent'i kavramsal olarak anla (fine-tuning'de lazım olacak)

### Kaynaklar (bunlar altın değerinde)
- **3Blue1Brown — "Essence of Linear Algebra"** serisi (YouTube) — en iyi görsel anlatım
- **3Blue1Brown — "Neural Networks"** serisi — attention dahil
- **StatQuest (Josh Starmer)** — istatistik/ML kavramları için sabırlı anlatım

### Görevler
1. numpy ile: 5 kelimenin sahte embedding'ini oluştur, aralarındaki kosinüs benzerliğini
   hesapla, bir matris olarak yazdır.
2. Softmax fonksiyonunu numpy ile elle yaz, bir skor vektörüne uygula.

**Faz projesi:** "Embedding benzerliği nasıl çalışır" konulu, kendi numpy kodunla
gösterdiğin küçük bir **açıklamalı notebook** (hem öğrenirsin hem portföy).

---

# FAZ 5 — LLM Temelleri + API + Prompt Engineering (4-5 gün)

Artık gerçek AI'ya giriyoruz. PDF'indeki Aşama 1'in kalbi burası.

### LLM nasıl çalışır (1 gün)
- Language model = bir sonraki token'ı tahmin eden istatistiksel model
- Tokenization: `tiktoken` ile bir cümleyi token'lara böl, gör
- Embedding: token → vektör
- Transformer & Attention: 3Blue1Brown'ın attention videosu (Faz 4'te başladıysan tamamla)
- Context window, sampling (temperature/top-k/top-p), hallucination

### API ile çalışma (1 gün)
- Anthropic (Claude) ve/veya OpenAI SDK
- `messages` yapısı, system prompt, roller
- `temperature` ve diğer parametrelerin etkisini canlı test et
- Streaming, token sayımı, maliyet hesabı
- Hata yönetimi, rate limit, retry

### Prompt Engineering (2 gün)
- **Anthropic'in resmi ücretsiz kursu:** `github.com/anthropics/prompt-eng-interactive-tutorial`
  (9 bölüm, Jupyter, kendi API key'inle pratik — sektörün en saygın kaynaklarından)
- System prompt, zero-shot vs few-shot
- Chain of Thought (adım adım düşündürme)
- Structured output / JSON mode
- Prompt chaining (bir çıktıyı diğerine besleme)

### Görevler
1. Aynı prompt'u temperature 0 ve 1 ile çalıştır, tutarlılık farkını raporla.
2. Modeli kasıtlı olarak halüsinasyona düşür (olmayan bir şey sor), gözlemle → RAG
   ihtiyacını hisset.
3. Anthropic kursunun 1-6. bölümlerini bitir, egzersizleri gerçekten çalıştır.

**Faz projesi:** **Akıllı metin analiz aracı** — system prompt + few-shot + JSON mode ile
bir metni alıp `{özet, duygu, anahtar_kelimeler, kategori}` şemasında yapılandırılmış
sonuç döndüren CLI aracı. (Bu, Faz 7'deki RAG projesinin çekirdeği olacak.)

---

# FAZ 6 — Embedding + Vektör Veritabanları (3-4 gün)

Sen de fark etmişsin: RAG'in temeli vektör veritabanı mantığı. Bu fazı ayrı tutuyorum
çünkü RAG'e girmeden önce sağlam oturması lazım.

### Embedding'ler (1 gün)
- Embedding modelleri: `text-embedding-3` (OpenAI), `bge`, `e5` (açık kaynak)
- Bir metni embedding'e çevir, boyutunu (örn. 1536) gör
- Kosinüs benzerliği ile iki metnin anlamsal yakınlığını ölç (Faz 4'ün kodunu gerçek
  embedding'lerle tekrarla)

### Vektör Veritabanları (2 gün)
- **Neden gerekli:** milyonlarca vektörde hızlı benzerlik araması (brute-force yavaş)
- ANN (Approximate Nearest Neighbor) mantığı — sezgisel olarak
- Araçlar:
  - **Chroma** — başlamak için en kolay, yerel çalışır (bununla başla)
  - **pgvector** — Postgres eklentisi (Faz 3'teki SQL bilgin burada işe yarayacak!)
  - **Pinecone / Weaviate / Qdrant** — production ölçeği (genel bilgi düzeyinde tanı)
- Chunking: uzun dokümanı anlamlı parçalara bölme stratejileri
- Metadata filtreleme (SQL bilgin burada devreye girer)

### Görevler
1. Chroma kur, 20-30 cümlelik bir metin koleksiyonunu embedding'leyip vektör DB'ye at.
2. Bir sorgu ver, en yakın 3 sonucu getir (semantik arama).
3. Aynısını pgvector ile Postgres'te yap — SQL + vektör kombinasyonunu gör.

**Faz projesi:** **Semantik arama motoru** — bir makale/blog koleksiyonu ver, kullanıcı
doğal dilde sorsun, en alakalı parçaları vektör benzerliğiyle bulup göstersin.

---

# FAZ 7 — RAG: İşin Kalbi (5-7 gün)

Bu faz müfredatın en önemli parçası. Faz 5 (prompt) + Faz 6 (vektör DB) burada birleşiyor.

### RAG mantığı (1 gün)
- Neden RAG: modeli yeniden eğitmeden güncel/özel bilgiyle doğru cevap ürettirmek
- RAG pipeline: **Yükle → Chunk → Embed → Sakla → Retrieve → Prompt'a ekle → Cevap üret**
- RAG vs Fine-tuning: ne zaman hangisi (bilgi eklemek = RAG, üslup/format = fine-tuning)

### Retrieval kalitesi (2 gün)
- Chunking stratejileri (sabit boyut, cümle/paragraf bazlı, overlap)
- Retrieval / similarity search ayarları (kaç sonuç, eşik değeri)
- **Reranking:** ilk sonuçları daha güçlü modelle yeniden sıralama
- Hybrid search (anahtar kelime + semantik)

### Framework'ler (1 gün)
- **LangChain** veya **LlamaIndex** — RAG akışını kolaylaştıran kütüphaneler
- Önce ham (framework'süz) yaz, mantığı anla; sonra framework'e geç (bu sırayla öğren!)

### Değerlendirme (1 gün)
- RAG'i nasıl test edersin: doğru chunk geldi mi, cevap dayanaklı mı
- **Ragas** gibi araçlarla otomatik değerlendirmeye giriş

### Görevler
1. Framework'süz, saf Python + Chroma ile mini bir RAG yaz (mantığı kavramak için).
2. Aynısını LangChain/LlamaIndex ile yeniden yaz, farkı gör.
3. Chunking boyutunu değiştir, cevap kalitesine etkisini gözlemle.
4. Reranking ekle, öncesi/sonrasını karşılaştır.

**Faz projesi:** **"Kendi dokümanlarınla konuşan asistan"** — PDF/metin dosyaları yükle,
soru sor, sistem ilgili parçaları bulup dayanaklı (kaynak gösteren) cevap versin. Bu,
portföyünün amiral gemisi projesi olacak. Basit bir web arayüzü (Streamlit/Gradio) ekle.

---

# FAZ 8 — AI Agents + Function Calling + MCP (4-6 gün)

Model artık sadece cevap vermiyor, **araç kullanıp iş yapıyor**.

### Function Calling / Tool Use (1.5 gün)
- Modele "şu fonksiyonları kullanabilirsin" deme, modelin doğru anda çağırması
- Bir hesap makinesi, bir hava durumu API'si, bir arama fonksiyonu bağla
- Tool call → sonuç → modele geri besleme döngüsü

### Agent kavramları (1.5 gün)
- Agent döngüsü: düşün → araç seç → çalıştır → gözlemle → tekrarla
- Memory (kısa/uzun vadeli) — agent'ın konuşmayı hatırlaması
- **Agent framework'leri:** LangChain, LlamaIndex, CrewAI (tanı ve birini kullan)

### MCP — Model Context Protocol (1 gün)
- Modellerin dış araçlara/verilere standart protokolle bağlanması (Anthropic öncülüğünde)
- Basit bir MCP server'a bağlanma / kullanma
- Kaynak: **Anthropic Academy'nin MCP kursu** (resmi, ücretsiz, sertifikalı)

### Multi-agent & otomasyon (1 gün)
- Multi-agent sistemler (planlayıcı + uygulayıcı rolleri)
- **n8n** — kod yazmadan görsel akışlarla LLM'i servislere bağlama (bir otomasyon kur)

### Görevler
1. Function calling ile modele gerçek bir API (örn. hava durumu) bağla.
2. RAG projeni bir agent'a çevir: model kendi karar versin, ne zaman doküman arayacağına.
3. n8n ile küçük bir otomasyon kur (örn. e-posta → özet → Slack).

**Faz projesi:** **Araç kullanan otonom agent** — birden fazla aracı (web arama +
hesaplama + senin RAG sistemin) olan, bir hedefi adım adım çözen bir agent.

---

# FAZ 9 — Fine-Tuning (LoRA/QLoRA) (4-6 gün)

En sona bıraktık çünkü en maliyetli ve en ileri konu. Artık altyapın hazır.

### Ne zaman / neden (0.5 gün)
- Sıralama: önce prompt → sonra RAG → **en son çare** fine-tuning
- Fine-tuning ne için: bilgi eklemek DEĞİL, kalıcı üslup/format/domain dili kazandırmak

### Veri hazırlama (1 gün)
- **Dataset preparation:** temiz, tutarlı örnek seti (senin Faz 1-2 verisi kasın burada)
- **JSONL formatı:** her satır bir JSON — fine-tuning'in standart formatı
- Train / validation / test split
- Data quality: "garbage in, garbage out" — az ama temiz > çok ama gürültülü

### Eğitim süreci kavramları (1 gün)
- Hyperparameters: learning rate, batch size, epoch
- Loss function & gradient descent (Faz 4 sezgisi burada somutlaşıyor)
- Overfitting ve validation ile tespiti
- Catastrophic forgetting

### Verimli yöntemler — asıl uygulayacağın (1.5 gün)
- **Full fine-tuning** (neden bugün nadiren tercih edilir)
- **PEFT** ailesi
- **LoRA** — ana ağırlıkları dondur, küçük adaptör katmanları eğit (hızlı, ucuz)
- **QLoRA** — quantize + LoRA, tek GPU'da bile çalışır
- **Quantization** (32-bit → 4-bit) mantığı
- Base model seçimi (Llama, Mistral, Qwen)

### Değerlendirme (0.5 gün)
- Evaluation metrics (accuracy, BLEU, perplexity — göreve göre)
- Human evaluation

### Kaynaklar
- **Hugging Face NLP Course** + **PEFT/TRL dökümantasyonu** (ücretsiz, kodlu)
- Google Colab (ücretsiz GPU) üzerinde QLoRA denemesi yapılabilir

### Görevler
1. Küçük bir JSONL veri seti hazırla (örn. belirli bir üslupta yanıt veren bir asistan).
2. Google Colab'da QLoRA ile küçük bir açık kaynak modeli (örn. bir Llama/Qwen türevi)
   fine-tune et.
3. Fine-tune öncesi/sonrası çıktıları karşılaştır, evaluation metrikleriyle ölç.

**Faz projesi:** Belirli bir görev/üslup için **fine-tune edilmiş küçük bir model** +
"neden fine-tuning'i seçtim, RAG neden yetmedi" açıklamalı raporu.

---

# FAZ 10 — Evaluation, LLMOps, Deployment, Security (4-5 gün)

Bir şeyi çalıştırmak başka, **güvenilir şekilde canlıda tutmak** başka.

### Evaluation & LLMOps (1.5 gün)
- LLM evaluation framework'leri: Ragas, DeepEval, promptfoo
- Observability: LangSmith / Langfuse ile çağrı, maliyet, gecikme, hata izleme
- Cost & latency optimizasyonu: caching, model seçimi, token yönetimi

### Deployment / Serving (1.5 gün)
- Modeli/uygulamayı API olarak sunma: **FastAPI** ile bir endpoint yaz
- Docker ile paketleme (Faz 0'da kurdun)
- Serving araçları: vLLM, TGI, Modal (genel tanı)
- Basit bir bulut deployment (Render/Railway/Fly.io gibi)

### AI Security (1 gün)
- **Prompt injection** — kötü niyetli girdilerle sistem talimatını atlatma
- **Jailbreaking** — güvenlik kısıtlarını aşma girişimleri
- **Guardrails** — girdi/çıktı filtreleme katmanları
- **Data privacy** — kullanıcı verisi nereye gidiyor, saklanıyor mu, eğitimde kullanılıyor mu

### Görevler
1. Faz 7'deki RAG'ini FastAPI ile API'ye çevir, Docker'la paketle.
2. Bir bulut servisine deploy et, gerçek bir URL'den çağır.
3. Basit bir guardrail ekle (istenmeyen içerik filtresi).
4. Langfuse ile çağrıları izle.

**Faz projesi:** **Canlıya alınmış RAG API'si** — Docker'lı, izlenebilir, guardrail'li,
gerçek bir URL'den erişilebilir.

---

# FAZ 11 — Bitirme Projesi + Portföy (5-7 gün)

Artık tek parça bir ürün. İş başvurusunda göstereceğin şey bu.

### Bitirme projesi fikirleri (birini seç, derinleştir)
- **Domain-özel akıllı asistan:** belirli bir alanda (hukuk, sağlık, finans dokümanları)
  RAG + agent + güzel arayüz + deployment
- **Doküman otomasyonu:** yüklenen belgeleri işleyip yapılandırılmış çıktı + aksiyon üreten sistem
- **Çok-agent'lı araştırma asistanı:** web arama + RAG + rapor üreten agent ekibi

### Portföy paketi
- GitHub: temiz README, mimari diyagramı, kurulum talimatı, demo GIF/video
- Canlı demo linki (deployment)
- Kısa bir teknik blog yazısı: "nasıl yaptım, hangi kararları neden verdim"
- LinkedIn: projeleri ve (aldıysan) sertifikaları öne çıkar

**Faz çıktısı:** İşverene "bak, ben AI Developer'ım" diyebileceğin, uçtan uca çalışan,
deploy edilmiş, açıklanmış bir ürün.

---

## Gerçek Değer Katan Sertifikalar (Udemy tarzı değil)

| Kaynak | Neden değerli | Ne zaman |
|---|---|---|
| **Anthropic Academy** (academy.anthropic.com) | Anthropic'in resmi ücretsiz platformu, gerçek sertifika (Skilljar), LinkedIn'e eklenebilir. Claude API, Claude Code, MCP, Agent Skills kursları. | Faz 5-8 boyunca ilgili kursları al |
| **DeepLearning.AI** (Andrew Ng) | Kısa, yoğun, ücretsiz kurslar ("ChatGPT Prompt Engineering for Developers", "LangChain for LLM App Dev", "Building & Evaluating RAG"). Coursera'da sertifikalı "Generative AI with LLMs" (AWS) da CV'de iyi durur. | Faz 5, 6, 7'de birebir örtüşür |
| **Hugging Face NLP Course** | Ücretsiz, kodlu; Transformers, tokenizer, fine-tuning'i gerçek kodla öğretir. | Faz 6 ve 9'da |
| **NVIDIA DLI** | "Building RAG Agents with LLMs" gibi sertifikalı, production/GPU odaklı kurslar. İşveren tanır. | Faz 7-10'da |
| **AWS Certified AI Practitioner** | Tanınırlığı artan, AI ürünlerini gerçek dünyada kullanma odaklı sertifika. | Portföy bittikten sonra, iş başvurusuna yakın |

**Strateji:** Sertifikaları faz konularıyla eşleştir — o fazı çalışırken ilgili kursu al,
hem öğren hem sertifikayı kazan. Ama önceliğin her zaman **çalışan projeler** olsun;
sertifika onları destekler, yerini tutmaz.

---

## Nasıl İlerleyelim

Her fazı bitirdiğinde bana "Faz X bitti, şurada zorlandım / şunu merak ediyorum" de.
O fazın gerçek gidişatına göre bir sonraki fazı **saat saat günlük plana** dökerim
(bugün Gün 1 için yaptığım gibi). Böylece bu genel müfredat iskelet olur, günlük planlar
da eti kemiği. İhtiyaca göre faz ekler/çıkarır, hızlandırır/yavaşlatırız.

Kolay gelsin — sağlam gidiyorsun.
