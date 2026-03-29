# NOVA-X
Raspberry Pi ve Arduino tabanlı otonom uzay çöpü tespit ve imha sistemi prototipi.
Otonom Yörünge Temizlik Sistemi (Autonomous Space Debris Remover)

Bu proje, Dünya yörüngesindeki kontrolsüz uzay çöplerini otonom olarak tespit eden, sınıflandıran ve yörünge dışına iterek temizleyen bir Unity tabanlı mühendislik simülasyonudur. Proje, deterministik algoritmalar ve vektörel hesaplamalar üzerine kurulu bir otonom operasyon döngüsü sunar.
 Temel Özellikler ve Çalışma Mantığı

Sistem, üç ana aşamadan oluşan bir otonom görev döngüsünü takip eder:
1. Nesne Tarama ve Tanımlama

Araç, algilamaMesafesi içindeki tüm nesneleri sürekli olarak tarar. Nesneler, Unity'nin Tag sistemi kullanılarak iki sınıfa ayrılır:

    Aktif Uydu: Zararsız, operasyonel uydular.

    Çöp (Cop): İmha edilmesi gereken kontrolsüz nesneler.

2. Otonom Operasyon ve Lazer Müdahalesi

Bir çöp tespit edildiğinde araç, hedefle arasındaki açıyı (Quaternion.Slerp) ve mesafeyi otonom olarak ayarlar.

    Haberleşme: Operasyon onayı için Dünya ve Uydu Merkezi arasında görsel bir veri transferi (sinyalizasyon) simüle edilir.

    İmha Süreci: Lazer (LineRenderer) ile hedefe kilitlenir ve nesne Dünya merkezine doğru bir itme kuvvetine maruz bırakılarak atmosfere itilir.

3. Görsel Geri Bildirim

Operasyonun durumunu takip etmek için nesneler dinamik olarak renk değiştirir:

    🟡 Sarı: Tarama/Analiz süreci.

    🟢 Yeşil: Güvenli nesne (Aktif Uydu).

    🔴 Kırmızı: İmha süreci (Uzay Çöpü).

 Proje Bileşenleri (Scriptler)
OtonomGorev.cs (Sistemin Beyni)

Aracın tüm hareket, tarama, boyama ve imha mantığını yöneten ana scripttir. Nesneleri analiz eder ve lazer operasyonunu yürütür.
YorungeDizici.cs (Kurulum Modülü)

Sahne başladığında nesneleri (uydular ve çöpler) matematiksel bir hassasiyetle yörünge düzlemine yerleştirir. Simülasyonun statik temelini oluşturur.
UzayTrafigi.cs (Dinamik Akış - Zorunlu Değil)

Bu modül, araç ilerledikçe önünde yeni nesneler üretir (Procedural Generation).

    Not: Bu script projenin çalışması için zorunlu değildir. Sadece sonsuz bir döngü ve daha yoğun bir trafik simülasyonu istenirse aktif edilir. Devre dışı bırakıldığında sistem sadece YorungeDizici tarafından yerleştirilen nesnelerle otonom görevini sürdürür.
