
# Power Devresi Nedir ?

Power Devresi, bir elektronik  kart üzerindeki bileşenlere gerekli olan elektriksel gücü (gerilimi ve akımı) sağlayan devre bölümüdür. Bu devre, kartın kalbidir; çünkü diğer tüm bileşenler (mikrodenetleyici, sensörler, modüller vs.) düzgün çalışmak için kararlı bir güç kaynağına ihtiyaç duyar.Bütün bileşenlere gerektiği ölçüde güç verilmesi sistemin tasarımının ana unsurudur.


## Power Devresinin Temel Görevleri:

- Girişten alınan elektriği kart üzerindeki parçalara dağıtmak.


- Gelen gerilimi istenilen seviyeye düşürmek ya da yükseltmek yani regüle etmek.


- Aşırı akım, kısa devre ya da ters polarite gibi durumlara karşı kartı korumak.

- Güç kaynağındaki parazitleri ve gerilim dalgalanmalarını filtrelemek.

---

## Regülasyon

### Voltaj Regülasyonu

Voltaj regülasyonu, bir elektrik devresinde veya sisteminde çıkış voltajını belirli bir seviyede sabit tutmak için kullanılan yöntemlerdir. Voltaj regülasyonu, yük değişimleri veya giriş voltajındaki dalgalanmalara rağmen kararlı bir çıkış sağlamak amacıyla uygulanır.
Projemizin güç kaynağı 12V sağlayan bir aküdür . MCU ve diğer bileşenleri 12V ile beslemek mümkün olamayacağı için istenen seviyelere(3.3V - 5V) voltajı getirmek gerekir. 

Temel voltaj regüle yöntemleri:


**Anahtarlı Regülatör Kullanımı**

Anahtarlamalı regülatörler, temel olarak bir regülatör entegresi ile onun etrafında yer alan destekleyici pasif bileşenlerden oluşur. Bu entegreler hazır olarak temin edilir ve çalışabilmesi için üretici firmanın sunduğu datasheet belgelerinde yer alan tipik uygulama devrelerine göre çevresel elemanlar ile desteklenir. Devre tasarımında genellikle bobin (endüktör), kondansatör (kapasitör) ve diyot gibi elemanlara ihtiyaç duyulur. Entegrenin çalışma prensibine ve çıkış gereksinimlerine bağlı olarak bu bileşenlerin değeri belirlenir ve devreye entegre edilir.

- Buck Konvertör (Step-Down Regülatör): Giriş voltajını daha düşük sabit bir voltaja indirir.

    Örnek: 12V → 5V 

- Boost Konvertör (Step-Up Regülatör): Giriş voltajını yükseltir.

   Örnek: 3.7V Li-ion pil → 5V USB çıkışı    

- Buck-Boost Konvertör: Hem artırma hem azaltma yapabilir.Giriş voltajı, çıkış voltajının altına da üstüne de çıkabilir.



**Lineer Voltaj Regülatörleri**

Lineer voltaj regülatörleri, giriş voltajını sürekli izleyip gereksiz kısmını ısı olarak yayarak sabit bir çıkış voltajı sağlar. Bu regülatörler basit ve ucuz olmasına rağmen, düşük verimliliğe sahiptirler çünkü fazladan enerji ısıya dönüştürülerek kaybedilir.

**PWM (Pulse Width Modulation) ile Regülasyon**

Darbe genişlik modülasyonu kullanılarak ortalama çıkış voltajı kontrol edilir (DC motor kontrolü, LED sürücüler gibi uygulamalarda kullanılır).

**Zener Diyot Regülatörü**

Zener Diyot, değişen yük akımı koşullarında düşük dalgalanma ile stabilize bir voltaj çıkışı üretmek için kullanılabilir. Uygun bir akım sınırlama direnci kullanarak devre sağlıklı bir şekilde tamamlanabilir.

---

 ## GÜVENLİK



 ### Kısa Devre Koruma Devresi

 Kısa devre koruma devresi, güç kaynağı ile yük arasındaki bağlantıda çok düşük dirençli bir yol (yani kısa devre) oluştuğunda ani ve yüksek akım akışını tespit edip sistemi korumaya alan bir güvenlik devresidir.

 Uygulanan Koruma Yöntemleri
 
**Sigorta**

En temel kısa devre korumasıdır.

Kısa devre anında akım çok yükselir, sigorta erir ve devreyi açar.

Dezavantajı ise tek kullanımlık olmasıdır.

**Shunt Direnci + Komparatör / Op-Amp**

Küçük bir direnç üzerinden geçen akım ölçülür.

Ani yüksek akım tespit edilince, bir komparatör yardımıyla MOSFET veya anahtar kesilir.

Bu sistemle kısa devre durumu çok hızlı algılanabilir.

---

###  Aşırı Akım Koruma Devresi 


Aşırı akım koruma devresi, bir devreden geçen akım belirlenen sınırın üzerine çıktığında, devreyi ve bağlı bileşenleri zarar görmekten koruyan bir güvenlik sistemidir.

Aşırı akım; kısa devre, yükteki arıza, fazla yüklenme veya bileşen arızaları nedeniyle oluşabilir. Bu koruma devreleri, sigorta gibi pasif ya da entegre tabanlı aktif çözümler şeklinde olabilir.

**PTC (Pozitif Sıcaklık Katsayılı Termistör)**

Akım yükseldiğinde ısınır ve direnci artar, böylece akımı sınırlar.

Kendini sıfırlayan sigorta gibi çalışır.

Yeniden kullanılabilir, küçük devrelerde kullanışlıdır.


**Shunt Direnç + Komparatör / Op-Amp**

Devreden geçen akımı algılamak için düşük değerli bir direnç (shunt) kullanılır.

Akım, direnç üzerinde voltaj düşümüne sebep olur.

Bu voltaj, bir komparatör veya op-amp ile ölçülür.

Akım limiti aşıldığında MOSFET, röle veya başka bir anahtar devreyi keser.  


---

### Aşırı Gerilim Koruma Devresi

Aşırı gerilim koruma devreleri, elektronik sistemlerin belirlenen voltaj eşiklerinin üzerindeki gerilimlere maruz kalmasını önlemek amacıyla tasarlanır. Bu tür devreler, hassas bileşenlerin zarar görmesini engellemek için kritik öneme sahiptir.

**Zener Diyot ile Koruma**

Zener diyotun katodu, komparatörün pozitif (non-inverting) girişine bağlanırken, anodu giriş gerilimine bağlanır. Bu sayede, Zener diyot üzerinde sabit bir referans gerilimi oluşturulur.

Komparatörün negatif (inverting) girişi, korunması gereken devrenin giriş gerilimine bağlanır.

Komparatör çıkışı, MOSFET'in gate terminaline veya röle bobinine bağlanır. MOSFET kullanımında, source terminali toprağa, drain terminali ise yükün toprak hattına seri olarak bağlanarak yükün devre dışı bırakılması sağlanır. Röle kullanımında ise, röle kontakları yük devresini keserek koruma sağlar.

Giriş gerilimi, Zener diyotun belirlenen eşik değerini aştığında, komparatör çıkışı anahtarlama elemanını tetikler. MOSFET veya röle aktif hale gelerek yükün enerjisini keser ve sistemin aşırı gerilimden korunmasını sağlar.

