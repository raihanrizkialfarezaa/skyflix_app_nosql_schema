# Dokumentasi Query Database Skyflix

## Daftar Isi

1. [Users Collection](#users-collection)
2. [Actors Collection](#actors-collection)
2. [Studios Collection](#studios-collection)
2. [Directors Collection](#directors-collection)
2. [Genres Collection](#genres-collection)
2. [Films Collection](#films-collection)
2. [Reviews Collection](#reviews-collection)
2. [watchHistory Collection](#watchHistory-collection)
2. [Watchlist Collection](#watchlist-collection)
2. [Analitycs Collection](#analytics-collection)
2. [userRecommendations Collection](#userRecommendations-collection)
2. [watchHistory_archive Collection](#watchHistory_archive-collection)

## 1. Users Collection:
```javascript
db.users.insertMany([
  {
    _id: ObjectId(),
    username: "fahryan",
    email: "fahryan@gmail.com",
    password: "hashed_password",
    fullName: "Fahryan Akbar Rizqy Santoso",
    dateOfBirth: ISODate("1990-05-15"),
    country: "ID",
    createdAt: ISODate("2024-10-15T12:47:31Z"),
    preferences: [
      {
        genreId: ObjectId(),
        actorId: ObjectId(),
        preferenceScore: 0.9
      }
    ],
    paymentInfo: {
      cardType: "VISA",
      cardNumber: "4111111111111111",
      expirationDate: ISODate("2025-12-31")
    },
    subscription: {
      status: "active",
      startDate: ISODate("2023-01-01"),
      endDate: ISODate("2024-01-01")
    }
  },
  {
    _id: ObjectId(),
    username: "hanfik",
    email: "hanfik@gmail.com",
    password: "hashed_password",
    fullName: "Rayhan Syaputra Fikri",
    dateOfBirth: ISODate("1988-09-22"),
    country: "ID",
    createdAt: ISODate("2024-10-15T12:47:31Z"),
    preferences: [
      {
        genreId: ObjectId(),
        actorId: ObjectId(),
        preferenceScore: 0.8
      }
    ],
    paymentInfo: {
      cardType: "MasterCard",
      cardNumber: "5555555555554444",
      expirationDate: ISODate("2024-10-31")
    },
    subscription: {
      status: "active",
      startDate: ISODate("2023-02-15"),
      endDate: ISODate("2024-02-15")
    }
  }
])
```
Collection ini menyimpan data pengguna dengan struktur berikut:

- `_id`: ID unik MongoDB untuk setiap dokumen pengguna
- `username`: Nama pengguna untuk login (unique)
- `email`: Alamat email pengguna (unique)
- `password`: Password yang di-hash untuk keamanan
- `fullName`: Nama lengkap pengguna
- `dateOfBirth`: Tanggal lahir pengguna (format ISODate)
- `country`: Kode negara pengguna
- `createdAt`: Timestamp pembuatan akun
- `preferences`: Array yang berisi preferensi pengguna
  - `genreId`: ID genre yang disukai
  - `actorId`: ID aktor yang disukai
  - `preferenceScore`: Skor preferensi (0-1)
- `paymentInfo`: Object berisi informasi pembayaran
  - `cardType`: Jenis kartu (VISA/MasterCard)
  - `cardNumber`: Nomor kartu
  - `expirationDate`: Tanggal kadaluarsa kartu
- `subscription`: Object berisi info langganan
  - `status`: Status langganan (active/inactive)
  - `startDate`: Tanggal mulai langganan
  - `endDate`: Tanggal berakhir langganan

## 2. Actors Collection:
```javascript
db.actors.insertMany([
  {
    _id: ObjectId(),
    firstName: "Tom",
    lastName: "Hanks",
    dateOfBirth: ISODate("1956-07-09"),
    nationality: "American",
    biography: "Award-winning actor known for various roles",
    email: null,
    awards: [
      {
        awardName: "Academy Award for Best Actor",
        awardYear: 1994
      }
    ]
  },
  {
    _id: ObjectId(),
    firstName: "Scarlett",
    lastName: "Johansson",
    dateOfBirth: ISODate("1984-11-22"),
    nationality: "American",
    biography: "Versatile actress and singer",
    email: null,
    awards: [
      {
        awardName: "BAFTA Award for Best Actress",
        awardYear: 2020
      }
    ]
  },
  {
    _id: ObjectId(),
    firstName: "Benedict",
    lastName: "Cumberbatch",
    dateOfBirth: ISODate("1976-07-19"),
    nationality: "British",
    biography: "Known for playing Sherlock Holmes",
    email: null,
    awards: [
      {
        awardName: "Emmy Award for Outstanding Lead Actor",
        awardYear: 2014
      }
    ]
  }
])
```
Collection ini menyimpan data aktor dengan struktur:

- `_id`: ID unik MongoDB untuk setiap aktor
- `firstName`: Nama depan aktor
- `lastName`: Nama belakang aktor
- `dateOfBirth`: Tanggal lahir aktor
- `nationality`: Kewarganegaraan aktor
- `biography`: Biografi singkat aktor
- `email`: Email aktor (opsional)
- `awards`: Array berisi penghargaan yang diterima
  - `awardName`: Nama penghargaan
  - `awardYear`: Tahun menerima penghargaan

## 3. Studios Collection:
```javascript
db.studios.insertMany([
  {
    _id: ObjectId(),
    studioName: "Pixar",
    country: "USA",
    foundationYear: 1979,
    active: true,
    headquarters: {
      city: "Emeryville",
      state: "California",
      country: "USA"
    }
  },
  {
    _id: ObjectId(),
    studioName: "Studio Ghibli",
    country: "Japan",
    foundationYear: 1985,
    active: true,
    headquarters: {
      city: "Koganei",
      state: "Tokyo",
      country: "Japan"
    }
  },
  {
    _id: ObjectId(),
    studioName: "Marvel Studios",
    country: "USA",
    foundationYear: 1993,
    active: true,
    headquarters: {
      city: "Burbank",
      state: "California",
      country: "USA"
    }
  }
])
```
Collection ini menyimpan data studio produksi dengan struktur:

- `_id`: ID unik MongoDB untuk setiap studio
- `studioName`: Nama studio
- `country`: Negara asal studio
- `foundationYear`: Tahun pendirian studio
- `active`: Status keaktifan studio (boolean)
- `headquarters`: Object berisi lokasi kantor pusat
  - `city`: Kota
  - `state`: Negara bagian/provinsi
  - `country`: Negara

Setiap collection juga memiliki index untuk optimasi query:
```javascript
let pixarId = db.studios.findOne({ studioName: "Pixar" })._id;
let ghibliId = db.studios.findOne({ studioName: "Studio Ghibli" })._id;
let marvelId = db.studios.findOne({ studioName: "Marvel Studios" })._id;
```
Index ini memastikan username bersifat unik dan mempercepat pencarian berdasarkan username.

## 4. Directors Collection:
```javascript
db.directors.insertMany([
  {
    _id: ObjectId(),
    directorName: "John Lasseter",
    nationality: "American",
    birthDate: ISODate("1957-01-12"),
    specialization: ["Animation", "Family Films"],
    activeYears: {
      start: 1978,
      end: null
    }
  },
  {
    _id: ObjectId(),
    directorName: "Hayao Miyazaki",
    nationality: "Japanese",
    birthDate: ISODate("1941-01-05"),
    specialization: ["Animation", "Fantasy"],
    activeYears: {
      start: 1963,
      end: null
    }
  },
  {
    _id: ObjectId(),
    directorName: "Jon Favreau",
    nationality: "American",
    birthDate: ISODate("1966-10-19"),
    specialization: ["Action", "Adventure"],
    activeYears: {
      start: 1996,
      end: null
    }
  }
])
```
Collection ini menyimpan data sutradara dengan struktur:

- `_id`: ID unik MongoDB untuk setiap sutradara
- `directorName`: Nama lengkap sutradara
- `nationality`: Kewarganegaraan sutradara
- `birthDate`: Tanggal lahir (format ISODate)
- `specialization`: Array berisi genre/bidang spesialisasi
- `activeYears`: Object berisi periode aktif
  - `start`: Tahun mulai berkarir
  - `end`: Tahun berhenti (null jika masih aktif)

```javascript
let lasseterId = db.directors.findOne({ directorName: "John Lasseter" })._id;
let miyazakiId = db.directors.findOne({ directorName: "Hayao Miyazaki" })._id;
let favreauId = db.directors.findOne({ directorName: "Jon Favreau" })._id;
```
Kode tersebut memiliki fungsi penting untuk menyimpan ID referensi dari para sutradara. Mari saya jelaskan secara detail:

```javascript
// Store director IDs for reference
let lasseterId = db.directors.findOne({ directorName: "John Lasseter" })._id;
let miyazakiId = db.directors.findOne({ directorName: "Hayao Miyazaki" })._id;
let favreauId = db.directors.findOne({ directorName: "Jon Favreau" })._id;
```

Fungsi utamanya:

1. **Menyimpan Reference ID:**
   - Kode ini mengambil ObjectID dari setiap sutradara dan menyimpannya dalam variabel
   - ObjectID ini akan digunakan sebagai referensi di collection lain (terutama Films collection)

2. **Metode yang Digunakan:**
   - `db.directors.findOne()`: Mencari satu dokumen dalam collection directors
   - `{ directorName: "..." }`: Query filter untuk mencari berdasarkan nama sutradara
   - `._id`: Mengakses field _id dari dokumen yang ditemukan

3. **Kegunaan Praktis:**
   ```javascript
   // Contoh penggunaan di Films collection
   {
     directors: [
       {
         directorId: lasseterId,  // Menggunakan ID yang disimpan
         directorName: "John Lasseter"
       }
     ]
   }
   ```

4. **Manfaat:**
   - **Referential Integrity**: Memastikan integritas referensi antar collection
   - **Query Efficiency**: Memudahkan join atau lookup antar collection
   - **Data Consistency**: Menghindari kesalahan penulisan ID secara manual
   - **Maintenance**: Memudahkan pembaruan data terkait di masa depan

5. **Contoh Use Case:**
   ```javascript
   // Mencari semua film yang disutradarai oleh John Lasseter
   db.films.find({
     "directors.directorId": lasseterId
   })
   ```

6. **Best Practice:**
   - Menyimpan ID dalam variabel menghindari pengulangan query
   - Memudahkan debugging jika ada masalah dengan referensi
   - Meningkatkan readability kode

Jadi, kode ini juga bagian penting dari sistem referensi database yang memungkinkan relasi antar collection berjalan dengan efisien dan konsisten.

## 5. Genres Collection:
```javascript
db.genres.insertMany([
  {
    _id: ObjectId(),
    genreName: "Animation",
    description: "Animated films and series",
    popularityRank: 1,
    ageGroup: "All",
    moods: [
      {
        moodId: ObjectId(),
        moodName: "Happy",
        intensity: 0.8
      },
      {
        moodId: ObjectId(),
        moodName: "Excited",
        intensity: 0.7
      }
    ],
    targetAudience: ["Children", "Family"],
    commonThemes: ["Adventure", "Coming of Age", "Friendship"]
  },
  {
    _id: ObjectId(),
    genreName: "Science Fiction",
    description: "Films set in imaginary future",
    popularityRank: 2,
    ageGroup: "Teens",
    moods: [
      {
        moodId: ObjectId(),
        moodName: "Excited",
        intensity: 0.9
      },
      {
        moodId: ObjectId(),
        moodName: "Thoughtful",
        intensity: 0.6
      }
    ],
    targetAudience: ["Teens", "Young Adults"],
    commonThemes: ["Technology", "Future", "Space"]
  },
  {
    _id: ObjectId(),
    genreName: "Drama",
    description: "Character development and emotional themes",
    popularityRank: 3,
    ageGroup: "Adults",
    moods: [
      {
        moodId: ObjectId(),
        moodName: "Thoughtful",
        intensity: 0.9
      },
      {
        moodId: ObjectId(),
        moodName: "Sad",
        intensity: 0.7
      }
    ],
    targetAudience: ["Adults"],
    commonThemes: ["Relationships", "Personal Growth", "Conflict"]
  }
])
```
Collection ini menyimpan kategori/genre film dengan struktur kompleks:

- `_id`: ID unik MongoDB untuk setiap genre
- `genreName`: Nama genre (Animation, Sci-Fi, dll)
- `description`: Deskripsi genre
- `popularityRank`: Peringkat popularitas
- `ageGroup`: Target kelompok usia
- `moods`: Array berisi mood/suasana yang terkait
  - `moodId`: ID unik untuk mood
  - `moodName`: Nama mood (Happy, Excited, dll)
  - `intensity`: Intensitas mood (0-1)
- `targetAudience`: Array target penonton
- `commonThemes`: Array tema umum dalam genre

```javascript
let animationId = db.genres.findOne({ genreName: "Animation" })._id;
let sciFiId = db.genres.findOne({ genreName: "Science Fiction" })._id;
let dramaId = db.genres.findOne({ genreName: "Drama" })._id;
```
Kode tersebut memiliki fungsi untuk menyimpan ID referensi dari genre-genre film. Mari saya jelaskan secara detail:

```javascript
// Store genre IDs for reference
let animationId = db.genres.findOne({ genreName: "Animation" })._id;
let sciFiId = db.genres.findOne({ genreName: "Science Fiction" })._id;
let dramaId = db.genres.findOne({ genreName: "Drama" })._id;
```

Fungsi utamanya:

1. **Menyimpan Reference ID Genre:**
   - Mengambil ObjectID dari setiap genre film
   - Menyimpannya dalam variabel untuk digunakan sebagai referensi
   - Digunakan untuk mengaitkan film dengan genre-genrenya

2. **Metode yang Digunakan:**
   ```javascript
   db.genres.findOne() // Mencari satu dokumen dalam collection genres
   { genreName: "Animation" } // Filter pencarian berdasarkan nama genre
   ._id // Mengambil ID dari dokumen yang ditemukan
   ```

3. **Contoh Penggunaan Praktis:**
   ```javascript
   // Penggunaan dalam Films collection
   {
     genres: [
       {
         genreId: animationId,  // Menggunakan ID yang tersimpan
         genreName: "Animation"
       },
       {
         genreId: sciFiId,
         genreName: "Science Fiction"
       }
     ]
   }
   ```

4. **Manfaat:**
   - **Data Consistency**: 
     - Memastikan konsistensi referensi genre dalam database
     - Menghindari kesalahan penulisan nama genre
   
   - **Query Efficiency**:
     ```javascript
     // Mencari semua film animasi
     db.films.find({
       "genres.genreId": animationId
     })
     ```

   - **Relational Mapping**:
     - Memudahkan pencarian film berdasarkan genre
     - Memungkinkan filtering dan kategorisasi film
     - Mendukung sistem rekomendasi berbasis genre

5. **Use Cases:**
   ```javascript
   // Menghitung jumlah film per genre
   db.films.aggregate([
     { $unwind: "$genres" },
     { $match: { "genres.genreId": animationId }},
     { $count: "total_animation_films" }
   ])

   // Mencari film dengan multiple genre
   db.films.find({
     "genres.genreId": { 
       $all: [animationId, sciFiId] 
     }
   })
   ```

6. **Best Practices yang Diterapkan:**
   - **Performance**: Menyimpan ID dalam variabel menghindari query berulang
   - **Maintenance**: Memudahkan perubahan atau update genre di masa depan
   - **Scalability**: Mendukung penambahan genre baru dengan mudah
   - **Error Prevention**: Mengurangi risiko kesalahan dalam referensi genre

7. **Kegunaan dalam Fitur Platform:**
   - Filtering film berdasarkan genre
   - Sistem rekomendasi berbasis genre
   - Kategorisasi konten
   - Analisis preferensi pengguna
   - Personalisasi konten berdasarkan genre favorit

Kode ini merupakan komponen penting dalam sistem kategorisasi dan pengorganisasian konten film dalam platform streaming, memungkinkan manajemen konten yang lebih efisien dan pengalaman pengguna yang lebih baik.

## 6. Films Collection:
```javascript
db.films.insertMany([
  {
    _id: ObjectId(),
    studioId: pixarId,
    isSeries: false,
    title: "Toy Story",
    releaseYear: 1995,
    duration: 81,
    description: "A story of toys that come to life",
    ageRating: "G",
    viewCount: 1000000,
    createdAt: ISODate("2024-10-15T12:52:56Z"),
    directors: [
      {
        directorId: lasseterId,
        directorName: "John Lasseter"
      }
    ],
    genres: [
      {
        genreId: animationId,
        genreName: "Animation"
      }
    ],
    cast: [
      {
        actorId: db.actors.findOne({ firstName: "Tom" })._id,
        characterName: "Woody",
        role: "Lead",
        screenTime: 45  // dalam minutes
      }
    ],
    technicalSpecs: {
      resolution: "4K",
      audioFormats: ["Dolby Digital", "DTS"],
      subtitleLanguages: ["English", "Spanish", "French"]
    },
    ratings: {
      imdb: 8.3,
      rottenTomatoes: 92,
      internal: 4.5
    },
    streamingQuality: ["SD", "HD", "4K"],
    availability: {
      regions: ["North America", "Europe", "Asia"],
      restrictions: []
    }
  },
  {
    _id: ObjectId(),
    studioId: marvelId,
    isSeries: false,
    title: "Iron Man",
    releaseYear: 2008,
    duration: 126,
    description: "The story of Tony Stark becoming Iron Man",
    ageRating: "PG-13",
    viewCount: 1500000,
    createdAt: ISODate("2024-10-15T12:52:56Z"),
    directors: [
      {
        directorId: favreauId,
        directorName: "Jon Favreau"
      }
    ],
    genres: [
      {
        genreId: sciFiId,
        genreName: "Science Fiction"
      }
    ],
    cast: [
      {
        actorId: db.actors.findOne({ firstName: "Scarlett" })._id,
        characterName: "Black Widow",
        role: "Supporting",
        screenTime: 30  // minutes
      }
    ],
    technicalSpecs: {
      resolution: "4K",
      audioFormats: ["Dolby Atmos", "DTS-X"],
      subtitleLanguages: ["English", "Spanish", "French", "German"]
    },
    ratings: {
      imdb: 7.9,
      rottenTomatoes: 94,
      internal: 4.3
    },
    streamingQuality: ["HD", "4K", "HDR"],
    availability: {
      regions: ["Global"],
      restrictions: ["Some scenes edited in certain regions"]
    }
  }
])
```
Collection ini adalah collection utama yang menyimpan data film dengan struktur yang sangat detail:

- `_id`: ID unik MongoDB untuk setiap film
- `studioId`: Referensi ke studio produksi
- `isSeries`: Boolean penanda film serial atau tidak
- `title`: Judul film
- `releaseYear`: Tahun rilis
- `duration`: Durasi dalam menit
- `description`: Sinopsis film
- `ageRating`: Rating usia
- `viewCount`: Jumlah penonton
- `createdAt`: Timestamp penambahan ke database
- `directors`: Array berisi sutradara
  - `directorId`: Referensi ke collection directors
  - `directorName`: Nama sutradara
- `genres`: Array berisi genre film
  - `genreId`: Referensi ke collection genres
  - `genreName`: Nama genre
- `cast`: Array berisi pemeran
  - `actorId`: Referensi ke collection actors
  - `characterName`: Nama karakter
  - `role`: Tipe peran (Lead/Supporting)
  - `screenTime`: Durasi tampil dalam menit
- `technicalSpecs`: Object spesifikasi teknis
  - `resolution`: Resolusi tersedia
  - `audioFormats`: Array format audio
  - `subtitleLanguages`: Array bahasa subtitle
- `ratings`: Object berisi rating dari berbagai sumber
  - `imdb`: Rating IMDB
  - `rottenTomatoes`: Rating Rotten Tomatoes
  - `internal`: Rating internal platform
- `streamingQuality`: Array kualitas streaming tersedia
- `availability`: Object informasi ketersediaan
  - `regions`: Array wilayah tersedia
  - `restrictions`: Array pembatasan jika ada

```javascript
let toyStoryId = db.films.findOne({ title: "Toy Story" })._id;
let ironManId = db.films.findOne({ title: "Iron Man" })._id;
```
Kode tersebut memiliki fungsi untuk menyimpan ID referensi dari film-film spesifik. Mari saya jelaskan secara detail:

```javascript
let toyStoryId = db.films.findOne({ title: "Toy Story" })._id;
let ironManId = db.films.findOne({ title: "Iron Man" })._id;
```

Fungsi utamanya:

1. **Menyimpan Reference ID Film:**
   - Mengambil ObjectID dari film "Toy Story" dan "Iron Man"
   - Menyimpannya dalam variabel untuk referensi
   - Digunakan untuk mengaitkan film dengan collection lain

2. **Metode yang Digunakan:**
   ```javascript
   db.films.findOne() // Mencari satu dokumen dalam collection films
   { title: "Toy Story" } // Filter pencarian berdasarkan judul film
   ._id // Mengambil ID dari dokumen yang ditemukan
   ```

3. **Contoh Penggunaan Praktis:**
   ```javascript
   // Penggunaan dalam Reviews collection
   {
     filmId: toyStoryId,
     rating: 9,
     commentText: "A classic animation that never gets old"
   }

   // Penggunaan dalam Watch History
   {
     filmId: ironManId,
     watchDate: ISODate("2023-05-16"),
     watchDuration: 126
   }
   ```

4. **Use Cases Spesifik:**

   a. **Reviews:**
   ```javascript
   // Mencari semua review untuk Toy Story
   db.reviews.find({ 
     filmId: toyStoryId 
   })
   ```

   b. **Watch History:**
   ```javascript
   // Mencari riwayat menonton Iron Man
   db.watchHistory.find({ 
     "film.filmId": ironManId 
   })
   ```

   c. **Watchlist:**
   ```javascript
   // Menambahkan film ke watchlist
   db.watchlist.updateOne(
     { userId: someUserId },
     { 
       $push: { 
         films: {
           filmId: toyStoryId,
           dateAdded: new Date()
         }
       }
     }
   )
   ```

5. **Manfaat:**
   - **Data Consistency**:
     - Memastikan referensi film yang konsisten
     - Menghindari duplikasi data film
   
   - **Query Performance**:
     - Optimasi pencarian berbasis ID
     - Mempercepat operasi join/lookup

   - **Data Integrity**:
     - Memastikan referensi yang valid
     - Memudahkan tracking film-related data

6. **Implementasi dalam Fitur:**

   a. **Sistem Rating:**
   ```javascript
   // Menghitung rating rata-rata
   db.reviews.aggregate([
     { $match: { filmId: toyStoryId }},
     { $group: {
       _id: null,
       averageRating: { $avg: "$rating" }
     }}
   ])
   ```

   b. **Analytics:**
   ```javascript
   // Menganalisis popularitas film
   db.watchHistory.aggregate([
     { $match: { "film.filmId": ironManId }},
     { $group: {
       _id: null,
       totalViews: { $sum: 1 },
       avgWatchDuration: { $avg: "$watchDuration" }
     }}
   ])
   ```

7. **Best Practices yang Diterapkan:**
   - **Efficiency**: Menyimpan ID untuk menghindari query berulang
   - **Maintainability**: Memudahkan update data terkait film
   - **Reliability**: Memastikan konsistensi referensi film
   - **Scalability**: Mendukung penambahan data terkait film

8. **Kegunaan dalam Analisis:**
   - Tracking performa film
   - Analisis engagement penonton
   - Pembuatan rekomendasi
   - Monitoring popularitas film
   - Analisis pola menonton

Kode ini merupakan komponen kunci dalam sistem manajemen konten dan analisis perilaku penonton dalam platform streaming, memungkinkan tracking yang akurat dan analisis yang mendalam tentang performa setiap film.

Dapat kita lihat bahwa Films collection memiliki banyak referensi ke collection lain (studioId, directorId, actorId, dll) yang membentuk relasi antar collection. Ini memungkinkan query yang kompleks untuk mendapatkan informasi lengkap tentang sebuah film.

## 7. Episodes Collection (Bagian dari Films Collection):
```javascript
db.films.updateOne(
  { title: "Sherlock" },
  {
    $set: {
      episodes: [
        {
          episodeId: ObjectId(),
          episodeNumber: 1,
          seasonNumber: 1,
          title: "A Study in Pink",
          duration: 88,
          releaseDate: ISODate("2010-07-25"),
          synopsis: "A woman in pink is the latest victim in a series of seemingly impossible suicides.",
          viewCount: 500000,
          cast: [
            {
              actorId: db.actors.findOne({ firstName: "Benedict" })._id,
              characterName: "Sherlock Holmes",
              screenTime: 75
            }
          ],
          ratings: {
            imdb: 8.8,
            internal: 4.7
          }
        },
        {
          episodeId: ObjectId(),
          episodeNumber: 2,
          seasonNumber: 1,
          title: "The Blind Banker",
          duration: 89,
          releaseDate: ISODate("2010-08-01"),
          synopsis: "Mysterious symbols and murders are discovered across London.",
          viewCount: 480000,
          cast: [
            {
              actorId: db.actors.findOne({ firstName: "Benedict" })._id,
              characterName: "Sherlock Holmes",
              screenTime: 80
            }
          ],
          ratings: {
            imdb: 8.5,
            internal: 4.5
          }
        }
      ]
    }
  }
)
```
Collection ini menyimpan data episode untuk film serial sebagai subdocument dalam Films collection:

- `episodeId`: ID unik untuk setiap episode
- `episodeNumber`: Nomor urut episode
- `seasonNumber`: Nomor season
- `title`: Judul episode
- `duration`: Durasi dalam menit
- `releaseDate`: Tanggal rilis episode
- `synopsis`: Ringkasan cerita episode
- `viewCount`: Jumlah penonton
- `cast`: Array pemeran dalam episode
  - `actorId`: Referensi ke collection actors
  - `characterName`: Nama karakter
  - `screenTime`: Durasi tampil dalam menit
- `ratings`: Object rating episode
  - `imdb`: Rating IMDB
  - `internal`: Rating internal platform

## 8. Reviews Collection:
```javascript
db.reviews.insertMany([
  {
    _id: ObjectId(),
    userId: db.users.findOne({ username: "john_doe" })._id,
    filmId: toyStoryId,
    rating: 9,
    commentText: "A classic animation that never gets old",
    datePosted: ISODate("2024-10-15T13:04:21Z"),
    likeCount: 0,
    isEdited: false,
    watchedComplete: true,
    sentiment: {
      positive: 0.9,
      negative: 0.1,
      neutral: 0.0
    },
    tags: ["nostalgic", "family-friendly", "innovative"],
    userPlatform: {
      device: "mobile",
      os: "iOS",
      appVersion: "2.1.0"
    }
  },
  {
    _id: ObjectId(),
    userId: db.users.findOne({ username: "jane_smith" })._id,
    filmId: ironManId,
    rating: 8,
    commentText: "Great start to the Marvel Cinematic Universe",
    datePosted: ISODate("2024-10-15T13:04:21Z"),
    likeCount: 0,
    isEdited: false,
    watchedComplete: true,
    sentiment: {
      positive: 0.8,
      negative: 0.1,
      neutral: 0.1
    },
    tags: ["action-packed", "superhero", "origin-story"],
    userPlatform: {
      device: "desktop",
      os: "Windows",
      appVersion: "2.1.0"
    }
  }
])
```
Collection ini menyimpan ulasan pengguna dengan analisis sentiment:

- `_id`: ID unik untuk setiap review
- `userId`: Referensi ke collection users
- `filmId`: Referensi ke collection films
- `rating`: Nilai rating (1-10)
- `commentText`: Teks ulasan
- `datePosted`: Timestamp posting
- `likeCount`: Jumlah like
- `isEdited`: Flag penanda edit
- `watchedComplete`: Flag penonton selesai menonton
- `sentiment`: Object analisis sentimen
  - `positive`: Skor sentimen positif (0-1)
  - `negative`: Skor sentimen negatif (0-1)
  - `neutral`: Skor sentimen netral (0-1)
- `tags`: Array tag terkait ulasan
- `userPlatform`: Object informasi platform
  - `device`: Jenis perangkat
  - `os`: Sistem operasi
  - `appVersion`: Versi aplikasi

## 9. Watch History Collection:
```javascript
db.watchHistory.insertMany([
  {
    _id: ObjectId(),
    userId: db.users.findOne({ username: "john_doe" })._id,
    contentType: "FILM",
    film: {
      filmId: toyStoryId,
      title: "Toy Story"
    },
    episode: null,
    watchDate: ISODate("2023-05-15"),
    watchDuration: 81,
    watchProgress: 100,
    lastWatchedPosition: 81,
    watchSession: {
      startTime: ISODate("2023-05-15T14:00:00Z"),
      endTime: ISODate("2023-05-15T15:21:00Z"),
      pauseCount: 2,
      bufferingEvents: 1,
      quality: "HD",
      device: {
        type: "smart_tv",
        model: "Samsung TV",
        osVersion: "Tizen 4.0"
      },
      network: {
        type: "wifi",
        speed: "50mbps"
      }
    },
    userInteractions: {
      rewinds: 1,
      forwards: 0,
      pauses: 2,
      qualityChanges: 0
    }
  },
  {
    _id: ObjectId(),
    userId: db.users.findOne({ username: "jane_smith" })._id,
    contentType: "FILM",
    film: {
      filmId: ironManId,
      title: "Iron Man"
    },
    episode: null,
    watchDate: ISODate("2023-05-16"),
    watchDuration: 126,
    watchProgress: 100,
    lastWatchedPosition: 126,
    watchSession: {
      startTime: ISODate("2023-05-16T20:00:00Z"),
      endTime: ISODate("2023-05-16T22:06:00Z"),
      pauseCount: 1,
      bufferingEvents: 0,
      quality: "4K",
      device: {
        type: "mobile",
        model: "iPhone 13",
        osVersion: "iOS 15.0"
      },
      network: {
        type: "5G",
        speed: "100mbps"
      }
    },
    userInteractions: {
      rewinds: 0,
      forwards: 1,
      pauses: 1,
      qualityChanges: 1
    }
  }
])
```
Collection ini mencatat riwayat menonton dengan detail teknis lengkap:

- `_id`: ID unik untuk setiap riwayat
- `userId`: Referensi ke collection users
- `contentType`: Tipe konten (FILM/EPISODE)
- `film`: Object referensi film
  - `filmId`: ID film
  - `title`: Judul film
- `episode`: Data episode (null jika bukan serial)
- `watchDate`: Tanggal menonton
- `watchDuration`: Durasi menonton
- `watchProgress`: Persentase progress (0-100)
- `lastWatchedPosition`: Posisi terakhir menonton (menit)
- `watchSession`: Object detail sesi menonton
  - `startTime`: Waktu mulai
  - `endTime`: Waktu selesai
  - `pauseCount`: Jumlah jeda
  - `bufferingEvents`: Jumlah buffering
  - `quality`: Kualitas streaming
  - `device`: Object informasi perangkat
    - `type`: Jenis perangkat
    - `model`: Model perangkat
    - `osVersion`: Versi OS
  - `network`: Object informasi jaringan
    - `type`: Tipe jaringan
    - `speed`: Kecepatan jaringan
- `userInteractions`: Object interaksi pengguna
  - `rewinds`: Jumlah mundur
  - `forwards`: Jumlah maju cepat
  - `pauses`: Jumlah jeda
  - `qualityChanges`: Jumlah perubahan kualitas

Collection ini sangat penting untuk analisis perilaku penonton dan optimasi pengalaman streaming.

## 10. Watchlist Collection:
```javascript
db.watchlist.insertMany([
  {
    _id: ObjectId(),
    userId: db.users.findOne({ username: "john_doe" })._id,
    films: [
      {
        filmId: ironManId,
        dateAdded: ISODate("2023-06-01"),
        priority: 1,
        notes: "Recommended by friend",
        addedFrom: "friend_recommendation",
        plannedWatchDate: ISODate("2023-06-15"),
        reminders: {
          enabled: true,
          frequency: "weekly"
        }
      }
    ],
    lastUpdated: ISODate("2023-06-01"),
    sortPreference: "priority",
    notificationSettings: {
      emailNotifications: true,
      pushNotifications: true,
      reminderDays: [1, 3] 
    }
  },
  {
    _id: ObjectId(),
    userId: db.users.findOne({ username: "jane_smith" })._id,
    films: [
      {
        filmId: toyStoryId,
        dateAdded: ISODate("2023-06-02"),
        priority: 2,
        notes: "Classic animation",
        addedFrom: "platform_recommendation",
        plannedWatchDate: ISODate("2023-06-20"),
        reminders: {
          enabled: false,
          frequency: null
        }
      }
    ],
    lastUpdated: ISODate("2023-06-02"),
    sortPreference: "dateAdded",
    notificationSettings: {
      emailNotifications: false,
      pushNotifications: true,
      reminderDays: [2] 
    }
  }
])
```
Collection ini menyimpan daftar film yang ingin ditonton pengguna:

- `_id`: ID unik untuk setiap watchlist
- `userId`: Referensi ke collection users
- `films`: Array film dalam watchlist
  - `filmId`: Referensi ke collection films
  - `dateAdded`: Tanggal penambahan
  - `priority`: Prioritas menonton (1-n)
  - `notes`: Catatan pengguna
  - `addedFrom`: Sumber rekomendasi
  - `plannedWatchDate`: Rencana tanggal menonton
  - `reminders`: Object pengaturan pengingat
    - `enabled`: Status pengingat aktif
    - `frequency`: Frekuensi pengingat
- `lastUpdated`: Timestamp update terakhir
- `sortPreference`: Preferensi pengurutan
- `notificationSettings`: Object pengaturan notifikasi
  - `emailNotifications`: Status notifikasi email
  - `pushNotifications`: Status notifikasi push
  - `reminderDays`: Array hari pengingat sebelum tanggal rencana

## 11. Analytics Collection:
```javascript
db.analytics.insertMany([
  {
    _id: ObjectId(),
    filmId: toyStoryId,
    period: "2024-Q1",
    dailyStats: [
      {
        date: ISODate("2024-01-01"),
        viewCount: 1000,
        uniqueViewers: 950,
        averageWatchDuration: 75,
        completionRate: 0.92,
        peakViewingHours: {
          start: 20, // 8 PM
          end: 22    // 10 PM
        },
        deviceDistribution: {
          mobile: 0.3,
          tablet: 0.1,
          desktop: 0.2,
          smart_tv: 0.4
        },
        qualityDistribution: {
          "4K": 0.4,
          "HD": 0.5,
          "SD": 0.1
        }
      }
    ],
    demographicData: {
      ageGroups: {
        "0-12": 0.3,
        "13-17": 0.15,
        "18-24": 0.25,
        "25-34": 0.2,
        "35+": 0.1
      },
      genderDistribution: {
        male: 0.48,
        female: 0.51,
        other: 0.01
      },
      topRegions: [
        {
          region: "North America",
          viewershipShare: 0.45
        },
        {
          region: "Europe",
          viewershipShare: 0.30
        }
      ]
    },
    engagement: {
      averageRating: 4.5,
      reviewCount: 1500,
      shareCount: 500,
      addedToWatchlist: 2000,
      socialMediaMentions: {
        twitter: 1200,
        facebook: 800,
        instagram: 1500
      }
    },
    technicalMetrics: {
      averageBufferingTime: 0.8,
      streamingErrors: 25,
      averageBitrate: "8mbps",
      cdnPerformance: {
        latency: 45,
        errorRate: 0.002
      }
    }
  }
])
```
Collection ini menyimpan data analitik detail untuk setiap film:

- `_id`: ID unik untuk setiap analitik
- `filmId`: Referensi ke collection films
- `period`: Periode analisis (e.g., "2024-Q1")
- `dailyStats`: Array statistik harian
  - `date`: Tanggal statistik
  - `viewCount`: Jumlah penonton
  - `uniqueViewers`: Penonton unik
  - `averageWatchDuration`: Rata-rata durasi menonton
  - `completionRate`: Tingkat penyelesaian
  - `peakViewingHours`: Object jam sibuk
    - `start`: Jam mulai peak
    - `end`: Jam akhir peak
  - `deviceDistribution`: Object distribusi perangkat
  - `qualityDistribution`: Object distribusi kualitas
- `demographicData`: Object data demografi
  - `ageGroups`: Object distribusi usia
  - `genderDistribution`: Object distribusi gender
  - `topRegions`: Array region teratas
    - `region`: Nama region
    - `viewershipShare`: Persentase penonton
- `engagement`: Object metrik engagement
  - `averageRating`: Rating rata-rata
  - `reviewCount`: Jumlah review
  - `shareCount`: Jumlah share
  - `addedToWatchlist`: Jumlah tambah ke watchlist
  - `socialMediaMentions`: Object mention media sosial
- `technicalMetrics`: Object metrik teknis
  - `averageBufferingTime`: Rata-rata waktu buffering
  - `streamingErrors`: Jumlah error streaming
  - `averageBitrate`: Rata-rata bitrate
  - `cdnPerformance`: Object performa CDN
    - `latency`: Latensi
    - `errorRate`: Tingkat error

## 12. Indexes untuk Optimasi:
```javascript
// Users Collection Indexes
db.users.createIndex({ "username": 1 }, { unique: true })
db.users.createIndex({ "email": 1 }, { unique: true })
db.users.createIndex({ "subscription.status": 1 })
db.users.createIndex({ "subscription.endDate": 1 })
db.users.createIndex({ 
    "fullName": "text",
    "email": "text" 
})
```

Penjelasan index:
- Index pada username dan email dengan {unique: true} memastikan tidak ada duplikasi
- Index pada subscription.status mempercepat query status langganan
- Index pada subscription.endDate mempercepat query tanggal kadaluarsa
- Text index pada fullName dan email memungkinkan pencarian teks full-text

Keseluruhan struktur database ini dirancang untuk:
1. Mendukung streaming platform dengan fitur lengkap
2. Memungkinkan analisis mendalam tentang perilaku penonton
3. Optimasi performa dengan penggunaan index yang tepat
4. Fleksibilitas untuk pengembangan fitur baru
5. Tracking detail untuk peningkatan layanan