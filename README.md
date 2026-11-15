# Solar Pulse

**Human first. Space next.**

Solar Pulse, astronotların günlük sağlık farkındalığını, egzersiz rutinlerini ve görev planlamasını tek bir çalışma alanında birleştiren bir **NASA Space Apps proje prototipidir**. Yerel çalışan Qwen yapay zekâ asistanı ve NASA kaynaklarına dayanan araştırma modu sayesinde, kurulum tamamlandıktan sonra internet veya Wi-Fi bağlantısı olmadan kullanılabilir.

> An offline-capable astronaut wellness and mission planning workspace, built with React, TypeScript, FastAPI and local Qwen inference. NASA research answers use a small curated local corpus with inspectable citations. This is an educational prototype, not an operational spacecraft or clinical system.

> **Paylaşım durumu:** Proje tanıtımı yayımlandı. Kaynak kodu aktarımı henüz tamamlanmadı; aşağıdaki kurulum komutları ve dosya bağlantıları tam proje paketi içindir.

## Ne yapar?

| Bölüm | İşlev |
| --- | --- |
| Dashboard | Sağlık demo kayıtları, görev ilerlemesi ve günlük rutinlerin ortak özeti |
| Health Monitoring | Nabız, kan oksijeni, uyku, egzersiz, cilt sıcaklığı ve ölçüm ayrıntıları; veri kaynağı ve kullanılabilirlik durumları |
| Daily Exercise Goal | Adım sayısı yerine kaydedilmiş egzersiz süreleri: koşu bandı, bisiklet ve direnç antrenmanı; başlangıç demosunda 95/120 dakika, hesaplanan %79 ilerleme |
| Mission Planner | Günlük/haftalık plan, kişisel görevler, görev kökenleri, çakışmalar ve korunmuş dinlenme aralıkları |
| AI Workspace | Gerçek yerel Qwen yanıtları, akış, durdurma, yeniden deneme ve kalıcı sohbet geçmişi |
| NASA Research | Dört onaylı NASA kaynağından yerel pasaj araması; kaynak adı, bağlantı, alınma zamanı ve okunabilir destekleyici metin |
| Library | Kullanıcının tek tek onayladığı ve etkinleştirdiği anılar; isteğe bağlı bağlam paylaşımı |
| Schedules & Reports | Hatırlatıcılar, bildirimler, görev geçmişi, egzersiz eğilimleri ve JSON dışa aktarma |
| Mission Environments | ISS, Ay ve Mars gibi eğitim senaryoları; isteğe bağlı rutin katılım başarıları ve NASA temelli sağlık eğitimi |

## Nasıl çalışır?

Tarayıcıdaki React arayüzü, aynı bilgisayarda çalışan FastAPI servisine bağlanır. FastAPI izin verilmiş sohbet bağlamını doğrular ve LM Studio üzerinden yerel **Qwen3.8-27B Q4_K_M** modeline iletir. Yanıtlar Server-Sent Events ile parça parça gösterilir. Başarısız veya iptal edilmiş kısmi yanıtlar tamamlanmış mesaj olarak kaydedilmez.

NASA araştırması modelin yeniden eğitilmesine dayanmaz. Küçük bir RAG akışı, önceden indirilmiş NASA metinlerini parçalara ayırır, yerel sözcüksel aramayla ilgili pasajları seçer ve yalnızca sınırlı miktarda kanıtı modele verir. Kaynak kimlikleri doğrulanır; kullanıcı alıntının dayandığı pasajı inceleyebilir. Araştırma soruları ve kişisel sağlık bilgileri NASA'ya gönderilmez. Bu mod canlı web araması değildir.

Görevler, sohbetler, tercihler ve onaylanmış anılar tarayıcının yerel depolamasında tutulur. Aynı tarayıcı profili ve aynı `http://localhost:5173` adresi kullanılmalıdır. Farklı adres veya port farklı bir depolama alanıdır.

## Amaç ve beklenen etki

