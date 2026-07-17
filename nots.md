JAVA- Stream: list üstünde kolay işlem yapmayı sağlar.

Maven: bağımlılıkları yönetir, projenin build edilmesini sağlar.

    pom.xml: Projedeki tüm bağımlılıkların (dependencies) bulunduğu XML dosyasıdır. 
             Maven internetten gerekli kütüphaneleri indirir otomatik.  

Hibernate: Java objects ile database table arasındaki çeviriyi yapan ORM (Object Relational Mapping) aracıdır. java class --> database table 

── JPA / HIBERNATE ANNOTATION'LARI ───
@Entity    → "Bu sınıf bir veritabanı tablosudur" diye Hibernate'e bildirir
@Table     → Tablo adını belirtir. Belirtmezsek sınıf adı kullanılır (user → user)

Entity: Veritabanındaki bir tabloyu temsil eden Java sınıfıdır. 

*   Java                    Veritabanı
*   ──────────────────    ────────────────────────────
*   User sınıfı      →   "users" tablosu
*   User nesnesi     →   tablodaki bir SATIR (row)
*   String email     →   "email" SÜTUNU (column)
*
* Hibernate bu dönüşümü otomatik yapar.

Dependency: projenin çalışabilmesi için ihtiyaç duyduğu hazır kütüphanelerdir.

Lombok: Java programlama dilinde sürekli tekrarlanan standart kodları (getter, setter, constructor vb.) ortadan kaldıran bir açık kaynak kütüphanedir.

── LOMBOK ANNOTATION'LARI ───
@Data      → getter, setter, toString, equals, hashCode metodlarını otomatik üretir
@Builder   → User.builder().email("...").password("...").build() şeklinde nesne oluşturmayı sağlar
@NoArgsConstructor → boş constructor: new User()
@AllArgsConstructor → tüm alanları alan constructor: new User(id, firstName, ...)

Swagger: Geliştiricilerin, ek bir araca (Postman vb.) ihtiyaç duymadan arayüzdeki "Try it out" butonu ile canlı veri testi yapmasını sağlar

ENUM NEDİR: önceden belirlenmiş sabit değerler kümesidir. Bir şeyin sadece belirli değerler alabileceğini garantiler.

═══════════════════════════════════════════════════════════════════════════════════════════

@Id : primary key olduğunu belirtir

DTO (Data Transfer Object): "Dış dünyaya hangi verinin gidip geleceğini belirleyen veri paketidir.

    -Sadece o iş için gereken alanları taşır
    -API'ye gelen ve API'den giden veriyi taşır.
    -Frontend’e gitmeyen verilerin(private alanlar, şifre, ID, foreign key’ler vb.) gönderilmemiş olur
    
    - dto yazarken record kullanılır, constructor-getter-setter vs yazmaya gerek kalmaz otomatik tanımlanır
    - record sayesinde immituable olur



@NotBlank → null veya boş string kabul etme
   ""    → hata verir
   " "   → hata verir (sadece boşluksa da geçersiz)
         
        
Mapper: (MapStruct)
   - DTO ile Entity arasında alan eşleştirmesi ve gerektiğinde veri
     dönüşümü yapan sınıftır.
   - Service veya Controller içinde dönüşüm kodu yazılsaydı o sınıflar şişerdi.
   - Dönüşüm sorumluluğunu ayrı bir sınıfa veririz → Tek Sorumluluk İlkesi (SRP).
   - Mapper, frontend'den gelen veriyi Entity'ye dönüştürür ve hangi DTO
     alanının Entity'deki hangi alana aktarılacağını belirler. tam tersi içinde
     aynısı.


 JpaRepository<User, Long> extend edilince:
    save(user)           → INSERT veya UPDATE
    findById(id)         → SELECT * FROM users WHERE id = ?
    findAll()            → SELECT * FROM users
    delete(user)         → DELETE FROM users WHERE id = ?
    existsById(id)       → SELECT COUNT(*) FROM users WHERE id = ?
    count()              → SELECT COUNT(*) FROM users
    ... ve daha fazlası

Metod adını doğru yazarsan Spring otomatik SQL üretir:
Anahtar kelimeler: findBy, existsBy, countBy, deleteBy + alan adı
