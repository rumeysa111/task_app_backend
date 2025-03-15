📝 **Task Manager API**

Bu proje, **Node.js, Express ve TypeScript** kullanılarak geliştirilmiştir. Kullanıcı yönetimi, görev takibi ve offline senkronizasyon gibi özellikler sunar.

##  Özellikler
✅ Kullanıcı yönetimi (kayıt, giriş, doğrulama)  
✅ Görev oluşturma, listeleme ve silme  
✅ JWT tabanlı kimlik doğrulama  
✅ Offline senkronizasyon desteği  
✅ Docker ile konteynerleştirme  

---

## 🛠️ Teknolojiler
| **Teknoloji** | **Açıklama** |
|--------------|-------------|
| **TypeScript** | Tip güvenliği ve güçlü geliştirme deneyimi sağlar. |
| **Node.js & Express** | API sunucusu için kullanılmıştır. |
| **PostgreSQL** | Veritabanı yönetimi için kullanılmıştır. |
| **Drizzle ORM** | SQL işlemlerini kolaylaştırmak için tercih edilmiştir. |
| **JWT** | Kimlik doğrulama mekanizması olarak kullanılmıştır. |
| **bcryptjs** | Şifre güvenliği ve hashing işlemleri için eklenmiştir. |
| **Docker** | Konteynerleştirme ve dağıtım için kullanılmıştır. |

---

## 📁 Proje Yapısı
```
backend/
├── src/
│   ├── db/               # Veritabanı işlemleri
│   ├── middleware/       # API ara yazılımları
│   ├── routes/           # API rotaları
│   └── index.ts          # Uygulama giriş noktası
├── docker-compose.yml    # Docker yapılandırması
├── Dockerfile            # Docker imaj tanımı
└── tsconfig.json         # TypeScript yapılandırması
```

---

## ⚙️ Kurulum ve Çalıştırma

### 📌 Normal Kurulum
1. Depoyu klonlayın:
   ```sh
   git clone https://github.com/rumeysa111/task_app_backend.git

   ```

2. Bağımlılıkları yükleyin:
   ```sh
   npm install
   ```

3. Geliştirme sunucusunu başlatın:
   ```sh
   npm run dev
   ```

---

### 🐳 Docker ile Çalıştırma
Eğer Docker kullanıyorsanız aşağıdaki komut ile konteynerleri çalıştırabilirsiniz:
```sh
docker-compose up
```

---

## 📚 API Dokümantasyonu

### 🧑‍💼 Kullanıcı Yönetimi
| **Endpoint** | **Metod** | **Açıklama** |
|-------------|----------|-------------|
| `/auth/signup` | `POST` | Yeni kullanıcı oluştur |
| `/auth/login` | `POST` | Kullanıcı girişi yap |
| `/auth/tokenIsValid` | `GET` | Token doğrulama |
| `/auth/` | `GET` | Kullanıcı bilgilerini getir |

### ✅ Görev Yönetimi
| **Endpoint** | **Metod** | **Açıklama** |
|-------------|----------|-------------|
| `/tasks/` | `POST` | Yeni görev oluştur |
| `/tasks/` | `GET` | Tüm görevleri getir |
| `/tasks/` | `DELETE` | Görevi sil |
| `/tasks/sync` | `POST` | Görevleri senkronize et |

---
## 📝 Örnek İstekler

### 🔐 Kullanıcı İşlemleri

#### Kullanıcı Kaydı
```bash
curl -X POST http://localhost:8000/auth/signup \
  -H "Content-Type: application/json" \
  -d '{"email": "test@example.com", "password": "password123"}'
```

#### Kullanıcı Girişi
```bash
curl -X POST http://localhost:8000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "test@example.com", "password": "password123"}'
```

### ✅ Görev İşlemleri

#### Yeni Görev Oluşturma
```bash
curl -X POST http://localhost:8000/tasks \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"title": "Yeni Görev", "description": "Açıklama", "dueAt": "2025-03-30T15:00:00Z"}'
```

#### Görevleri Listeleme
```bash
curl -X GET http://localhost:8000/tasks \
  -H "Authorization: Bearer YOUR_TOKEN"
```

#### Görevleri Senkronize Etme
```bash
curl -X POST http://localhost:8000/tasks/sync \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"tasks": [{"id": "1", "title": "Senkronize Görev", "description": "Açıklama", "completed": false}]}'
```

## 🔐 Güvenlik
✅ bcryptjs ile şifre hashing  
✅ JWT tabanlı kimlik doğrulama  
✅ Güvenli veritabanı yapılandırması  

---

## 💾 Veritabanı
Bu API'de **PostgreSQL** veritabanı ve **Drizzle ORM** kullanılmıştır.

| **Tablo** | **Açıklama** |
|----------|-------------|
| `users` | Kullanıcı bilgileri ve kimlik doğrulama |
| `tasks` | Kullanıcı görev bilgileri ve ilişkileri |

---

## 🐳 Docker Kullanımı
Aşağıda **Docker Compose** yapılandırması yer almaktadır:

```yaml
services:
  app:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db
  
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: test123
      POSTGRES_DB: mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data
```

Eğer PostgreSQL veritabanı için bir **Docker volume** kullanıyorsanız, temiz bir başlatma yapmak için aşağıdaki komutu kullanabilirsiniz:
```sh
docker-compose down -v
docker-compose up --build
```