Uzay görevlerinde bağlantı gecikmesi, sınırlı iletişim, yoğun iş yükü ve mikro yerçekimine uyarlanmış fiziksel aktivite ihtiyaçları birlikte düşünülmelidir. Solar Pulse, bu koşullarda günlük rutini daha anlaşılır ve erişilebilir kılmayı hedefler. Amaç; egzersiz ve dinlenme farkındalığını artırmak, planlama yükünü azaltmak ve güvenilir eğitim kaynaklarına bağlantı kesildiğinde de erişim sağlamaktır. Bu hedeflerin tıbbi veya operasyonel etkisi henüz saha çalışmalarıyla doğrulanmamıştır.

Projenin yaratıcı tarafı, sağlık görünümünü yalnızca bir ölçüm paneli olarak ele almamasıdır: görev planı, mikro yerçekimine uygun egzersiz hedefi, isteğe bağlı kişisel bağlam ve kaynakları görülebilen yerel yapay zekâ aynı deneyimde bir araya gelir. Adım sayısı astronot aktivitesinin güvenilir ölçüsü kabul edilmez; ilerleme egzersiz kayıtlarındaki sürelerden hesaplanır.

Tasarım ve geliştirme sırasında mahremiyet, kullanıcı onayı, kesintili bağlantı, sınırlı RAM/VRAM, okunabilir arayüz, mobil kullanım, veri tutarlılığı ve mevcut görev geçmişinin korunması dikkate alınmıştır. Katılım başarıları klinik sağlık puanı olarak sunulmaz; yapay zekâ komutan görevlerini veya görev takvimini kendiliğinden değiştirmez.

## Kullanılan teknolojiler

- **Arayüz:** React 19, TypeScript, Vite, CSS ve Lucide ikonları; yerel fontlar ve yeniden kullanılabilir grafik bileşenleri.
- **Backend:** Python, FastAPI, Uvicorn ve HTTPX.
- **Yapay zekâ:** LM Studio, yerel Qwen3.8-27B Q4_K_M, SSE akışı ve sınırlı sohbet bağlamı.
- **Araştırma:** Python HTML ayrıştırma, normalize edilmiş metin parçaları, yerel JSON önbelleği ve sözcüksel sıralama; vektör veritabanı gerektirmez.
- **Doğrulama:** TypeScript typecheck, ESLint, Node test runner ve pytest.
- **Test bilgisayarı:** AMD Ryzen 9 8940HX, yaklaşık 30 GiB RAM ve 8 GB VRAM'li NVIDIA RTX 5070 Laptop GPU. Bu bir evrensel minimum gereksinim değildir.

Paylaşılan web arayüzü Windows ve Linux tarayıcılarında kullanılmak üzere hazırlanmıştır. Gerçek çalışma testleri Fedora/Linux üzerinde yapılmıştır; native masaüstü paketleme henüz tamamlanmamıştır.

## Kurulum

Gerekenler: Node.js **22.13+**, npm, uyumlu Python 3 ve LM Studio. Model ağırlıkları repoya dahil değildir. İnternetsiz kullanım öncesinde bağımlılıklar ve model bir kez kurulmuş veya bilgisayara aktarılmış olmalıdır.

```bash
git clone https://github.com/ilyascinar593-ops/solar-pulse.git
cd solar-pulse
npm ci
python3 -m venv backend/.venv
backend/.venv/bin/python -m pip install -r backend/requirements-dev.txt
cp backend/.env.example backend/.env
```

Windows PowerShell'de Python kurulumu için:

```powershell
py -m venv backend/.venv
backend/.venv/Scripts/python.exe -m pip install -r backend/requirements-dev.txt
Copy-Item backend/.env.example backend/.env
```

Mevcut `.env` dosyanız varsa üzerine yazmayın. LM Studio'ya kurulu Qwen modelinin gerçek kimliğini `backend/.env` içindeki `LM_STUDIO_MODEL_ID` alanına girin. Gerekliyse API tokenını yalnızca bu özel dosyada tutun; tarayıcı koduna veya GitHub'a eklemeyin.

### İnternetsiz çalıştırma

```bash
npm run offline
```

