# LostPet AI 🐾

LostPet AI, kayıp ve bulunan evcil hayvan ilanlarının yönetilebildiği, **Spring Boot tabanlı bir backend uygulamasıdır**.

Proje, yalnızca bir kayıp hayvan platformu geliştirmekten ziyade, gerçek bir backend projesinde kullanılan teknolojileri **aşamalı olarak öğrenmek ve uygulamak** amacıyla geliştirilmektedir.

Proje geliştikçe yeni teknolojiler ve özellikler eklenerek basit bir REST API'den daha kapsamlı bir uygulamaya dönüştürülmesi hedeflenmektedir.

---

## 🎯 Project Goals

Bu projede temel hedefler:

- Spring Boot ekosistemini öğrenmek
- RESTful API geliştirmek
- PostgreSQL ve JPA/Hibernate kullanmak
- Authentication ve Authorization süreçlerini öğrenmek
- Git ve GitHub ile proje geliştirme sürecini yönetmek
- Docker ile uygulamayı containerize etmek
- Unit testing ve deployment süreçlerini öğrenmek
- İlerleyen aşamalarda AI ve harita teknolojilerini projeye entegre etmek

Proje, tüm özellikleri baştan geliştirmek yerine **aşamalı olarak büyütülecektir.**

---

# 🛠️ Tech Stack

### Backend

- Java 21
- Spring Boot 3
- Spring Web
- Spring Data JPA
- Spring Security
- JWT
- Hibernate
- Bean Validation
- Lombok
- Swagger / OpenAPI

### Database

- PostgreSQL

### Frontend

- React
- Tailwind CSS

### DevOps

- Git
- GitHub
- Docker
- Docker Compose

### Future Technologies

- FastAPI
- OpenCV
- CLIP
- Leaflet
- Email Notifications

---

# 🚀 Development Roadmap

## V1 — Core Backend

**Goal:** Spring Boot ve temel backend geliştirme konularını öğrenmek.

### User Management

- User registration
- User login
- JWT-based authentication
- Role-based authorization

### Pet Listings

- Create a listing
- Update a listing
- Delete a listing
- List all listings
- View listing details

### Listing Fields

Her ilan aşağıdaki temel bilgileri içerecektir:

- Title
- Description
- Animal Type
- City
- District
- Contact Information
- Status
- Created At

> İlk versiyonda konum bilgisi yalnızca şehir ve ilçe olarak tutulacaktır.

### V1 Learning Topics

- Entity
- DTO
- Repository
- Service
- Controller
- REST API
- JPA / Hibernate
- PostgreSQL
- Entity Relationships
- Validation
- Exception Handling
- Spring Security
- JWT
- Swagger / OpenAPI

---

# 📸 V2 — Application Features

İlk backend yapısı tamamlandıktan sonra uygulamaya daha gerçekçi özellikler eklenecektir.

### Planned Features

- Photo upload
- MultipartFile
- Local file storage
- City-based filtering
- Search
- Pagination

Bu aşamada özellikle **file handling, filtering ve pagination** konularının öğrenilmesi hedeflenmektedir.

---

# ⚙️ V3 — Production-Oriented Development

Uygulamanın daha gerçek bir deployment sürecine yaklaştırılması hedeflenmektedir.

### Planned Features

- Docker Compose
- Environment Variables
- Logging
- Unit Tests
- Integration Tests
- GitHub Actions
- CI/CD
- Deployment

### Possible Deployment Platforms

- Railway
- Render

---

# 🤖 V4 — AI & Smart Features

Temel backend ve deployment süreçleri tamamlandıktan sonra AI destekli özellikler araştırılacaktır.

### Planned Features

- Visual similarity analysis
- Animal type classification
- OCR
- Smart lost/found matching
- Map integration
- Notification system

### Possible Technologies

- FastAPI
- OpenCV
- CLIP
- Leaflet

> AI özellikleri projenin ilk aşamasının bir parçası değildir. Öncelik, sağlam bir backend altyapısı oluşturmaktır.

---

# 📚 Learning Roadmap

Proje aşağıdaki sırayla geliştirilecektir:

1. Spring Boot
2. REST API
3. PostgreSQL
4. JPA / Hibernate
5. Entity Relationships
6. DTO & Mapper
7. Validation
8. Exception Handling
9. Spring Security
10. JWT
11. Swagger / OpenAPI
12. Git & GitHub
13. Docker
14. React
15. File Upload
16. Testing
17. CI/CD
18. Deployment
19. AI Integration

---

# 📂 Project Structure

Proje geliştikçe backend tarafında katmanlı bir mimari kullanılacaktır.

```text
lostpet/
│
├── backend/
│   └── src/
│       └── main/
│           └── java/
│               └── com/lostpet/
│                   ├── controller/
│                   ├── service/
│                   ├── repository/
│                   ├── entity/
│                   ├── dto/
│                   ├── mapper/
│                   ├── security/
│                   ├── exception/
│                   └── config/
│
├── frontend/
│
├── docker-compose.yml
└── README.md
