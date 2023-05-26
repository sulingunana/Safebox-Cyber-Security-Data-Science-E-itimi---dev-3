# Safebox-Cyber-Security-Data-Science-E-itimi---dev-3
Safebox Cyber Security Data Science Eğitimi - Ödev 3

ANALİTİK SQL NEDİR?
Analitik SQL, verilerin analiz edilmesi ve raporlanması için kullanılan SQL sorgularıdır. Analitik SQL, veritabanı içerisindeki verileri sorgulayarak, özetleyerek ve ilişkilendirerek anlamlı bilgiler elde etmeyi sağlar. Bu sayede işletmeler, veri analitiği yaparak trendleri, desenleri ve ilişkileri keşfedebilir, kararlarını destekleyebilir ve stratejik yönelimlerini belirleyebilirler.
Analitik SQL'in normal SQL'den farkları:
1.	Veri İşleme Yaklaşımı: Normal SQL, genellikle veritabanında yapısal değişiklikler yapmak, veri ekleme, güncelleme ve silme gibi işlemleri gerçekleştirmek için kullanılır. Analitik SQL ise verileri sorgulayarak analiz etmek ve raporlamak için kullanılır. Analitik SQL sorguları, veritabanı içindeki verileri özetleyebilir, filtreleyebilir, gruplayabilir ve analiz edebilir.
2.	Veri Analitiği Odaklı Fonksiyonlar: Analitik SQL, veri analitiği ve raporlama için özel olarak tasarlanmış fonksiyonlara sahiptir. Bu fonksiyonlar, verilerin toplamını, ortalama değerini, standart sapmasını, en büyük/en küçük değerleri gibi istatistiksel hesaplamaları yapmak için kullanılabilir. Normal SQL'de ise bu tür analitik fonksiyonlar genellikle bulunmaz veya sınırlıdır.
3.	İş Zekası Raporlaması: Analitik SQL, iş zekası raporlarının oluşturulmasında yaygın olarak kullanılır. İş zekası, işletmelerin verilerini analiz ederek stratejik kararlar almasına yardımcı olan bir süreçtir. Analitik SQL sorguları, işletmelerin performans metriklerini izlemelerini, trendleri analiz etmelerini, pazar analizi yapmalarını sağlar.
4.	Veri Madenciliği ve Keşifsel Analiz: Analitik SQL, veri madenciliği ve keşifsel analiz için kullanılır. Bu tür analizlerde, veritabanındaki veriler üzerinde desenleri, ilişkileri ve segmentleri keşfetmek amaçlanır. Normal SQL ise genellikle veritabanı yönetimi ve veri işleme amaçlarına odaklanır.
5.	İş Performansı ve Optimizasyon: Analitik SQL, veritabanı sorgularının performansını değerlendirmek ve iyileştirme fırsatlarını belirlemek için kullanılır. Analitik SQL sorguları, büyük veri kümeleri üzerinde kompleks sorguları çalıştırmak ve sonuçları hızlı bir şekilde elde etmek için optimize edilebilir.
Sonuç olarak, analitik SQL, veri analitiği ve raporlama için tasarlanmış bir SQL alt kümesidir. Normal SQL, genel veritabanı yönetimi ve veri işleme işlemleri için kullanılırken, analitik SQL verilerin analiz edilmesi ve anlamlı bilgiler elde edilmesi için özelleştirilmiştir.
Analitik SQL, birçok alanda kullanılmaktadır. İşte analitik SQL'in kullanıldığı bazı alanlar ve örnekler:

1.	İş Zekâsı ve Raporlama: Analitik SQL, işletmelerin verilerini analiz etmelerine ve iş zekası raporları oluşturmalarına yardımcı olur. Bu raporlar, işletmelere performanslarını izleme, trendleri anlama, pazar analizi yapma gibi konularda önemli bilgiler sunar.
Örnek:
SELECT ProductCategory, SUM(SalesAmount) AS TotalSales 
FROM Sales 
GROUP BY ProductCategory 
ORDER BY TotalSales DESC; 
Bu SQL sorgusu, "Sales" tablosundaki ürün kategorilerine göre toplam satış miktarını hesaplar ve en yüksek satışa sahip kategoriyi ilk sırada listeler.



2.	Veri Madenciliği ve Keşifsel Analiz: Analitik SQL, veri madenciliği ve keşifsel analiz için kullanılır. Bu sayede veritabanındaki veriler üzerinde desenleri, ilişkileri ve segmentleri keşfedebiliriz.
Örnek:
SELECT AgeGroup, COUNT(*) AS CustomerCount 
FROM Customers 
GROUP BY AgeGroup 
HAVING CustomerCount > 100; 
Bu SQL sorgusu, "Customers" tablosundaki müşterileri yaş gruplarına göre gruplar ve 100'den fazla müşterisi olan yaş gruplarını filtreler.



