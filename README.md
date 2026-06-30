# Products API — NestJS & MongoDB Atlas

REST API untuk manajemen data produk, dibangun menggunakan NestJS sebagai backend framework dan MongoDB Atlas sebagai database cloud dengan Mongoose sebagai ODM (Object Data Modeling).

Proyek ini merupakan Tugas Praktikum 8 mata kuliah Pemrograman Web, dengan topik integrasi MongoDB Atlas & Mongoose pada aplikasi NestJS.

## Fitur

- CRUD lengkap (Create, Read, Update, Delete) untuk data produk
- Schema validation menggunakan Mongoose `@Prop()` decorator
- Pencarian produk berdasarkan nama (`/products/search?q=keyword`)
- Error handling: `404 Not Found` dan `400 Bad Request`
- Koneksi ke MongoDB Atlas (cloud database)

## Tech Stack

- [NestJS](https://nestjs.com/) — Backend framework (Node.js)
- [MongoDB Atlas](https://www.mongodb.com/atlas) — Cloud NoSQL database
- [Mongoose](https://mongoosejs.com/) — ODM untuk MongoDB
- TypeScript

## Struktur Data Product

| Field        | Tipe      | Keterangan                  |
|--------------|-----------|------------------------------|
| name         | string    | Wajib diisi                 |
| price        | number    | Wajib diisi, minimal 0      |
| description  | string    | Opsional                    |
| category     | string    | Opsional, default: "umum"   |
| stock        | number    | Default: 0                  |
| isAvailable  | boolean   | Default: true               |
| createdAt    | Date      | Otomatis (timestamps)       |
| updatedAt    | Date      | Otomatis (timestamps)       |

## API Endpoints

| Method | Endpoint                     | Deskripsi                          |
|--------|-------------------------------|-------------------------------------|
| POST   | `/products`                   | Menambah produk baru               |
| GET    | `/products`                   | Mendapatkan semua produk           |
| GET    | `/products/search?q=keyword`  | Mencari produk berdasarkan nama    |
| GET    | `/products/:id`               | Mendapatkan produk berdasarkan ID  |
| PUT    | `/products/:id`               | Mengupdate produk                  |
| DELETE | `/products/:id`               | Menghapus produk                   |

## Struktur Folder Proyek

```
nestjs-mongodb-crud/
├── dist/                          # Hasil build (auto-generated)
├── node_modules/                  # Dependencies (auto-generated)
├── src/
│   ├── products/
│   │   ├── dto/
│   │   │   ├── create-product.dto.ts
│   │   │   └── update-product.dto.ts
│   │   ├── schemas/
│   │   │   └── product.schema.ts
│   │   ├── products.controller.ts
│   │   ├── products.module.ts
│   │   └── products.service.ts
│   ├── app.controller.ts
│   ├── app.controller.spec.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   └── main.ts
├── test/
│   ├── app.e2e-spec.ts
│   └── jest-e2e.json
├── .env                           # Connection string MongoDB Atlas (tidak di-push ke GitHub)
├── .gitignore
├── .prettierrc
├── eslint.config.mjs
├── nest-cli.json
├── package.json
├── package-lock.json
├── README.md
├── tsconfig.build.json
└── tsconfig.json
```

## Instalasi & Menjalankan Project

1. Clone repository ini
```bash
   git clone <url-repo-ini>
   cd nestjs-products-api-mongodb
```

2. Install dependencies
```bash
   npm install
```

3. Buat file `.env` di root project, isi dengan connection string MongoDB Atlas kamu
```env
   MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<database>?retryWrites=true&w=majority
```

4. Jalankan aplikasi dalam mode development
```bash
   npm run start:dev
```

5. Server akan berjalan di `http://localhost:3000`

## Contoh Request

**Membuat produk baru**
```http
POST /products
Content-Type: application/json

{
  "name": "Laptop Asus ROG",
  "price": 15000000,
  "description": "Laptop gaming high-end",
  "category": "elektronik",
  "stock": 5
}
```

**Mencari produk**
```http
GET /products/search?q=laptop
```