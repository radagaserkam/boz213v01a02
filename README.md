# boz213v01a02

# Kablosuz Sensör Ağlarında Bağlantı Kesintisi Sırasında Saat Sapmasının Yazılımsal Tahmini ve Telafisi

## 1. Araştırmanın Bilimsel Niteliği

### 1.1. Konunun Önemi ve Araştırma Önerisinin Bilimsel Niteliği

Kablosuz mikrodenetleyici ağlarında zaman eşzamanlılığı, verilerin doğru zaman damgalarıyla kaydedilmesi ve cihazlar arasında koordineli işlemlerin gerçekleştirilmesi açısından önemlidir. Mikrodenetleyicilerin yerel saatleri, osilatörlerin frekans farklılıkları nedeniyle zamanla birbirinden sapmaktadır. Normal koşullarda bu sapmalar, ağ üzerinden gerçekleştirilen zaman eşzamanlama işlemleriyle düzeltilebilirken bağlantının kesilmesi durumunda cihazlar güncel zaman referansına erişememekte ve zamanlama hataları birikmektedir.

Literatürde bu probleme yönelik çeşitli yazılımsal yöntemler geliştirilmiştir. *Adaptive Compensation for Time-Slotted Synchronization in Wireless Sensor Network* (2014) çalışmasında uyarlanabilir saat sapması telafisi [1], *Adaptive Time Window Linear Regression Algorithm for Accurate Time Synchronization in Wireless Sensor Networks* (2015) çalışmasında ise regresyon tabanlı tahmin yöntemleri incelenmiştir [2]. Daha güncel çalışmalardan *Time Synchronization on ESP-NOW Based Wireless Sensor Network Using Flooding Time Synchronization Protocol* (2023), ESP-NOW üzerinden aktif zaman eşzamanlamasını ele almaktadır [4]. *Energy-efficient Clock-Synchronization in IoT Using Reinforcement Learning* (2024) çalışmasında ise öğrenme tabanlı eşzamanlama yöntemleri araştırılmıştır [5].

Bu araştırmanın odağı, aktif eşzamanlamadan farklı olarak bağlantının tamamen kesilmesi durumunda yerel saat hatasının yazılımsal olarak tahmin edilmesidir. Projenin özgün değeri, telafisiz çalışma, sabit saat sapması düzeltmesi ve regresyon tabanlı tahmin yöntemlerinin aynı ESP32 donanımı üzerinde, karşılaştırılabilir deney koşullarında değerlendirilmesidir. Böylece yöntemlerin farklı bağlantı kesintisi sürelerindeki başarısı ve ölçüm geçmişinin tahmin doğruluğuna etkisi incelenecektir.

#### Araştırmanın Temel Sorusu

Kablosuz mikrodenetleyici ağlarında zaman referansıyla bağlantı kesildiğinde, geçmiş ölçümlere dayalı yazılımsal tahmin yöntemleri zamanlama hatasını ne ölçüde azaltabilir ve belirlenen hata sınırları içerisinde ne kadar süre çalışabilir?

#### Araştırmanın Hipotezleri

- **H1:** Kısa bağlantı kesintilerinde sabit saat sapması düzeltmesi ile regresyon tabanlı yöntemler arasındaki performans farkı sınırlı olacaktır.

- **H2:** Bağlantı kesintisi süresi arttıkça telafisiz çalışmada biriken zamanlama hatası, yazılımsal tahmin yöntemlerine kıyasla daha yüksek olacaktır.

- **H3:** Ölçüm geçmişinin uzatılması her durumda tahmin doğruluğunu artırmayacak; saat sapmasının değişkenlik gösterdiği koşullarda yakın geçmişteki ölçümlere ağırlık veren yöntemler daha başarılı olabilecektir.

#### Araştırmanın Kapsamı ve Sınırlılıkları

Araştırma, düşük maliyetli ESP32 mikrodenetleyicileri ve yazılımsal saat sapması tahmin yöntemleriyle sınırlandırılmıştır. Yeni bir donanım veya haberleşme protokolü geliştirilmeyecektir. Sıcaklık bağımsız bir deney değişkeni olarak ele alınmayacak ve sıcaklık telafisi uygulanmayacaktır. Deneyler mümkün olduğunca benzer çevresel koşullarda gerçekleştirilecektir.

Proje, On İkinci Kalkınma Planı (2024–2028) ve 2030 Sanayi ve Teknoloji Stratejisi'nin dijital dönüşüm, nesnelerin interneti ve haberleşme teknolojileri hedefleriyle ilişkilidir. Araştırma sonuçlarının, bağlantı kesintilerinde zamanlama güvenilirliğini artırmaya yönelik yazılımsal yöntemlerin seçimine katkı sağlaması beklenmektedir.

### 1.2. Amaç ve Hedefler

