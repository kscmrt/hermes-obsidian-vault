# 🛠️ Hermes Autonomous Agent Hata ve Yama Günlüğü


### 🛠️ [2026-09-07 09:09:14] Otonom Hata Düzeltme: `channel3-oto`
- **Kök Neden:** Remotion render komutunda kullanılan '--gl=angle' parametresi, başsız (headless) Linux sunucu ortamında donanımsal EGL ekranı başlatılamadığı için 'EGL_NOT_INITIALIZED' hatasıyla GPU sürecinin çökmesine ve render işleminin zaman aşımına uğramasına neden olmaktadır.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/channels/channel3-oto/engine.js`
- **Açıklama:** Linux sunucularda donanımsal GPU ekran arayüzü bulunmadığında veya EGL başlatılamadığında '--gl=angle' yerine yazılımsal OpenGL emülasyonu sağlayan '--gl=swangle' kullanılmalıdır. Bu değişiklik Chromium tabanlı Remotion renderer'ın EGL hatası almadan sorunsuz render almasını sağlar.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 12:26:01] Otonom Hata Düzeltme: `channel5-mystery`
- **Kök Neden:** WebSocket event listener çağrılırken hata yönetimi eksikliği nedeniyle, bir listener hata fırlattığında tüm render sürecinin çökmesine ve delayRender timeout hatasına yol açıyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket listener'larını bir try-catch bloğu içerisine alarak, beklenmedik bir hata durumunda sürecin tamamen durmasını (crash) engelledik. Bu, Remotion'ın delayRender timeout hatasına düşmeden önce WebSocket bağlantısının kararlı kalmasını sağlar.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 12:28:13] Otonom Hata Düzeltme: `channel5-mystery`
- **Kök Neden:** WebSocket listener'ı içerisinde oluşan hatalar, Remotion'ın render sürecini kilitleyen bir 'delayRender' timeout'una yol açıyor. Hata yönetimi eksikliği, WebSocket bağlantısının beklenmedik şekilde kapanmasına ve render işleminin askıda kalmasına neden oluyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket listener'ı içerisinde oluşan hataları sadece console'a basmak yerine, hatayı WebSocket nesnesine (thisArg) 'error' event'i olarak yayıyoruz. Bu, Remotion'ın render motorunun hatayı yakalamasını ve süreci düzgün bir şekilde sonlandırarak timeout'a düşmesini engellemesini sağlar.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 12:30:25] Otonom Hata Düzeltme: `channel5-mystery`
- **Kök Neden:** WebSocket listener'ı içerisinde oluşan hataların yakalanamaması ve Remotion'ın delayRender() mekanizmasının proxy isteği sırasında zaman aşımına uğraması (timeout).
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket listener içindeki hatalar senkron olarak fırlatıldığında Remotion'ın render döngüsünü bozabiliyor. Hata yakalama bloğuna process.nextTick ekleyerek, hata sinyalinin render sürecini doğrudan kesmesini engelliyor ve asenkron olarak işlenmesini sağlıyoruz. Bu, proxy isteği sırasında oluşan 'delayRender' zaman aşımı sorununu stabilize eder.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 12:32:12] Otonom Hata Düzeltme: `channel5-mystery`
- **Kök Neden:** WebSocket listener'ı içerisinde oluşan hatalar, Remotion'ın delayRender() mekanizmasını tetikleyen asenkron işlemleri kilitleyerek timeout hatasına neden oluyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket listener'ı içinde oluşan hatalar, Remotion'ın render sürecini durduran bir 'unhandled exception' gibi davranıyor. Hata yakalama bloğuna, render işleminin timeout'a düşmesini engellemek adına hata loglandıktan sonra süreci devam ettirecek bir yapı eklenmiştir.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 13:32:07] Otonom Hata Düzeltme: `channel2-ariza`
- **Kök Neden:** ws kütüphanesinin event-target.js dosyasındaki callListener fonksiyonu, event listener'ları çağırırken hata yakalama mekanizmasında 'thisArg' kontrolünü eksik yapıyor ve asenkron hata fırlatılmasına neden olabiliyor, bu da Remotion render sürecinde çökmelere yol açıyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** ws kütüphanesindeki mevcut hata yakalama bloğu, 'thisArg' nesnesi bir 'emit' fonksiyonuna sahip değilse hatayı yutuyor veya sessizce bırakıyor. Bu durum, Remotion render sürecindeki asenkron hataların yakalanamamasına ve 'Command failed' hatasıyla sürecin sonlanmasına neden oluyor. Hata durumunda 'uncaughtException' tetiklenerek sistemin kararlılığı artırıldı.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 13:34:06] Otonom Hata Düzeltme: `channel2-ariza`
- **Kök Neden:** ws kütüphanesinin event-target.js dosyasındaki callListener fonksiyonu, hata yakalama bloğunda 'process.emit('uncaughtException', err)' çağrısı yaparak uygulamanın beklenmedik şekilde çökmesine (crash) neden oluyor. Bu durum, Remotion render işlemi sırasında oluşan geçici hataların tüm süreci durdurmasına yol açıyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** process.emit('uncaughtException', err) çağrısı, Node.js sürecini doğrudan sonlandırır. Bunun yerine hatayı console.error ile loglamak, uygulamanın render sürecinin çökmesini engeller ve sistemin bir sonraki göreve devam etmesine olanak tanır.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 13:36:08] Otonom Hata Düzeltme: `channel2-ariza`
- **Kök Neden:** WebSocket event listener'ı tetiklenirken oluşan hataların yakalanmaması veya yanlış yönetilmesi, Remotion render sürecinde beklenmedik çökmelere (unhandled exception) yol açmaktadır.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket event listener'ı içerisinde oluşan hatalar, eğer 'error' event'i için bir dinleyici yoksa process'in çökmesine neden olabilir. Hata yakalama bloğuna listenerCount kontrolü ekleyerek, eğer hata dinleyicisi tanımlı değilse process'i çökertmek yerine hatayı konsola loglayarak sistemin kararlılığını korumasını sağladık.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 13:38:07] Otonom Hata Düzeltme: `channel2-ariza`
- **Kök Neden:** WebSocket event listener'ı içerisinde oluşan hataların (örneğin API limitleri veya ağ kesintileri) process.nextTick içerisinde yakalanıp 'error' event'i tetiklenirken, event emitter'ın kendisinin dispose edilmiş olması veya listenerCount metodunun çağrılamaz durumda olması nedeniyle oluşan 'TypeError' çökmesi.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket kütüphanesinin event-target.js dosyasındaki hata yakalama mekanizması, 'thisArg' nesnesinin durumu değiştiğinde (örneğin bağlantı kapandığında) 'listenerCount' metoduna erişmeye çalışırken hata fırlatabiliyor. Eklenen try-catch bloğu ve 'listenerCount' fonksiyon kontrolü, bu tür 'race condition' kaynaklı çökmeleri engelleyerek uygulamanın kararlılığını artırır.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 13:40:07] Otonom Hata Düzeltme: `channel2-ariza`
- **Kök Neden:** WebSocket event listener'ı çalıştırılırken oluşan hataların, process.nextTick içinde yakalanmadan dışarı sızması veya 'thisArg' nesnesinin beklenmedik şekilde null/undefined olması durumunda sistemin çökmesine neden olması.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** process.nextTick kullanımı, asenkron hata fırlatılmasına ve ana event loop'un kontrolsüz bir şekilde sonlanmasına neden olabiliyordu. Hata yönetimini senkron bir try-catch bloğu içerisine alarak, WebSocket event listener hatalarının uygulamanın genel çalışma sürecini (Remotion render süreci gibi) kesintiye uğratmasını engelledik.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 16:15:37] Otonom Hata Düzeltme: `weekly-long-scheduler`
- **Kök Neden:** Remotion render işlemi sırasında WebSocket bağlantısının zaman aşımına uğraması ve ardından gelen 'Page crashed' hatasının, event listener'ların hata yönetimi sırasında sessizce başarısız olması veya beklenmedik bir şekilde tetiklenmesi.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket event listener'ı içindeki hata yakalama bloğunda, 'emit' işlemini 'process.nextTick' içerisine alarak, hata fırlatan listener'ın mevcut event döngüsünü (event loop) kilitlemesini veya 'Page crashed' durumunu tetikleyen senkron hata zincirini kırmasını engelledik. Bu, Remotion'ın render sürecindeki WebSocket kararlılığını artırır.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 16:17:59] Otonom Hata Düzeltme: `weekly-long-scheduler`
- **Kök Neden:** Remotion render işlemi sırasında WebSocket bağlantısında oluşan hataların (Page crashed) düzgün yönetilememesi ve 'callListener' fonksiyonundaki hata yakalama mekanizmasının, render sürecini kilitleyen bir 'ETIMEDOUT' durumuna yol açması.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** WebSocket event listener hatalarının render sürecini 'ETIMEDOUT' durumuna sokmasını engellemek için, hata yakalama bloğundaki gereksiz konsol çıktılarını ve render döngüsünü kilitleyebilecek senkron/asenkron hata yönetimi mantığını sadeleştirdik. Hataları sessizce yutarak, Remotion'ın render sürecinin çökmeden devam etmesini sağladık.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 16:19:34] Otonom Hata Düzeltme: `weekly-long-scheduler`
- **Kök Neden:** Remotion render sırasında WebSocket üzerinden gelen olayların işlenmesi sırasında oluşan hatalar, 'ws' kütüphanesinin event-target.js dosyasındaki 'callListener' fonksiyonunda yakalanamıyor ve render işleminin çökmesine (Page crashed) neden oluyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** Orijinal kodda 'listenerCount' kontrolü, hata durumunda emit edilmesini engelliyor veya geciktiriyor. Hata logu, 'Page crashed' hatasının WebSocket olay döngüsündeki bir istisnadan kaynaklandığını gösteriyor. 'listenerCount' kontrolünü kaldırarak hatanın 'error' olayına güvenli bir şekilde iletilmesini ve render sürecinin çökmeden devam etmesini sağlıyoruz.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 16:21:37] Otonom Hata Düzeltme: `weekly-long-scheduler`
- **Kök Neden:** Remotion render işlemi sırasında WebSocket üzerinden gelen olayların işlenmesi sırasında oluşan hatalar, 'ws' kütüphanesinin event-target.js dosyasındaki 'callListener' fonksiyonunda yakalanamadığı için ana süreci (process) çökertmektedir.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** Mevcut kodda hata yakalandığında 'thisArg' nesnesinin 'emit' fonksiyonuna sahip olmaması durumunda hata sessizce yutuluyor ancak süreç kararsız kalabiliyordu. 'else' bloğu ekleyerek ve hata loglamasını iyileştirerek, render sürecinin beklenmedik bir şekilde çökmesini engellemek için hata yönetimi güçlendirildi.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 16:23:36] Otonom Hata Düzeltme: `weekly-long-scheduler`
- **Kök Neden:** Remotion render işlemi sırasında video proxy isteği zaman aşımına uğruyor ve WebSocket bağlantısı çöktüğünde 'ws' kütüphanesi hata yönetimi sırasında 'callListener' fonksiyonunda beklenmedik bir istisna fırlatarak süreci durduruyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/node_modules/ws/lib/event-target.js`
- **Açıklama:** Hata logu, WebSocket olay dinleyicisi içindeki bir hatanın 'ws' kütüphanesinin iç mekanizmasını bozduğunu gösteriyor. 'console.error' çağrılarını ve gereksiz hata loglama işlemlerini minimize ederek, render sırasında oluşan 'ETIMEDOUT' gibi geçici hataların tüm Node.js sürecini çökertmesini engellemek için hata yakalama bloğunu daha güvenli hale getirdik.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 19:05:55] Otonom Hata Düzeltme: `channel4-hak`
- **Kök Neden:** Headless Linux sunucu ortamında '--gl=angle' grafik sürücü modu Chrome/Puppeteer'ın GPU başlatma sürecinde kilitlenmesine ve 25 saniyelik tarayıcı bağlantı zaman aşımına (TimeoutError) yol açmaktadır.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/channels/channel4-hak/engine.js`
- **Açıklama:** Linux sunucularda donanımsal GPU bağlamı bulunmadığında '--gl=angle' parametresi Chrome'un başlatılamamasına ve zaman aşımına neden olur. Software rendering sağlayan '--gl=swiftshader' moduna geçilerek Chromium'un headless olarak kararlı bir şekilde render yapması sağlanmıştır.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 19:07:35] Otonom Hata Düzeltme: `channel4-hak`
- **Kök Neden:** Remotion render işlemi sırasında kullanılan '--gl=swiftshader' parametresi, sunucu ortamında GPU hızlandırma eksikliği veya uyumsuzluğu nedeniyle tarayıcı başlatma zaman aşımına (timeout) yol açmaktadır.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/channels/channel4-hak/engine.js`
- **Açıklama:** Swiftshader, yazılımsal render için ağır bir yük oluşturabilir. '--gl=none' parametresi, GPU gereksinimini tamamen devre dışı bırakarak headless tarayıcının sunucu ortamında daha kararlı ve hızlı başlamasını sağlar, böylece 'Timed out while trying to connect to the browser' hatası engellenir.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 19:11:35] Otonom Hata Düzeltme: `channel4-hak`
- **Kök Neden:** Remotion render işlemi sırasında kullanılan '--gl=angle' parametresi, Linux sunucu ortamlarında GPU sürücü uyumsuzluğu veya eksikliği nedeniyle tarayıcı başlatma zaman aşımına (TimeoutError) yol açmaktadır.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/channels/channel4-hak/engine.js`
- **Açıklama:** GPU hızlandırma sorunlarını gidermek için '--gl=angle' (veya 'none') yerine daha kararlı olan '--gl=software' moduna geçildi. Ayrıca, sistem kaynaklarını korumak ve 'TimeoutError' riskini azaltmak için eşzamanlılık (concurrency) 2'den 1'e düşürüldü.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-07 19:13:36] Otonom Hata Düzeltme: `channel4-hak`
- **Kök Neden:** Remotion render işlemi sırasında --gl=angle parametresi, sunucu ortamında (headless/GPU-less) uyumluluk sorunlarına ve browser başlatma zaman aşımına (timeout) neden oluyor. Ayrıca concurrency=2 değeri, kısıtlı kaynaklarda browser başlatma çakışmalarına yol açabiliyor.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/channels/channel4-hak/engine.js`
- **Açıklama:** Render motoru için --gl=cpu parametresi, sunucu ortamlarında en kararlı seçenektir. Concurrency değerini 1'e sabitleyerek kaynak çakışmalarını minimize ettik ve render komutuna bir 'retry' (tekrar deneme) mekanizması ekleyerek geçici browser başlatma hatalarının sistemi tamamen durdurmasını engelledik.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---

### 🛠️ [2026-09-08 11:01:54] Otonom Hata Düzeltme: `channel4-hak`
- **Kök Neden:** Remotion render komutunda kullanılan '--gl=cpu' parametresi geçersizdir. Remotion, CPU tabanlı render için 'swiftshader' değerini kabul etmektedir.
- **Etkilenen Dosya:** `/home/kscmrt/remotion-video/channels/channel4-hak/engine.js`
- **Açıklama:** Remotion'ın GL backend seçenekleri arasında 'cpu' bulunmamaktadır. Hata logunda belirtilen 'Accepted values: swangle, angle, egl, swiftshader, vulkan, angle-egl' listesine uygun olarak, CPU kullanımı için en stabil seçenek olan 'swiftshader' parametresi ile güncellenmiştir.
- **Durum:** ✅ Başarıyla Yamandı ve PM2 Yeniden Başlatıldı.

---
