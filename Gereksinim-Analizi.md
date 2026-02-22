# Gereksinim Analizi
# Tüm Gereksinimler 

1. **Üye Olma**
   - **API Metodu:** `POST /api/auth/register`
   - **Açıklama:** Kullanıcıların yeni hesaplar oluşturarak sisteme kayıt olmasını sağlar. Güvenlik gereği yalnızca `.edu` uzantılı e-posta adresleri kabul edilir. Kullanıcılar email adresi ve şifre belirleyerek hesap verilerini oluşturur.

2. **Hesap Doğrulama**
   - **API Metodu:** `POST /api/auth/verify`
   - **Açıklama:** Kayıt olan kullanıcıların hesaplarını aktif hale getirmesini sağlar. Admin onayına sunulur ve onaylanırsa hesaba giriş yetkisi verilir.(İlerleyen zamanlarda mail ile doğrulama özellikleri için gerekli kodlar eklenecek şimdilik manuel doğrulama sağlanmaktadır.)

3. **Giriş Yapma**
   - **API Metodu:** `POST /api/auth/login`
   - **Açıklama:** Kullanıcıların sisteme giriş yaparak hizmetlere erişmesini sağlar. Doğrulanmış ve onaylanmış email adresi ile şifre eşleştirilerek kimlik doğrulama yapılır. Başarılı giriş sonrası kullanıcıya güvenli erişim tokenı (JWT) verilir.

4. **Kendi Profilini Görüntüleme**
   - **API Metodu:** `GET /api/auth/user`
   - **Açıklama:** Sisteme giriş yapmış kullanıcının kendi profil bilgilerini görüntülemesini sağlar. Kişisel tanımlayıcılar, hesap kredisi ve o an sepetinde bulunan ürünlerin detayları listelenir.

5. **Profil Bilgilerini Güncelleme**
   - **API Metodu:** `PUT /api/auth/profile`
   - **Açıklama:** Kullanıcının kendi profil hatlarını özelleştirmesini sağlar. Güvenlik kuralları çerçevesinde kullanıcılar yalnızca ad ve soyad gibi temel kimlik bilgilerini değiştirebilir.

6. **Sepet Görüntüleme**
   - **API Metodu:** `GET /api/cart`
   - **Açıklama:** Kullanıcının takaslamak için değerlendirdiği ürünleri listelemesini sağlar. Sepetteki aktif öğeler, resimleriyle birlikte kullanıcıya sunulur.

7. **Sepete Ürün Ekleme**
   - **API Metodu:** `POST /api/cart/{id}`
   - **Açıklama:** Kullanıcının ilgilendiği bir ürünü sonradan onaylamak üzere sepetine almasını sağlar. Sistem kısıtlamaları gereği kullanıcılar kendi ürünlerini sepete ekleyemez ve sepette aynı anda en fazla bir ürün bulunabilir.

8. **Sepetten Ürün Çıkarma**
   - **API Metodu:** `DELETE /api/cart/{id}`
   - **Açıklama:** Kullanıcının sepetine eklediği ancak almaktan vazgeçtiği ürünü iptal etmesini sağlar. Seçilen id'ye ait ürün sepet listesinden temizlenir.

9. **Sepeti Onaylama (Satın Alma)**
   - **API Metodu:** `POST /api/cart/checkout/all`
   - **Açıklama:** Sepette bekleyen ürün için takas işlemini başlatır. Sistem arka planda kullanıcının kredi yeterliliğini kontrol eder; işlem uygunsa alıcıdan kredi düşülür, satıcının hesabında kredi beklemeye alınır ve ürün durumu "sold" olarak işaretlenir.

10. **Teslimat Onayı**
    - **API Metodu:** `POST /api/products/confirm-delivery/{id}`
    - **Açıklama:** Takaslanan ürünün alıcıya fiziksel ve sorunsuz bir şekilde teslim edildiğinin sistem üzerinden onaylanmasını sağlar. Bu onayla birlikte satıcı hesabında bekletilen kredi asıl bakiyeye aktarılır ve süreç tamamlanır.

11. **Aktif Ürünleri Listeleme**
    - **API Metodu:** `GET /api/products`
    - **Açıklama:** Platformda şu an takasa/satışa açık olan tüm onaylı ürünlerin görüntülenmesini sağlar. Kullanıcılara başlığa göre arama yapma ve filtreleme (fiyat, en yeni) imkanı sunulur.

13. **Ürün Detayı Görüntüleme**
    - **API Metodu:** `GET /api/products/{id}`
    - **Açıklama:** Seçilen bir ürünün kapsamlı sayfasına erişilmesini sağlar. Ürün resmi, açıklaması, istenen kredi miktarı ve sahibinin temel iletişim/hesap detayları gösterilir.

