## Step-by-Step running Aplikasi flask auth

1. Pastikan menggunakan pyton 3.11 (If docker python:3.11-slim)
2. Install package pendukung 
  ```
  apt-get update && apt-get install -y libpq-dev gcc && rm -rf /var/lib/apt/lists/*
  ```
3. Install requirements.txt
  ```
  pip install --no-cache-dir -r requirements.txt
  ```
4. Jalankan app python
  ```
  python app.py
  ```
## Yang perlu diperhatikan
1. Aplikasi akan expose di port 5000
2. Ketika dijalankan aplikasi butuh environment untuk connect ke database sebagai berikut
  ```
  DATABASE_URL: postgresql://user:password@service_db:port/db_name
  ```

## Clue Dockerfile
berikut adalah contoh Dockerfile yang berisi Instruction, anda dapat melengkapi dengan argument
  ```
  # Base Image Pyton
  FROM ___

  # Install library pendukung untuk PostgreSQL
  RUN ___

  WORKDIR /app
  # Copy semua file ke container
  COPY ___
  # Install requirements.txt
  RUN ___
  # Expose aplikasi python, port 5000
  EXPOSE ___
  # Command untuk menjalankan aplikasi python
  CMD ["___", "___"]
  ```
## Clue docker compose

  ```
# Version Compose, disarankan 3
version: ___

services:
# Service untuk database postgress
  db:
    image: ___
    restart: always
    # Environment Postgres ada 3
    environment:
      ___
      ___
      ___
    # Volumes untuk postgres
    volumes:
      - ___
    # Networks untuk postgres & aplikasi agar terhubung
    networks:
      - ___

  aplikasi:
    # Agar compose dapat melakukan build image terhadap aplikasi
    build: ___
    # Port Expose aplikasi
    ports:
      - ____
    environment:
      # Nama host di URL tetap 'db' karena merujuk pada nama service dalam network yang sama
      DATABASE_URL: postgresql://user:password@NAMA_HOST_DB:5432/NAMA_DATABSE
    # Networks untuk postgres & aplikasi agar terhubung
    networks:
      - ___

networks:
  # Networks untuk postgres & aplikasi agar terhubung
  ____:
    driver: bridge

volumes:
  # Volumes untuk postgres  
  ____:
   ```