Bu projenin amacı, kablosuz mikrodenetleyici ağlarında zaman referansıyla bağlantının kesilmesi durumunda, geçmiş ölçümlere dayalı yazılımsal saat sapması tahmin yöntemlerinin başarısını deneysel olarak karşılaştırmaktır. Farklı algoritmaların zamanlama hatasını ne ölçüde azaltabildiği ve kabul edilebilir doğruluğu ne kadar süre koruyabildiği araştırılacaktır.

#### Projenin Somut Hedefleri

1. **Deney düzeneğinin kurulması:** En az üç ESP32 mikrodenetleyici kullanılarak ESP-NOW üzerinden zaman eşzamanlamasının gerçekleştirilebildiği, bağlantının kontrollü olarak kesilebildiği ve saat farklarının kaydedilebildiği bir deney ortamı oluşturulması.

2. **Tahmin algoritmalarının geliştirilmesi:** Bağlantı öncesinde toplanan saat farkı ölçümlerinden yararlanılarak sabit saat sapması düzeltmesi, doğrusal regresyon ve kayan pencere regresyonu yöntemlerinin uygulanması. Telafisiz çalışma, karşılaştırma için temel yöntem olarak kullanılacaktır.

3. **Deneysel karşılaştırmaların gerçekleştirilmesi:** Algoritmaların kısa, orta ve uzun süreli bağlantı kesintilerindeki davranışlarının incelenmesi. Ayrıca tahminde kullanılan geçmiş ölçüm penceresinin uzunluğu değiştirilerek bunun tahmin doğruluğuna etkisinin araştırılması.

4. **Performansın değerlendirilmesi:** Algoritmaların zamanlama hatalarının bağımsız doğrulama ölçümleriyle belirlenmesi; ortalama mutlak hata (MAE), kök ortalama kare hata (RMSE), maksimum mutlak hata ve belirlenen hata eşiklerinin aşılmasına kadar geçen süre bakımından karşılaştırılması. Elde edilen sonuçların grafikler ve tablolarla raporlanması.

Proje sonucunda, farklı yazılımsal saat sapması tahmin yöntemlerinin bağlantı kesintisi koşullarındaki başarılarını gösteren deneysel verilerin elde edilmesi ve yöntemlerin kullanım sınırlarının belirlenmesi hedeflenmektedir.

---

## 2. Yöntem

Araştırmada kontrollü deneysel yöntem kullanılacaktır. ESP32 mikrodenetleyicilerinden oluşan bir ağda bağlantı kesintileri oluşturularak farklı yazılımsal saat sapması tahmin yöntemleri karşılaştırılacaktır.

**Bağımsız değişkenler:**

- Bağlantı kesintisi süresi
- Bağlantı öncesi ölçüm geçmişinin uzunluğu
- Kullanılan tahmin yöntemi

**Bağımlı değişkenler:**

- Zamanlama hatası
- Belirlenen hata sınırlarının aşılmasına kadar geçen süre

### 2.1. Deney Düzeneğinin Oluşturulması

Araştırmada aynı modelden en az üç ESP32 mikrodenetleyici kullanılacaktır. Düğümler arasında ESP-NOW protokolü üzerinden zaman eşzamanlama mesajlarının iletilebildiği ve bağlantının kontrollü olarak kesilebildiği bir ağ oluşturulacaktır.

Bağlantı kesintisi sırasında oluşan gerçek zamanlama hatalarını belirlemek amacıyla, mikrodenetleyicilerin belirli zamanlarda ürettiği sayısal çıkış darbeleri ortak zaman tabanına sahip harici bir ölçüm cihazıyla kaydedilecektir. Bu cihaz yalnızca ölçüm amacıyla kullanılacak, mikrodenetleyicilere herhangi bir zaman referansı sağlamayacaktır.

### 2.2. Bağlantı Öncesi Veri Toplama

Bağlantı mevcutken düğümler arasındaki saat farkları belirli aralıklarla ölçülecek ve saat sapmasının zamana bağlı değişimi kaydedilecektir.

Tahmin başarısına etkisini değerlendirmek amacıyla aşağıdaki ölçüm geçmişleri kullanılacaktır:

- 5 dakika
- 15 dakika
- 30 dakika

Toplanan veriler, bağlantı kesintisi sırasında kullanılacak tahmin modellerinin oluşturulmasında değerlendirilecektir.

### 2.3. Bağlantı Kesintisi Senaryoları

Veri toplama aşamasının ardından düğümler arasındaki kablosuz zaman eşzamanlaması kontrollü biçimde durdurulacaktır. Kesinti boyunca düğümler yeni zaman referansı almayacak ve tahmin yöntemleri yalnızca bağlantı öncesinde elde edilen verilere dayanacaktır.