14. **Yeni Ürün Yükleme**
    - **API Metodu:** `POST /api/products`
    - **Açıklama:** Kullanıcıların takaslamak istedikleri yeni eşyaları sisteme kaydetmesini sağlar. Görseller ve ürün açıklamaları toplanarak veritabanına eklenir. Yüklenen kayıt, yöneticiler onaylayana kadar bekleyen "pending" statüsünde tutulur.

15. **Kendi Ürünlerini Görüntüleme**
    - **API Metodu:** `GET /api/products/my-listings`
    - **Açıklama:** Kullanıcının sisteme önceden yüklemiş olduğu kendi ilanlarını tek bir yerde görmesini sağlar. Hem hala aktif olan hem de satılmış ürünler listelenir.

16. **Ürün Silme**
    - **API Metodu:** `DELETE /api/products/{id}`
    - **Açıklama:** Kullanıcının kendi ürününü sistemden kalıcı olarak temizlemesini sağlar. Artık takaslanmak istenmeyen veya dışarıda elden çıkarılan ürünleri yayından kaldırmak için kullanılır.

18. **Giden Siparişleri Takip Etme**
    - **API Metodu:** `GET /api/products/orders`
    - **Açıklama:** Kullanıcının platform üzerinden aldığı ürünleri takip etmesini sağlar. Satın alınan ürünlerin teslimat durumları bu bölümden incelenir.

19. **Gelen Siparişleri Takip Etme**
    - **API Metodu:** `GET /api/products/incoming-sales`
    - **Açıklama:** Kullanıcının kendi ilanlarından satılan, alıcısı belli olan ürünleri listelemesini sağlar. Teslimatı yapılması gereken ürünler takip edilir.

20. **Tüm Kullanıcıları Listeleme (Yönetici)**
    - **API Metodu:** `GET /api/users`
    - **Açıklama:** Yöneticilerin sistemdeki tüm aktif ve inaktif üyeleri tek bir ekranda incelemesini sağlar. Kullanıcı kitlesini denetlemek ve yönetmek amacıyla kullanılır.

21. **Kullanıcı Bilgilerini Güncelleme (Yönetici)**
    - **API Metodu:** `PUT /api/users/{id}`
    - **Açıklama:** Yöneticilerin diğer hesaplar üzerinde kritik yetki ve denetim değişiklikleri yapmasını sağlar. Kullanıcı rolleri, onay durumları (isVerified) ve sistem bakiyeleri (credits) güncellenebilir.

22. **Hesap Silme (Yönetici)**
    - **API Metodu:** `DELETE /api/users/{id}`
    - **Açıklama:** Yöneticilerin kural ihlali yapan veya sistemden temizlenmesi gereken profilleri kalıcı olarak kaldırmasını sağlar. Kullanıcının satışa koyduğu tüm aktif ilanlar da sistemden otomatik silinir.

23. **Onay Bekleyen Ürünleri Görüntüleme (Yönetici)**
    - **API Metodu:** `GET /api/products/pending`
    - **Açıklama:** Yöneticilerin sisteme yeni yüklenmiş ancak henüz herkese görünür olmayan ürün içeriklerini modere etmesini sağlar.

24. **Ürün Onaylama (Yönetici)**
    - **API Metodu:** `PUT /api/products/approve/{id}`
    - **Açıklama:** Yöneticilerin standartlara uygun bulduğu ürünleri aktif yayına almasını sağlar. İşlem gerçekleştirildiğinde ürünü yükleyen kişiye sistemi kullandığı için ödül kredisi (+5 kredi) yüklenir.

25. **Tüm Satışları İnceleme (Yönetici)**
    - **API Metodu:** `GET /api/products/admin/sold`
    - **Açıklama:** Yöneticilerin platformda geçmişte başarıyla tamamlanmış olan bütün takas hareketlerini, alıcı ve satıcı eşleşmeleriyle birlikte listelemesini ve raporlamasını sağlar.

26. **Yapay Zeka ile Açıklama Üretme**
    - **API Metodu:** `POST /api/ai/generate-description`
    - **Açıklama:** Kullanıcıların ürün yükleme aşamasında Google Gemini modelini kullanarak otomatik bir ilan açıklaması yaratmasını sağlar. Sistem, üniversite öğrencisi diliyle ilgi çekici ve para kelimelerinin geçmediği metinler üretir.

27. **Yapay Zeka Asistanı ile Sohbet**
    - **API Metodu:** `POST /api/ai/chatbot`
    - **Açıklama:** Kullanıcıların ve ziyaretçilerin sistem işleyişi hakkında sisteme entegre öğrenci asistanına sorular yöneltmesini sağlar. Asistan, veritabanı belleği sayesinde geçmiş sorulara anında dönerek kurallara uygun yanıtlar verir.




