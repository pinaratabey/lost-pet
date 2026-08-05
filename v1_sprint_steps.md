# LostPet AI - V1 Sprint: Adım Adım Geliştirme Planı

> Bu dosya projeyi geliştirirken izleyeceğimiz yol haritasıdır.  
> Her adım tamamlandığında `[ ]` → `[x]` olarak işaretlenecektir.

---

## Faz 0: Ortam Hazırlığı
> **Hedef:** Geliştirme ortamını hazır hale getirmek

- [ ] **Adım 0.1** — Java 21 JDK kurulumunu doğrula (`java -version`)
- [ ] **Adım 0.2** — Maven kurulumunu doğrula (`mvn -version`)
- [ ] **Adım 0.3** — PostgreSQL kurulumu (Docker veya lokal)
- [ ] **Adım 0.4** — Git kurulumunu doğrula ve repo'yu initialize et
- [ ] **Adım 0.5** — IDE ayarları (Lombok plugin, Java 21 SDK)

### 📦 Çıktı
- Çalışır durumda Java, Maven, PostgreSQL ve Git

---

## Faz 1: Spring Boot Proje İskeleti
> **Hedef:** Boş ama çalışan bir Spring Boot projesi oluşturmak  
> **Öğrenilecek:** Spring Initializr, pom.xml, application.yml, proje yapısı

- [x] **Adım 1.1** — Spring Initializr ile proje oluştur
  - Group: `com.lostpet`
  - Artifact: `lostpet-backend`
  - Java: 21
  - Dependencies: Spring Web, Spring Data JPA, PostgreSQL Driver, Spring Security, Validation, Lombok, SpringDoc OpenAPI
- [x] **Adım 1.2** — `pom.xml` dosyasını kontrol et ve eksik bağımlılıkları ekle
  - JWT kütüphanesi: `jjwt-api`, `jjwt-impl`, `jjwt-jackson`
- [x] **Adım 1.3** — `application.yml` konfigürasyonu
  - PostgreSQL bağlantı bilgileri
  - JPA/Hibernate ayarları (`ddl-auto: update`)
  - Server port: 8080
  - JWT secret key ve expiration süresi
- [x] **Adım 1.4** — `application-dev.yml` profili oluştur
- [x] **Adım 1.5** — `.gitignore` dosyasını yapılandır
- [x] **Adım 1.6** — Projeyi çalıştır ve `localhost:8080` erişimini doğrula
- [x] **Adım 1.7** — İlk commit: `feat: initialize spring boot project`

### 📦 Çıktı
- `mvn spring-boot:run` ile başarıyla ayağa kalkan proje
- PostgreSQL'e bağlanan boş bir uygulama

---

## Faz 2: Entity ve Repository Katmanı
> **Hedef:** Veritabanı tablolarını Java sınıflarıyla tanımlamak  
> **Öğrenilecek:** JPA Entity, Annotations, Enum, Repository, Entity İlişkileri

- [x] **Adım 2.1** — Enum sınıflarını oluştur
  - `enums/Role.java` → `USER`, `ADMIN`
  - `enums/AnimalType.java` → `DOG`, `CAT`, `BIRD`, `OTHER`
  - `enums/PostStatus.java` → `ACTIVE`, `FOUND`, `CLOSED`