| Senaryo | Bağlantı Kesintisi Süresi |
| --- | --- |
| Kısa süreli kesinti | 5 dakika |
| Orta süreli kesinti | 30 dakika |
| Uzun süreli kesinti | 120 dakika |

Böylece yöntemlerin kısa, orta ve uzun süreli kesintilerdeki performansları değerlendirilecektir. Deneyler mümkün olduğunca benzer çevresel koşullarda yürütülecektir.

### 2.4. Yazılımsal Tahmin Yöntemleri

Araştırmada dört yöntem karşılaştırılacaktır:

#### 2.4.1. Telafisiz Çalışma (Baseline)

Saat sapmasına yönelik herhangi bir düzeltme uygulanmayan temel karşılaştırma durumu.

#### 2.4.2. Sabit Saat Sapması Düzeltmesi (Constant Clock Drift Compensation)

Bağlantı öncesi ölçümlerden hesaplanan ortalama saat sapması hızının kesinti boyunca sabit kabul edilmesi.

#### 2.4.3. Doğrusal Regresyon (Linear Regression)

Bağlantı öncesindeki saat farkı ölçümlerinin tamamına doğrusal model uygulanarak gelecekteki saat hatasının tahmin edilmesi.

#### 2.4.4. Kayan Pencere Regresyonu (Sliding Window Regression)

Yalnızca bağlantı öncesindeki belirli sayıda son ölçüm kullanılarak doğrusal tahmin modeli oluşturulması.

Yöntemlerin karşılaştırılmasında aynı deneylerden elde edilen veriler kullanılacaktır. Bağlantı kesintisi sırasında bağımsız ölçüm cihazından elde edilen bilgiler tahmin algoritmalarına aktarılmayacak, yalnızca sonuçların doğrulanmasında kullanılacaktır.

### 2.5. Performans Değerlendirmesi

Yöntemlerin doğruluğu, bağımsız ölçüm sonuçlarıyla karşılaştırılarak değerlendirilecektir. Bu amaçla aşağıdaki ölçütler kullanılacaktır:

| Performans Ölçütü | İngilizce Karşılığı |
| --- | --- |
| Ortalama mutlak hata | Mean Absolute Error (MAE) |
| Kök ortalama kare hata | Root Mean Square Error (RMSE) |
| Maksimum mutlak hata | Maximum Absolute Error |
| Hata sınırının aşılmasına kadar geçen süre | Time to Threshold |

Ölçüm sisteminin hassasiyetine bağlı olarak aşağıdaki zamanlama hatası sınırları kullanılacaktır:

- 1 ms
- 10 ms
- 100 ms

Temel deneyler her senaryo için en az üç kez tekrarlanacak ve sonuçların karşılaştırılmasında uygun istatistiksel yöntemlerden yararlanılacaktır.

Elde edilen veriler grafikler ve tablolar aracılığıyla analiz edilerek bağlantı kesintisi süresinin, ölçüm geçmişinin ve kullanılan tahmin yönteminin zamanlama doğruluğu üzerindeki etkileri ortaya konulacaktır.

---

## Ekler

### Ek 1. Araştırmanın Temel Literatür Kaynakları

**[1]** *Adaptive Compensation for Time-Slotted Synchronization in Wireless Sensor Network*. (2014).

https://doi.org/10.1155/2014/540397

**[2]** *Adaptive Time Window Linear Regression Algorithm for Accurate Time Synchronization in Wireless Sensor Networks*. (2015).

https://www.sciencedirect.com/science/article/abs/pii/S1570870514001735

**[3]** *Temperature-Compensated Clock Skew Adjustment*. (2013).

https://pmc.ncbi.nlm.nih.gov/articles/PMC3812638/

**[4]** *Time Synchronization on ESP-NOW Based Wireless Sensor Network Using Flooding Time Synchronization Protocol*. (2023).

https://doi.org/10.1145/3626641.3626683

**[5]** *Energy-efficient Clock-Synchronization in IoT Using Reinforcement Learning*. (2024).

https://deltazita.github.io/files/dcoss2024.pdf

**[6]** *Benchmarking OpenWiFiSync on ESP32: Towards Cost-Effective Wireless Time Synchronization*. (2025).

https://arxiv.org/abs/2511.14457

**[7]** *Wireless Clock Synchronization: A Comprehensive Survey and Taxonomy*. (2026).

https://ieeexplore.ieee.org/abstract/document/11593973
- <a id="ref-5"></a> [5] Energy-efficient Clock-Synchronization in IoT Using Reinforcement Learning. (2024). Makale / PDF
- <a id="ref-6"></a> [6] Benchmarking OpenWiFiSync on ESP32: Towards Cost-Effective Wireless Time Synchronization. (2025). Makale / arXiv
- <a id="ref-7"></a> [7] Wireless Clock Synchronization: A Comprehensive Survey and Taxonomy. (2026). Makale / IEEE Xplore