3.	İş Performansı ve Optimizasyon: Analitik SQL, işletmelerin iş performansını ölçmelerine ve optimizasyon fırsatlarını belirlemelerine yardımcı olur. Veri tabanı sorgularının performansını değerlendirerek, iyileştirme gerektiren alanları belirleyebiliriz.

Örnek:
EXPLAIN SELECT * FROM Orders WHERE OrderDate >= '2022-01-01'; 
Bu SQL sorgusu, "Orders" tablosundaki '2022-01-01' tarihinden sonra yapılan siparişleri seçerken, sorgunun performansını analiz eder ve optimize edilmesi gereken alanları gösterir.
--------------------------------------------------------------------------------------------------------------------------------------

WITH toplam_satis AS (
  SELECT
    EXTRACT(YEAR FROM tarih) AS yil,
    EXTRACT(MONTH FROM tarih) AS ay,
    SUM(satis_miktar) AS toplam_satis
  FROM
    satislar
  GROUP BY
    EXTRACT(YEAR FROM tarih),
    EXTRACT(MONTH FROM tarih)
), toplam_maliyet AS (
  SELECT
    EXTRACT(YEAR FROM tarih) AS yil,
    EXTRACT(MONTH FROM tarih) AS ay,
    SUM(maliyet) AS toplam_maliyet
  FROM
    maliyetler
  GROUP BY
    EXTRACT(YEAR FROM tarih),
    EXTRACT(MONTH FROM tarih)
)
SELECT
  t.yil,
  t.ay,
  t.toplam_satis,
  m.toplam_maliyet,
  t.toplam_satis - m.toplam_maliyet AS kar
FROM
  toplam_satis t
JOIN
  toplam_maliyet m ON t.yil = m.yil AND t.ay = m.ay
ORDER BY
  t.yil, t.ay;