- [x] **Adım 2.2** — `entity/User.java` Entity sınıfını oluştur
  - Alanlar: `id`, `firstName`, `lastName`, `email` (unique), `password`, `role`, `createdAt`
  - Annotations: `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, `@Enumerated`, `@CreationTimestamp`
  - Lombok: `@Data`, `@NoArgsConstructor`, `@AllArgsConstructor`, `@Builder`
- [x] **Adım 2.3** — `entity/Post.java` Entity sınıfını oluştur
  - Alanlar: `id`, `title`, `description`, `animalType`, `city`, `district`, `contactInfo`, `status`, `createdAt`, `updatedAt`
  - İlişki: `@ManyToOne` → User (bir kullanıcının birden fazla ilanı olabilir)
  - `@JoinColumn(name = "user_id")`
- [x] **Adım 2.4** — `repository/UserRepository.java` oluştur
  - `Optional<User> findByEmail(String email)`
  - `Boolean existsByEmail(String email)`
- [x] **Adım 2.5** — `repository/PostRepository.java` oluştur
  - `List<Post> findByUserId(Long userId)`
  - `List<Post> findByStatus(PostStatus status)`
- [x] **Adım 2.6** — Uygulamaı çalıştır, tabloların oluştuğunu PostgreSQL'de doğrula
- [x] **Adım 2.7** — Commit: `feat: add User and Post entities with repositories`

### 📦 Çıktı
- PostgreSQL'de `users` ve `posts` tabloları otomatik oluşmuş durumda
- Repository interface'leri hazır

---

## Faz 3: DTO ve Mapper Katmanı
> **Hedef:** İstemci ile sunucu arasındaki veri taşıma modellerini oluşturmak  
> **Öğrenilecek:** DTO pattern, Request/Response ayrımı, Java Record, Mapper

- [x] **Adım 3.1** — Request DTO'ları oluştur
  - `dto/request/RegisterRequest.java` → `firstName`, `lastName`, `email`, `password`
  - `dto/request/LoginRequest.java` → `email`, `password`
  - `dto/request/CreatePostRequest.java` → `title`, `description`, `animalType`, `city`, `district`, `contactInfo`
  - `dto/request/UpdatePostRequest.java` → Aynı alanlar (opsiyonel güncellenebilir)
- [x] **Adım 3.2** — Response DTO'ları oluştur
  - `dto/response/AuthResponse.java` → `token`, `email`, `firstName`
  - `dto/response/PostResponse.java` → Tüm ilan alanları + `ownerName`
  - `dto/response/UserResponse.java` → `id`, `firstName`, `lastName`, `email`
  - `dto/response/ApiResponse.java` → Generic wrapper: `success`, `message`, `data`
- [x] **Adım 3.3** — Validation annotation'ları ekle
  - `@NotBlank`, `@Email`, `@Size(min, max)`, `@NotNull`
- [x] **Adım 3.4** — Mapper sınıflarını oluştur
  - `mapper/UserMapper.java` → `toResponse(User)`, `toEntity(RegisterRequest)`
  - `mapper/PostMapper.java` → `toResponse(Post)`, `toEntity(CreatePostRequest, User)`
- [x] **Adım 3.5** — Commit: `feat: add DTOs, validation and mappers`

### 📦 Çıktı
- Request/Response DTO'ları validation ile hazır
- Mapper sınıfları Entity ↔ DTO dönüşümü yapabiliyor

---

## Faz 4: Exception Handling (Hata Yönetimi)
> **Hedef:** Anlamlı ve tutarlı hata yanıtları dönen bir yapı kurmak  
> **Öğrenilecek:** @ControllerAdvice, @ExceptionHandler, Custom Exception, HTTP Status Codes

- [x] **Adım 4.1** — Custom Exception sınıflarını oluştur
  - `exception/ResourceNotFoundException.java` → 404
  - `exception/DuplicateResourceException.java` → 409
  - `exception/UnauthorizedException.java` → 401
- [x] **Adım 4.2** — `exception/GlobalExceptionHandler.java` oluştur
  - `@RestControllerAdvice` ile merkezi hata yakalama
  - `MethodArgumentNotValidException` → Validation hataları (400)
  - `ResourceNotFoundException` → 404
  - `DuplicateResourceException` → 409
  - `UnauthorizedException` → 401
  - Genel `Exception` → 500
- [x] **Adım 4.3** — Hata yanıt formatı tanımla
  ```json
  {
    "success": false,
    "message": "İlan bulunamadı",
    "timestamp": "2026-07-13T15:30:00",
    "status": 404
  }
  ```
- [x] **Adım 4.4** — Commit: `feat: add global exception handling`

### 📦 Çıktı
- Tüm hatalar tutarlı JSON formatında dönüyor
- Her hata türü için doğru HTTP status code

---

## Faz 5: Service Katmanı (İş Mantığı)
> **Hedef:** İş mantığını controller'dan ayırarak service katmanında toplamak  
> **Öğrenilecek:** @Service, @Transactional, Business Logic, Entity-DTO dönüşümü

- [x] **Adım 5.1** — `service/UserService.java` oluştur
  - `getUserByEmail(String email)` → User entity döner
  - `existsByEmail(String email)` → Boolean
- [x] **Adım 5.2** — `service/PostService.java` oluştur
  - `createPost(CreatePostRequest, User)` → PostResponse
  - `getAllPosts()` → List\<PostResponse\>
  - `getPostById(Long id)` → PostResponse
  - `updatePost(Long id, UpdatePostRequest, User)` → PostResponse
  - `deletePost(Long id, User)` → void
  - `getMyPosts(User)` → List\<PostResponse\>
- [x] **Adım 5.3** — Yetkilendirme kontrolü ekle
  - Güncelleme ve silme işlemlerinde: "Bu ilan bu kullanıcıya mı ait?" kontrolü
- [x] **Adım 5.4** — Commit: `feat: add service layer with business logic`

### 📦 Çıktı
- Tüm iş mantığı Service katmanında
- Entity ↔ DTO dönüşümleri Mapper ile yapılıyor

---

## Faz 6: Security ve JWT Authentication
> **Hedef:** Kullanıcı kaydı, giriş ve JWT tabanlı kimlik doğrulama  
> **Öğrenilecek:** Spring Security, JWT, Filter, PasswordEncoder, UserDetails

- [ ] **Adım 6.1** — `security/JwtTokenProvider.java` oluştur
  - `generateToken(String email)` → JWT token üret
  - `getEmailFromToken(String token)` → Email çıkar
  - `validateToken(String token)` → Boolean
- [ ] **Adım 6.2** — `security/CustomUserDetailsService.java` oluştur
  - `UserDetailsService` implement et
  - `loadUserByUsername(String email)` → UserDetails
- [ ] **Adım 6.3** — `security/JwtAuthenticationFilter.java` oluştur
  - `OncePerRequestFilter` extend et
  - Her istekte Authorization header'ından JWT token al
  - Token'ı doğrula ve SecurityContext'e kullanıcıyı set et
- [ ] **Adım 6.4** — `config/SecurityConfig.java` oluştur
  - `SecurityFilterChain` bean tanımla
  - Public endpoint'leri (`/api/auth/**`, `GET /api/posts/**`) açık bırak
  - Diğer endpoint'leri authenticate et
  - JWT filter'ı zincire ekle
  - CORS yapılandırması
  - CSRF devre dışı (REST API için)
- [ ] **Adım 6.5** — `service/AuthService.java` oluştur
  - `register(RegisterRequest)` → AuthResponse (token ile birlikte)
  - `login(LoginRequest)` → AuthResponse (token ile birlikte)
  - PasswordEncoder ile şifre hashleme
  - Email duplicate kontrolü
- [ ] **Adım 6.6** — `controller/AuthController.java` oluştur
  - `POST /api/auth/register` → Kayıt ol
  - `POST /api/auth/login` → Giriş yap
- [ ] **Adım 6.7** — Postman ile test et
  - Kayıt ol → Token al
  - Giriş yap → Token al
  - Token olmadan korunan endpoint'e istek at → 401
  - Token ile korunan endpoint'e istek at → 200
- [ ] **Adım 6.8** — Commit: `feat: add JWT authentication and security`

### 📦 Çıktı
- Kullanıcı kayıt ve giriş yapabiliyor
- JWT token üretiliyor ve doğrulanıyor
- Korunan endpoint'lere sadece token ile erişilebiliyor

---

## Faz 7: Controller Katmanı (REST API)
> **Hedef:** Tüm API endpoint'lerini oluşturmak ve test etmek  
> **Öğrenilecek:** @RestController, @RequestMapping, @RequestBody, @PathVariable, @AuthenticationPrincipal, ResponseEntity

- [ ] **Adım 7.1** — `controller/PostController.java` oluştur
  - `POST /api/posts` → İlan oluştur (Auth gerekli)
  - `GET /api/posts` → Tüm ilanları listele (Public)
  - `GET /api/posts/{id}` → İlan detayı (Public)
  - `PUT /api/posts/{id}` → İlan güncelle (Auth + Owner)
  - `DELETE /api/posts/{id}` → İlan sil (Auth + Owner)
  - `GET /api/posts/my` → Kendi ilanlarım (Auth)
- [ ] **Adım 7.2** — `@AuthenticationPrincipal` ile mevcut kullanıcıyı al
- [ ] **Adım 7.3** — `@Valid` annotation ile request validation'ı aktif et
- [ ] **Adım 7.4** — ResponseEntity ile uygun HTTP status code'ları dön
  - `201 Created` → Oluşturma
  - `200 OK` → Güncelleme, listeleme
  - `204 No Content` → Silme
- [ ] **Adım 7.5** — Postman Collection oluştur ve tüm endpoint'leri test et
  - Kayıt ol
  - Giriş yap
  - İlan oluştur (token ile)
  - İlanları listele
  - İlan detayını gör
  - İlan güncelle (token ile, sadece kendi ilanı)
  - İlan sil (token ile, sadece kendi ilanı)
  - Başka kullanıcının ilanını silmeyi dene → 401/403
- [ ] **Adım 7.6** — Commit: `feat: add Post CRUD REST API endpoints`

### 📦 Çıktı
- Tüm CRUD endpoint'leri çalışıyor
- Validation hataları düzgün dönüyor
- Yetkilendirme kontrolü çalışıyor

---

## Faz 8: Swagger ve Docker
> **Hedef:** API dokümantasyonu ve konteynerizasyon  
> **Öğrenilecek:** SpringDoc OpenAPI, Swagger UI, Dockerfile, Docker Compose

- [ ] **Adım 8.1** — `config/SwaggerConfig.java` oluştur
  - API bilgilerini tanımla (title, description, version)
  - JWT Bearer authentication tanımı ekle
- [ ] **Adım 8.2** — Swagger UI'ı test et
  - `http://localhost:8080/swagger-ui.html` açıldığını doğrula
  - Tüm endpoint'lerin listelendiğini kontrol et
  - "Authorize" butonu ile JWT token girip test et
- [ ] **Adım 8.3** — `Dockerfile` oluştur
  - Multi-stage build: Maven build + Java 21 runtime
- [ ] **Adım 8.4** — `docker-compose.yml` oluştur
  - PostgreSQL service
  - Backend service (Dockerfile'dan build)
  - Environment variables
  - Volume: PostgreSQL data persistence
- [ ] **Adım 8.5** — Docker Compose ile projeyi ayağa kaldır
  - `docker-compose up -d`
  - Tüm endpoint'lerin çalıştığını doğrula
- [ ] **Adım 8.6** — `README.md` dosyasını oluştur
  - Proje açıklaması
  - Teknoloji yığını
  - Kurulum adımları
  - API endpoint tablosu
  - Docker ile çalıştırma
- [ ] **Adım 8.7** — Son commit: `feat: add Swagger docs, Docker support and README`

### 📦 Çıktı
- Swagger UI'da tüm endpoint'ler görünüyor ve test edilebiliyor
- `docker-compose up` ile tüm proje tek komutla ayağa kalkıyor
- Profesyonel README.md dosyası hazır

---

## 🏁 V1 Sprint Tamamlanma Kriterleri

| # | Kriter | Durum |
|---|--------|-------|
| 1 | Kullanıcı kayıt olabiliyor | ⬜ |
| 2 | Kullanıcı giriş yapıp JWT token alabiliyor | ⬜ |
| 3 | Token ile ilan oluşturulabiliyor | ⬜ |
| 4 | İlanlar listelenebiliyor (public) | ⬜ |
| 5 | İlan detayı görüntülenebiliyor | ⬜ |
| 6 | Sadece ilan sahibi güncelleme/silme yapabiliyor | ⬜ |
| 7 | Validation hataları anlamlı mesajlarla dönüyor | ⬜ |
| 8 | Swagger UI çalışıyor | ⬜ |
| 9 | Docker Compose ile proje ayağa kalkıyor | ⬜ |
| 10 | README.md profesyonel şekilde hazırlanmış | ⬜ |

---

## 📝 Notlar

- Her faz sonunda çalışan bir uygulama olacak
- Her fazda anlamlı Git commit'leri yapılacak
- Bir sonraki faza geçmeden önce mevcut faz tam test edilecek
- Hata ile karşılaşıldığında ilgili adımda not alınacak
