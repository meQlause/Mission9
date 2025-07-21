# Mission9 Database Setup

This project uses **PostgreSQL in Docker** with an auto-initializing SQL script.

## 📦 Requirements

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## 🚀 Getting Started

1. Clone the repository:

   ```bash
   git clone <your-repo-url>
   cd Mission9
   ```

2. Run the database:

   ```bash
   docker-compose up --build
   ```

   On the **first run**, Docker will:

   - Start a PostgreSQL container  
   - Automatically execute `init/init.sql` to create the tables

## ⚠️ Resetting the Database

If you want to re-run the `init.sql` (e.g., after editing the schema), you **must delete Docker's internal volume**.  
PostgreSQL **only executes `init.sql` when the database is empty** (i.e., uninitialized).

### 🧹 Reset Steps

```bash
docker-compose down --volumes
docker volume prune -f     # optional: clean unused volumes
docker-compose up --build
```

> This will wipe all data and re-run the SQL script from scratch.

## 📁 File Structure

```
Mission9/
├── init/
│   └── init.sql              # SQL script to initialize schema
├── docker-compose.yml        # PostgreSQL container config
└── README.md
```

## 📝 Notes

- The SQL script creates tables like:
  - `produk`, `kategori_kelas`, `tutor`, `users`, `orders`, `pembayaran`
  - `kelas_saya`, `pretest`, `review`, `modul_kelas`, `material`
- Foreign keys and `ON DELETE CASCADE` are used to maintain data integrity.
- No Docker volumes are defined, so data is always reset unless you add persistence manually.