Bu sorgu, "satislar" ve "maliyetler" adlı iki tablodan verileri kullanarak aylık satışları, maliyetleri ve karları hesaplamaktadır. İlk olarak, her bir tabloyu yıla ve aya göre gruplayan toplam satışları ve maliyetleri hesaplayan geçici tablolar (CTE'ler) oluşturulur. Ardından, bu geçici tabloları birleştirerek yıl, ay, toplam satışlar, toplam maliyetler ve karları içeren sonuç kümesini döndüren bir sorgu gerçekleştirilir. EXTRACT fonksiyonu ile tarih alanından yıl ve ay bilgileri alınır. Ayrıca, toplam_satis ve toplam_maliyet geçici tablolarını birleştirmek için JOIN ifadesi kullanılır. Sonuçlar, yıl ve ay sırasına göre sıralanır.

--------------------------------------------------------------------------------------------------------------------------------------

UPDATE customers SET status = 'VIP' WHERE total_orders > 10 AND total_revenue > 5000; 
Bu örnekte, "customers" adlı bir tablo varsayılmıştır. Tabloda müşterilere ilişkin bilgiler (müşteri kimliği, toplam sipariş sayısı, toplam gelir vb.) bulunmaktadır. Bu SQL sorgusu, belirli bir koşulu sağlayan müşterilerin durumunu günceller.
Sorgu, müşterilerin "total_orders" (toplam sipariş sayısı) değerinin 10'dan büyük ve "total_revenue" (toplam gelir) değerinin 5000'den büyük olduğu durumları seçer. Ardından, bu müşterilerin "status" (durum) alanını "VIP" olarak günceller.
Bu örnekteki veri işleme yaklaşımı, verilere dayalı bir koşulu sağlayan kayıtları güncellemek için kullanılır. Bu örnekte, belirli bir işlemi gerçekleştirmek için bir UPDATE ifadesi kullanılmıştır. Bu tür bir yaklaşımı, müşteri segmentasyonu, özel teklifler veya indirimler gibi senaryolarda kullanabilirsiniz.
--------------------------------------------------------------------------------------------------------------------------------------
SELECT departman,yil,
    SUM(satış) AS toplam_satis,
    AVG(satış) AS ortalama_satis,
    MAX(satış) AS max_satis,
    MIN(satış) AS min_satis
FROM satis_tablosu
GROUP BY departman, yil
ORDER BY departman,yil;
Bu örnekte “satis_tablosu” isimli tablodan departman ve yıla göre satış verilerini analiz eder. Yani her departman ve her yıl için toplam satış miktarı (“toplam_satis”) , ortalama satış miktarı (“ortalama_satis”) , en yüksek satış miktarı (“max_satis”) , en düşük satış miktarı (“min_satis”) görüntülenir ve gelen sonuçlar da departman ve yıla göre sıralanır sonuçlar öyle getirilir.




--------------------------------------------------------------------------------------------------------------------------------------
SELECT Movie.MID as “MID”,
Movie.title as “Film Adı”,
Movie.year as “Çekim Yılı”,
Location.Name as “Çekildiği Yer”
FROM Movie 
JOIN M_Location ON Movie.MID = M_Location.MID 
JOIN Location ON M_Location=LID=Location.LID
Bu örnekte “Movie”, “M_Location” ve “Location” adındaki üç tablodan, filmlerin bilgilerini ve çekildikleri yerleri birleştirerek çekim yerlerine göre film detaylarını getirmektir.



--------------------------------------------------------------------------------------------------------------------------------------
SELECT
    DATE_TRUNC('month', order_date) AS month,
    COUNT(DISTINCT customer_id) AS unique_customers,
    SUM(order_total) AS total_revenue,
    AVG(order_total) AS average_order_total
FROM
    orders
WHERE
    order_date >= '2022-01-01'
    AND order_date < '2023-01-01'
GROUP BY
    DATE_TRUNC('month', order_date)
ORDER BY
    month;
Bu SQL sorgusu, "orders" tablosundaki verileri işleyerek belirli bir tarih aralığındaki siparişlerin aylık bazda toplam gelirini, ortalama sipariş tutarını ve benzersiz müşteri sayısını hesaplar


--------------------------------------------------------------------------------------------------------------------------------------

Ada Virüsü Nedir ?
Ada virüsü, Ada programlama dilinde yazılmış olan bir virüstür. Ada virüsü, Ada programlarını enfekte ederek yayılan zararlı bir yazılımdır. Enfekte ettiği Ada programlarını kopyalayarak yayılır ve genellikle bu programların çalışmasını bozar veya verileri etkiler. Ada virüsü, dosya sistemi üzerinde bulaştığı programları arar ve bunları enfekte eder. Ada virüsleri genellikle kötü niyetli kişiler tarafından oluşturulur ve zararlı amaçlar için kullanılır. Bilgisayarlarda veri kaybına, sistem çökmesine veya hassas bilgilerin sızmasına neden olabilirler. Ada virüsleri, günümüzde daha az yaygın olan bir virüs türüdür. 

Ada Virüsü Nasıl Çalışır ?
İşleyişleri genel olarak şu adımları içerir:

1.	Enfeksiyon Yolu: Ada virüsleri, yayılmak için farklı yöntemler kullanabilir. Örneğin, bulaştığı Ada programlarının kaynak kodlarını değiştirerek veya Ada programlarının derlenmiş çalıştırılabilir dosyalarını enfekte ederek yayılabilir.
2.	Yayılma: Ada virüsleri, enfekte ettiği Ada programlarının kopyalarını oluşturarak yayılır. Bu kopyalar genellikle aynı bilgisayar üzerinde veya ağ üzerinde bulunan diğer dosyalara veya sistemlere bulaşabilir.
3.	Enfeksiyon Süreci: Ada virüsleri, enfekte ettikleri Ada programlarının içine zararlı kodlar ekleyerek veya mevcut kodları değiştirerek çalışır. Bu şekilde, virüsün zararlı etkileri gerçekleşir. Örneğin, veri kaybı, sistem çökmesi, yetkisiz erişim gibi zararlı eylemler yapabilir.
4.	Gizlenme: Ada virüsleri, enfeksiyonlarını gizlemek için bazı yöntemler kullanabilir. Örneğin, dosya boyutlarını değiştirerek veya kaynak kodlarını karıştırarak tespit edilmeyi zorlaştırabilir.
5.	Aktivasyon: Enfekte edilen Ada programları çalıştırıldığında veya belirli koşullar gerçekleştiğinde Ada virüsü aktive olur. Bu durumda, virüsün zararlı etkileri ortaya çıkar ve enfekte edilen programın normal işleyişini bozar.


Örnek: Wabbit Virüsü
"Wabbit" bilgisayar virüsü, 1970'lerin sonlarından itibaren ortaya çıkan ve 1980'lerin başında popüler hale gelen bir tür virüs olarak bilinir. Wabbit, genellikle kendini kopyalayan ve yayılan bir virüs değildir.
Wabbit, genellikle matematiksel bir döngü veya tekrarlı bir işlem içeren bir programdır. Örneğin, sonsuz döngüler veya kaynak tüketen hesaplamalar gibi işlemleri yürüterek bilgisayarın performansını düşürebilir veya hatta çökmesine neden olabilir. Wabbit virüsü, sistem kaynaklarını tüketme veya işlem gücünü boşa harcama gibi yollarla kullanıcıları rahatsız etmek veya zarar vermek amacıyla oluşturulmuştur.

Wabbit virüsü genellikle bilgisayara bir dosya yoluyla veya başka bir programın içinde dahil edilerek bulaşır. Kullanıcı, virüslü bir dosyayı açtığında veya çalıştırdığında Wabbit aktif hale gelir. Virüs, genellikle işletim sistemi ve donanım kaynaklarını aşırı yükleyen veya tüketen işlemleri yürüterek zararlı etkisini gerçekleştirir.