**http://localhost:5173/#assistant** adresini açın ve terminali açık bırakın. Başlatıcı kurulu bağımlılıklarla üretim derlemesini oluşturur, yerel LM Studio sunucusunu/modelini kontrol eder ve arayüz ile API'yi loopback üzerinde sunar. Model veya paket indirmez. Yerel fontlar ve kayıtlı NASA pasajları internet gerektirmez. Kaynak web sitelerini açmak veya NASA önbelleğini yenilemek internet gerektirir.

Daha fazla bilgi: [çevrimdışı kullanım](docs/OFFLINE.md) ve [backend kurulumu](backend/README.md).

### Geliştirme ve test

Backend için `backend/README.md` içindeki başlatma adımlarını uygulayın; başka terminalde:

```bash
npm run dev -- --host 127.0.0.1
npm run typecheck
npm run lint
npm test
npm run build
backend/.venv/bin/python -m pytest backend/tests -q
```

Son yerel doğrulama: **43 frontend testi, 30 backend testi**, typecheck, lint ve production build başarılı. Backend testlerinde mevcut Starlette/HTTPX deprecation uyarısı vardır. Dış IP bağlantılarının engellendiği uygulama doğrulamasında gerçek Qwen sohbeti ve NASA kaynaklı yanıt tamamlanmıştır; bilgisayarın Wi-Fi ayarı değiştirilmemiştir.

27B model, bu donanımda özellikle uzun yanıtlarda yavaş olabilir. Ayrıntılı ve sınırlamaları belirtilmiş gerçek ölçümler: [Qwen optimizasyonu ve NASA RAG raporu](docs/QWEN-PERFORMANCE-RAG.md).

## NASA bilgi kaynakları

- [5 Hazards of Human Spaceflight](https://www.nasa.gov/hrp/hazards/)
- [Astronaut Exercise](https://www.nasa.gov/general/astronaut-exercise/)
- [Counteracting Bone and Muscle Loss in Microgravity](https://www.nasa.gov/humans-in-space/counteracting-bone-and-muscle-loss-in-microgravity/)
- [Isolation and Confinement](https://www.nasa.gov/hrp/hazard-isolation-and-confinement/)

Kaynaklar NASA'ya aittir; repodaki önbellek kaynak bağlantıları ve alınma tarihlerini içerir. Solar Pulse resmi bir NASA ürünü değildir ve NASA onayı iddia etmez.

## Sınırlar ve gelecek çalışmalar

- Sağlık kayıtları açıkça etiketlenmiş deterministik **demo verileridir**. Canlı Galaxy Watch7/telefon bağlantısı ve ECG klinik yorumu uygulanmamıştır; veri sağlayıcı mimarisi gelecekteki entegrasyona açıktır.
- Tıbbi teşhis, ilaç önerisi, saatten kemik yoğunluğu ölçümü veya uzay aracı kontrolü yapılmaz.
- RAG yalnızca küçük yerel koleksiyonu arar. Atıf denetimi her iddianın doğruluğunu kanıtlayan tam bir anlamsal doğrulayıcı değildir.
- Depolama yereldir; şifreli klinik veri deposu, hesap sistemi veya çok cihazlı senkronizasyon yoktur. Uygulama kapalıyken hatırlatıcı teslimi garanti edilmez.
- Herkese açık backend dağıtımı, kimlik doğrulama ve klinik/operasyonel doğrulama ayrı gelecek çalışmalardır.

## Dosya yapısı

```text
src/                 React sayfaları, ortak durum, veri sağlayıcıları ve servisler
backend/app/         FastAPI, Qwen istemcisi ve NASA bilgi servisi
backend/data/        Kaynak bilgileriyle sınırlı NASA önbelleği
backend/tests/       API, akış ve araştırma testleri
public/              Yerel fontlar, lisans bildirimleri ve favicon
scripts/             İnternetsiz yerel başlatıcı
tests/               Frontend ve ortak iş mantığı testleri
docs/                Uygulama raporları, ölçümler ve demo görselleri
```

Özel `.env` ayarları, erişim anahtarları, kişisel sohbet/sağlık dışa aktarımları, model ağırlıkları, sanal ortam, `node_modules` ve derleme çıktıları bu kaynak paylaşımına dahil edilmez. Fontların lisans bildirimleri `public/fonts/` içinde korunur.
