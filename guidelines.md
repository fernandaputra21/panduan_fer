
# Panduan Kurasi Data

| Versi  | 0.1.0  |
| :------------ | :------------ |
| Catatan perubahan | - [2024-09-04] Rilis awal  |


## Pendahuluan

Format pengisian data ini disusun dengan mempertimbangkan kemudahan pembacaan komputer dan keseragaman pengisian data. Target awal untuk memiliki data pada tingkat spesies. Namun, format ini disiapkan untuk bisa terus dikembangkan hingga ke level subspecies maupun lebih rendah lagi tingkat taksonominya. Basis data ini juga akan berkembang menjadi panduan lapangan setelah karakter spesies diisi dan dilengkapi dengan foto/ilustrasi/suara/video. Isian data spesies juga memungkinkan untuk mengakses informasi pihak ketiga, misalnya data DNA lewat “Taxon Explorer” NCBI GenBank, data keberadaan spesies di GBIF, dan sebagainya.

## Kategori Data

Data dibagi menjadi tiga kategori: kelompok taksa, data taksa, dan media.

### **Data Kelompok Taksa**

Pengelompokan taksa tidak harus sesuai dengan kelompok kerja. Masing-masing kelompok kerja bisa membagi lagi datanya menjadi beberapa kelompok taksa (dibaca dataset). Setiap dataset memiliki metadata dan sistem penomoran sendiri. 

Maksimal total taksa per dataset perlu mempertimbangkan:

1. Kemudahan pembacaan dan pengisian data oleh manusia.  
2. Kapasitas distribusi. Semakin besar kelompok taksa semakin besar ukuran paket filenya. Data besar juga akan mempengaruhi waktu parsing oleh komputer.  
3. Jumlah taksa per kelompok taksa di Indonesia. Misalnya, untuk limit maksimal 1000 taksa, mamalia bisa dalam satu kelompok taksa, burung perlu dipecah minimal jadi dua kelompok, dst.  
   

Usulan maksimal 2000\. Isian bisa kurang, tetapi tidak boleh lebih.

### **Data Taksa**

Data ini berupa Google Sheets yang berisi daftar taksa dan informasi taksonominya. Penomoran dan metadata mengacu data kelompok taksa (dijelaskan dibawah).

### **Media**

Media tambahan yang bisa dipaketkan berbarengan dengan data taksa. Belum diprioritaskan untuk program tahap I. Media juga bisa menggunakan link eksternal selagi berada di domain publik. Lisensi medianya juga mengizinkan untuk digunakan oleh pihak ketiga.

## Sistem Penomoran

Penomoran kelompok taksa akan menggunakan Universally Unique Identifier (UUID) versi 7 ([https://en.wikipedia.org/wiki/Universally\_unique\_identifier](https://en.wikipedia.org/wiki/Universally\_unique\_identifier)). UUID memastikan keunikan identifikasi data dan memastikan data kita kompatibel dengan prinsip FAIR ([https://www.go-fair.org/fair-principles/](https://www.go-fair.org/fair-principles/)). UUID ini akan dicantumkan di file metadata. File metadata akan dihasilkan otomatis oleh program parsing yg sedang kita kembangkan.

**Usulan Penomoran Taksa**  
Untuk penomoran taksa, kita menggunakan sistem penomoran yang disepakati bersama. Nomornya berupa angka yang dapat digunakan untuk identifikasi.

Format penomoran:  
\<nomor-kelompok-grup+kelompok-kerja\>\<nomor-famili\>\<nomor-species\>

* Tiga digit pertama nomor grup dan kelompok kerja.  
* Dua Digit berikutnya nomor kelompok kerja  
* Tiga digit berikutnya nomor dataset. Dimulai dengan no 001 per masing-masing dataset. Ditentukan penomorannya oleh kelompok kerja.  
* 4 digit berikutnya urutan species. Dimulai dengan 0001 per masing-masing famili  
    
  **Nomor Grup Kelompok Kerja**

| No identifikasi | Grup |
| :---- | :---- |
| 1 | Mikroba |
| 2 | Plantae |
| 3 | Insecta |
| 4 | Vertebrata |
| 5 | Animalia lainnya |


  **Nomor identifikasi kelompok kerja**


| No Identifikasi | Kelompok Kerja | idKK |
| :---- | :---- | :---- |
| **KK Mikroba** |  |  |
| 01 | Virus dan prokaryotes | 101 |
| 02 | Fungi | 102 |
| 03 | Algae | 103 |
| **KK Plantae** |  |  |
| 01 | Lumut | 201 |
| 02 | Pteridophytes | 202 |
| 03 | Spermatophyta | 203 |
| **KK Insecta** |  |  |
| 01 | Lepidoptera | 301 |
| 02 | Odonata | 302 |
| 03 | Coleoptera | 303 |
| 04 | Mantodea | 304 |
| 05 | Phasmida | 305 |
| 06 | Hemiptera | 306 |
| 07 | Hymenoptera | 307 |
| 08 | Orthoptera | 308 |
| **KK Vertebrata** |  |  |
| 01 | Pisces | 401 |
| 02 | Amphibia | 402 |
| 03 | Reptilia | 403 |
| 04 | Aves | 404 |
| 05 | Mammalia | 405 |
| **KK Animalia Lainnya** |  |  |
| 01 | Cnidaria | 501 |
| 02 | Porifera | 502 |
| 03 | Echinodermata | 503 |
| 04 | Plathyhelminthes | 504 |
| 05 | Mollusca | 505 |
| 06 | Annelida | 506 |
| 07 | Arachnida | 507 |
| 08 | Crustacea | 508 |
| 09 | Myriapoda | 509 |
| 10 | Nematoda | 510 |

## Pengisian Data Taksonomi

### **Pemakaian Bahasa**

* Nama famili, genus, dan spesies memakai nama latin sesuai standar taksonomi yang disetujui KK Kelompok Taksa dan diberitahukan ke Komite Inti.  
* Nama umum (common names) utama dalam Bahasa Inggris dan Bahasa Indonesia sesuai kesepakatan KK kelompok taksa jika belum ada standardisasi.    
* Bahasa Inggris menggunakan menggunakan Bahasa Inggris Amerika Serikat. Alasannya, untuk konsistensi dengan Bahasa Inggris komputer dan bahasa pemrograman. Bahasa Inggris Amerika Serikat juga merupakan Bahasa Inggris yang paling banyak dipakai di Indonesia. 

### **Format pengisian data**

* Nama file dan folder menggunakan snake\_case. Format awal cukup dengan format Google Sheets. Saat dirilis, dieksport menjadi CSV. Contoh penamaan file: mamalia\_indonesia.csv. Jika ada pembagian dataset, penamaan file menjadi \<kolompok-data\>\_\<KK\>\_indonesia.csv.   
* Nama kolom menggunakan lowercase untuk yang satu kata dan camelCase untuk yang lebih dari satu kata. Contohnya: id dan taxonRank  
* Untuk kolom yang isiannya dalam berbagai bahasa. Kolom dipisah dengan masing-masingnya diberi suffix underscore dan kode bahasa sesuai **ISO 639-1** ([https://www.loc.gov/standards/iso639-2/php/code\_list.php](https://www.loc.gov/standards/iso639-2/php/code\_list.php)). Contohnya untuk nama umum dalam bahasa Inggris mainCommonName\_EN dan versi bahasa Indonesia nya mainCommonName\_ID.  
* Sebagian bahasa, seperti Bahasa Inggris, memiliki berbagai versi negara penutur bahasa tersebut. Kolom yang berisi data dengan bahasa spesifik negara tertentu, penamaan kolom menggunakan kode bahasa dan negara: mainCommonName\_EN-US.   
* Daftar (*list*) dipisah menggunakan titik koma  “;” mengacu GBIF. Contohnya: Indonesia;Malaysia;Brunei.  
* Jika didalam daftarnya terdapat subdaftar (*sublist*). Subdaftar dipisah menggunakan tanda pipe berspasi “ | ”. Contohnya: stateProvince:Sumatra Barat | Jambi | Riau;city:Padang | Pekanbaru | Bukittinggi  
* Gunakan tanda pagar untuk pemisah identifikasi kata dalam subdaftar. Contohnya pada isian symbions: hasParasite:biodivina\#100011 | biodivina\#100012;eatenBy:biodivina\#10001 | biodivina\#10001.

### **Kolom dan terminologi data taksonomi**

**Catatan:** 

* Kolom dengan label berwarna kuning bisa diisi jika memungkinkan, tetapi belum menjadi prioritas untuk program Biodiv-INA Tahap I.   
* Tipe data SQL sesuai format database SQLite untuk aplikasi selain website. Untuk website, akan menyesuaikan dengan format Postgres jika dibutuhkan.   
* Contoh penggunaan secara umum. Diharapkan masing-masing KK kelompok taksa memiliki contoh penggunaan untuk kelompok taksa yang menjadi tanggung jawab KK tersebut.  
* Tipe data akan dilengkapi dengan bahasa pemrograman lain untuk memudahkan penulisan aplikasi pendamping.


| Nama Kolom | Deskripsi | Format pengisian | Contoh penggunaan | Terminologi Darwin Core | Tipe data Rust | Tipe data SQL |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| kkID | Nomor kelompok kerja . Kolom hanya untuk memudahkan pengurutan nomor identifikasi. | \<satu-digit-no-group-dan-dua-digit-no-kk\> | 405 |  |  |  |
| datasetID | Nomor dataset. Kolom hanya untuk memudahkan pengurutan nomor identifikasi. | \<nomor-identifikasi\> | 001 |  |  |  |
| speciesID | Nomor spesies. Kolom hanya untuk memudahkan pengurutan nomor identifikasi. | \<nomor-identifikasi\> | 0001 |  |  |  |
| id | Tidak diisi manual. Gunakan formula untuk menggabungkan semua nomor identifikasi. | `=CONCATENATE($A$2,TEXT(B2,"000"),TEXT(C2,"0000"))` | 4050010001 |  |  |  |
| taxonRank | Level taksonomi. Opsi selalu *species* untuk program tahap  I. Bisa dikembangkan jadi *subspecies* kedepannya. Penting diingat kata kuncinya dalam Bahasa Inggris. | \<kata-kunci-tingkatan-taksa\> | species |  |  |  |
| kingdom | Nama kingdom. Format sentence case | \<nama-kingdom\> | Animalia |  | String | TEXT |
| phylum | Nama filum | \<nama-filum\> | Chordata |  | String | TEXT |
| phyloGroup | Grup taksa dibawah phylum dan di atas ordo. Disesuaikan dengan filogeni masing-masing kelompok taksa. Digunakan dalam penyusunan taksa untuk visualisasi database. | \<nama-group\> | Placentalia |  |  |  |
| phyloGroupSort | Urutan grup berdasarkan pohon filogeni. | \<nomor-urut-filogenetika\> | 3 |  | usize | INTEGER |
| taxonClass | Nama kelas. Awalan taxon untuk menghindari konflik dengan kata kunci bahasa pemograman. Ditulis nama Bahasa Inggris. | \<nama-kelas\> | Mammalia |  |  |  |
| taxonOrder | Nama ordo. Awalan taxon untuk menghindari konflik dengan kata kunci bahasa pemograman. Divisualisasi menjadi order (EN) atau ordo (ID) setalah parsing.  | \<nama-ordo\> | Rodentia |  | String | TEXT |
| taxonFamily | Nama famili. Parsing seperti dengan taxonOrder. | \<nama-famili\> | Muridae |  | String | TEXT |
| genus | Name genus dengan format huruf regular (tidak ditulis miring). | \<nama-genus\> | Bunomys |  | String | TEXT |
| species | Nama species, termasuk genus dan epithet (nama penjelas): Rattus rattus. Ditulis dengan huruf biasa. | \<nama-genus\>\<spasi\>\<nama-penjelas\> | Bunomys coelestis |  | String | TEXT |
| speciesAuthorLastNames | Daftar belakang author yang deskripsi. Tulis sesuai kode internasional penamaan spesies, seperti ICZN, ICBN, dan ICNafp, | \<nama-belakang-author\> | Thomas |  | String | TEXT |
| speciesYear | Tahun deskripsi | \<tahun-deskripsi-taksa\> | 1896 |  | usize | INTEGER |
| authorityParentheses | Apakah menggunakan tanda kurung atau tidak. Opsi: TRUE atau FALSE | \<true-atau-false\> | TRUE |  | bool | INTEGER |
| taxonomicNotes\_EN-US | Catatan taksonomi (jika ada). Misalnya, studi menunjukkan spesies ini kemungkinan mengacu pada beberapa spesies atau sinomim dari spesies lain, namun status taksonominya masih ditetapkan dipisah. Bisa juga diisi dengan informasi mengenai catatan perubahan taksonomi. | \<catatan-dalam-bahasa-inggris\> |  |  |  |  |
| taxonomicNotes\_ID | Sama taxonomicNotes\_EN-US. Ditulis dalam Bahasa Indonesia. |  |  |  |  |  |
| recognitionBasedOn | Basis pendeskripsian species. Diisi dengan daftar opsi. Opsi: morphology, sangerDNA, genomicDNA, ecology. | \<kata-kunci-1\>\<titik koma\>\<kata-kunci-2\> | morphology;sangerDNA;genomicDNA |  |  |  |
| mainCommonName\_EN | Nama utama dalam Bahasa Inggris. Pilih dari opsi yang ada jika belum ditetapkan   | \<nama-utama\> | Lompobatang Hill Rat |  | String | TEXT |
| otherCommonName\_EN | Nama lainnya dalam Bahasa Inggris | \<nama-lainnya-1\>\<semi-colon\>\<nama-lainnya-2\>\<semi-colon\>\<dst\> | Heavenly Hill Rat;Lompobatang Bunomys |  | String | TEXT |
| commonNameNotes\_EN | Catatan mengenai nama umum dalam Bahasa Inggris. | \<catatan-dalam-bahasa-inggris\> |  |  |  |  |
| mainCommonName\_ID | Nama utama dalam Bahasa Indonesia. Pilih jika belum ditetapkan. Penulisan sesuai format KBBI. | \<nama-utama\> | Pangusan Lompobatang |  | String | TEXT |
| otherCommonName\_ID | Nama lainnya, termasuk nama daerah. Kosongkan jika tidak ada / tidak diketahui. Penulisan sesuai format Ejaan Bahasa Indonesia. | \<bahasa-1\>\<titik dua\>\<nama-1\>\<titik koma\<bahasa-2\>\<titik dua\>\<nama-2\> | minangkabau:mancik |  | String | TEXT |
| commonNameNotes\_ID | Catatan mengenai nama umum dalam Bahasa Indonesia. Tambahkan referensi jika ada. | \<catatan-dalam-bahasa-indonesia\>\<refrensi\>\<\[nomor-referensi\]\> | Nama Bahasa Indonesia sesuai Maryanto et al. 2019 \[1\] |  | String | TEXT |
| typeCountryHost | Lokasi penyimpanan spesimen tipe. | \<type\>\<titik dua\>\<nama-negara\>\<titik koma\>\<tipe lainnya\>\<nama-negara\> | holotype:United Kingdom;paratype:Indonesia |  | String | TEXT |
| typeInstitution | Nama institusi tempat penyimpanan spesimen tipe. Sesuai nama di negara institusi tersebut. | \<type\>\<titik dua\>\<nama-institusi\>\<titik koma\>\<tipe lainnya\>\<nama-institusi\> | holotype:The British Museum of Natural History;paratype:Museum Zoologicum Bogoriense |  |  |  |
| typeInstitutionID | Kode institusi penyimpanan specimen tipe | \<type\>\<titik dua\>\<kode-institusi\> | holotype:BMNH;paratype:MZB |  | String | TEXT |
| typeVoucher | Nomor koleksi spesimen tipe. | \<type\>\<titik dua\>\<nomor-koleksi\> | holotype:Mamm:1897.1.3.12;paratype:32244 |  | String | TEXT |
| verbatimTypeLocality | Lokasi penemuan spesimen tipe sesuai publikasi deskripsi spesies (jika berbeda dengan nama saat ini). Jika sama, masukkan data di typeLocality. Tambahkan ketinggian jika tidak dalam meter. | \<type\>\<titik dua\>\<nama-lokasi-sesuai publikasi\>\<titik koma\>\<tipe lainnya\>\<nama-lokasi-sesuai publikasi\> | holotype:Bonthain Peak, 6000 ft, south-western Sulawesi, Indonesia;paratype: |  | String | TEXT |
| typeLocality | Lokasi penemuan spesimen tipe sesuai nama lokasi sekarang. Gunakan penamaan sesuai negara asal spesimen tanpa penunjuk administrasi. Untuk program ini dalam Bahasa Indonesia. Misalnya, tulis Sulawesi Selatan, bukan Provinsi Sulawesi Selatan atau South Sulawesi. | \<type\>\<titik dua\>\<nama-lokasi\>\<titik koma\>\<tipe lainnya\>\<nama-lokasi\> | holotype:Gunung Lompobatang, Sulawesi Selatan, Indonesia. |  |  |  |
| typeLocalityLatitude | Koordinat latitudinal spesimen tipe. Isi apa adanya sesuai publikasi. Visualisasi di parsing jadi dua jika koordinat tidak desimal: verbatim (sesuai publikasi) dan desimal (hasil konversi). Kosongkan jika tidak diketahui. | \<type\>\<titik dua\>\<koordinat\>\<titik koma\>\<tipe lainnya\>\<koordinat\> |  |  | f32 | REAL |
| typeLocalityLongitude | Koordinat longitudinal. Diparsing seperti typeLocalityLatitude. Kosongkan jika tidak diketahui. | \<type\>\<titik dua\>\<koordinat\>\<titik koma\>\<tipe lainnya\>\<koordinat\> |  |  | f32 | REAL |
| typeLocalityElevationInMeters | Ketinggian lokasi penemuan dalam meter. Ditulis angka saja tanpa unitnya. Untuk biota daratan. Kosongkan jika tidak ada.  | \<type\>\<titik dua\>\<ketinggian-lokasi-dalam-meter\>\<titik koma\>\<tipe lainnya\>\<ketinggian-lokasi-dalam-meter\> | holotype:1830;paratype:1900 |  | usize | INTEGER |
| typeLocalityDepthInMeters | Kedalaman lokasi penemuan spesimen tipe dalam meter. Untuk biota akuatik. Kosongkan jika tidak ada. | \<type\>\<titik dua\>\<kedalaman-lokasi-dalam-meter\> |  |  |  |  |
| originalNameAsDescribed | Nama sesuai deskripsi pertama.  | \<genus\>\<spasi\>\<spesies\> | Mus coelestis |  |  |  |
| synonymsWithAuthorYears | Daftar synonyms. Lengkap dengan author, tahunnya, dan referensi artikel ilmiah. Kosongkan jika tidak ada. | \<genus\>\<spasi\>\<species\>\<spasi\<penulis\>\<spasi\>\<tahun\> |  |  | String | TEXT |
| countryDistribution | Negara distribusi species. Gunakan titik koma sebagai tanda pemisah jika terdistribusi di beberapa negara. | \<negara-1\>\<titik koma\>\<negara-2\> | Indonesia;Malaysia |  | String | TEXT |
| ecoregion | Distribusi berdasarkan ekoregion. Butuh tambahan untuk biota laut. Opsi: island, islandGroup, areaOfEndemism, other. | \<kode-ekoregion\>\<titik dua\>\<nama-ekoregion\> | island:Sulawesi;aOE:South West Sulawesi |  | String | TEXT |
| nativeLocalDistribution\_ID | Distribusi asli berdasarkan batas administratif. Berguna untuk pengambil kebijakan konservasi. Level administrasi disesuaikan dengan tingkatkan wilayah Indonesia. | \<level-administrasi\>\<titik dua\>\<distribusi-1\>\<tanda | \>\<distribusi-2\>\<titik koma\> \<level-administrasi-2\>\<titik dua\>\<distribusi-1\>\<tanda | \>\<distribusi-2\> | kabupaten:Bantaeng;kecamatan:Parigi | Sinjai Barat | Kindang | Rumbia |  | Vector\<String\> | TEXT |
| introducedLocalDistribution\_ID | Distribusi introduksi berdasarkan batas administratif. Opsi sama dengan nativeLocalDistribution\_ID. Kosongkan jika bukan spesies introduksi. | \<level-administrasi\>\<titik dua\>\<distribusi-1\>\<tanda | \>\<distribusi-2\>\<titik koma\>\<level-administrasi-2\>\<titik dua\>\<distribusi-1\>\<tanda | \>\<distribusi-2\> |  |  | Vector\<String\> | TEXT |
| distributionStatus | Status distribusi spesies: native, partlyIntroduced, fullyIntroduced.  | \<kode-status-distribusi\> | native |  | Enum | TEXT |
| distributionNotes\_EN-US | Catatan distribusi dalam American English. Referensi tulis dalam brackets (tanda kurung besar). Contohnya \[1\]. Sesuaikan dengan list di referenceNameLinks | \<catatan-distribusi\> | The species is known only from a single mountain range, Lompobatang-Bawakareng, in the southwestern peninsula of Sulawesi.\[1\]  |  | String | TEXT |
| distributionNotes\_ID | Catatan distribusi dalam Bahasa Indonesia. Penulisan referensi seperti distributionNotes\_EN-US. | \<catatan-distribusi\> | Spesies ini hanya diketahui terdistribusi di pegunungan Lompobatang-Bawakaraeng di bagian semenanjung barat daya pulau Sulawesi. |  | String | TEXT |
| keyCharacters\_EN-US | Karakter utama spesies untuk membedakan dengan spesies berdekatan. | \<catatan-karakter-utama\> | Medium size rats (\~100g). The tail is short or the same length as the head and body. |  | String | TEXT |
| keyCharacters\_ID | Karakter utama dalam Bahasa Indonesia | \<catatan-karakter-utama\> | Tikus berukuran sedang (\~100g). Ekor lebih pendek dari kepala-badan atau sama panjang dengan kepala-badan. |  |  |  |
| characterNotes\_EN-US | Catatan tambahan mengenai karakter taksa. | \<catatan-tambahan\> | Other recognized species of Bunomys have bigger body size. |  | String | TEXT |
| characterNotes\_ID | Catatan tambahan dalam Bahasa Indonesia | \<catatan-tambahan\> | Spesies Bunomys lainnya umumnya  |  |  |  |
| habitatNotes\_EN-US | Catatan mengenai habitat distribusi taksa. | \<catatan-habitat\> | Typically found in the mountain forest of Lompobatang-Bawakaraeng. |  | String | TEXT |
| habitatNotes\_ID | Catatan mengenai habitat dalam Bahasa Indonesia | \<catatan-habitat\> | Umumnya ditemukan di hutan pegunungan di kawasan Lompobatang-Bawakaraeng. |  |  |  |
| additionalNotes\_EN-US | Catatan tambahan dalam Bahasa Inggris. Bisa diisi dengan informasi taksonomi terbaru, kekerabatan filegenetika, dan lain-lain. Lengkapi dengan referensi artikel ilmiah. Kosongkan jika tidak ada catatan tambahan. | \<catatan-tambahan\> |  |  |  |  |
| additionalNotes\_ID | Catatan tambahan dalam Bahasa Indonesia. Diisi seperti additionalNotes\_EN-US. | \<catatan-tambahan\> |  |  |  |  |
| iucnStatus | Kategori IUCN Red List diisi dalam format dua huruf standar IUCN. Opsi: EX, EW, CR, EN, VU, NT, LC, DD, NE.  | \<kategori-iucn\> | EN |  | Enum | TEXT |
| citesStatus | Status apendik CITES. Opsi: 1, 2, 3\. Kosongkan jika tidak dievaluasi. | \<kategori-cites\> |  |  | Enum | INTEGER |
| countryStatus | Status konservasi di negara asal takson lengkap dengan translasi dalam Bahasa Inggris. | \<negara\>\<titik dua\>\<status\>\<spasi\>\<buka kurung\>\<translasi Bahasa Inggris\>\<tutup kurung\> | Indonesia:Tidak dilindungi (unprotected);Malaysia: |  | String | TEXT |
| countryStatusReference | Referensi undang-undang mengenai status takson. | \<negara\>\<titik dua\>\<undang-undang\> |  |  |  |  |
| symbionts | Interaksi spesies dengan spesies lainnya. Data ini akan ditautkan dengan informasi taksa simbiotik-nya. Opsi: hasParasite, hostOf, preyedUponBy, eatenBy, eats. Kosongkan jika tidak diketahui. | \<kode-interaksi\>\<titik dua\>\<provider\>\<tanda pagar\>\<nomor-identifikasi\> | hasParasite:biodivina\#40100011 | biodivina\#100012;eatenBy:biodivina\#10001 | biodivina\#10001 |  | String | TEXT |
| symbiontNotes\_EN-US | Catatan interaksi dalam Bahasa Inggris. Lengkapi dengan referensi artikel ilmiah. Kosongkan jika tidak ada. | \<catatan interaksi\> | Parasite interaction was first described by Winterhoff et al. \[2\]. |  |  |  |
| symbiontNotes\_ID | Catatan interaksi dalam Bahasa Indonesia. Diisi sesuai symbionNotes\_EN-US. | \<catatan interaksi\> | Interaksi parasit pertama kali dideskripsikan oleh Winterhoff et al. \[2\] |  |  |  |
| referenceLinks | Referensi taksa. List berdasarkan urutan penggunaan. Penulisan nomor urutan dan link referensi. Utamakan berupa DOI. Jika tidak ada, gunakan tautan asli. | \<\[urutan\]\>\<spasi\>\<link\> | \[1\] [https://doi.org/10.1645/19-136](https://doi.org/10.1645/19-136) \[2\]  |  | String | TEXT |
| externalTaxonIdentifiers | Nomor identitas data taksonomi eksternal. Hanya untuk database yang dikenali. Lihat dibawah untuk opsinya. Diluar opsi ini gunakan externalLinks. | \<provider-1\>\<titik dua\>\<identifier-1\>\<titik koma\>\<provider-2\>\<titik dua\>\<identifier-2\> | mdd:1003513; ncbi:txid2606483 |  | Vector\<String\> | TEXT |
| externalLinks | Tautan lainnya yang tidak termasuk identitas taksonomi maupun referensi. Disediakan untuk link yang tidak memiliki takson identifier dan tautan permanen. | \<link-1\>\<titik koma\>\<link-2\> | https://www.iucnredlist.org/species/3329/22451992; |  | Vector\<String\> | TEXT |
| associatedData | Tipe data dan nomor identifikasi menggunakan sumber sendiri. File-nya satu paket dengan data taksa. Opsi: video, audio, photo, illustration, geoJSON. Kosongkan jika tidak ada. | \<tipe-data\>\<titik dua\>\<nomor-identifikasi\> |  |  | String | TEXT |
| externalAssociatedDataLinks | Data dari sumber eksternal. Pastikan kesepakatan copyright sebelum menggunakan. Opsi seperti associatedData | \<tipe-data-1\>\<titik dua\>\<copyright-1\> | \<links-1\>;\<tipe-data-1\>\<titik dua\>\<copyright-2\> | \<links-2\> | photo: |  | String | TEXT |
| contributorNameOrcid | Daftar nama kontributor dan ORCID-nya. | \<nama-kontributor-1\>\<titik dua\>\<ORCID-1\>\<titik koma\>\<nama-kontributor-2\>\<titik dua\>\<ORCID-2\> | Heru Handika:0000-0002-2834-7175 |  | String | TEXT |

## Daftar Kata Kunci Data Taksa

**Specimen Type**  
Digunakan untuk kolom type: **typeCountryHost**, **typeInstitution**, **typeInstitutionID**, **typeVoucher**, **verbatimTypeLocality**

| Kata kunci | Keterangan |
| :---- | :---- |
| holotype | Spesimen tunggal yang ditetapkan sebagai rujukan dalam deskripsi asli suatu spesies. |
| paratype | Spesimen lain yang dicantum dalam deskripsi suatu spesies sebagai pendamping spesimen holotipe. Bisa satu atau lebih dari satu individu. |
| allotype | Spesimen tipe rujukan yang memiliki kelamin berbeda dengan holotipe. Diambil dari paratipe. Kadang juga digunakan sebagai spesimen acuan yang karakternya tidak terdapat di spesimen tipe. |
| neotype | Spesimen tunggal yang ditetapkan belakangan sebagai rujukan dalam deskripsi suatu spesies. Biasanya karena deskripsi asli tidak memiliki holotipe, holotipe hilang, atau rusak. |
| syntype | Semua spesimen yang dijadikan rujukan dalam deskripsi suatu spesies. Semua kedudukan spesimen ini sama karena tidak ada penyebutan holotipe dalam deskripsi spesies tersebut. |
| lectotype | Spesimen tunggal yang dipilih belakangan dari daftar spesimen tipe untuk dijadikan spesimen acuan. Kedudukannya menjadi seperti holotipe. |
| paralectotype | Spesimen lainnya yang dipilih belakangan dari daftar spesimen tipe. Kedudukannya mirip seperti paratipe. |
| isotype | Biasanya dipakai di botani. Merujuk kepada duplikat dari spesimen holotipe. |

**ecoregion**  
Silahkan ditambahkan untuk ekoregion biota laut.

| Kata kunci | Keterangan | Contoh data |
| :---- | :---- | :---- |
| realm | Wilayah biogeografi | realm:Indomalaya;Australasia |
| island | Untuk isian pulau. | island:Sumatera;Jawa; Kalimantan |
| islandGroup | Kelompok/gugusan pulau.  | islandGroup:Maluku;Mentawai |
|  aOE | Area of endemism atau kawasan endemik. Sulawesi misalnya memiliki tujuh daerah endemik. Digunakan untuk biota tertentu yang distribusinya terbatas di kawasan endemik. | areaOfEndemism:North-East Sulawesi |

### **externalTaxonIdentifiers**

Silahkan tambahkan kata kunci database lain yang punya tautan permanen.

| Kata kunci | Keterangan | Link |
| :---- | :---- | :---- |
| mdd | Mammal Diversity Database. Salah satu database mamalia yang banyak dipakai. | https://www.mammaldiversity.org/ |
| ncbi | National Center for Biotechnology Information. Database sekuen genetik paling umum dipakai. | https://www.ncbi.nlm.nih.gov/ |
| aw | Amphibia Web. Salah satu database amfibi yang banyak dipakai | https://amphibiaweb.org/ |
| asw | Amphibian Species of the World. Salah satu database amfibi yang banyak dipakai | https://amphibiansoftheworld.amnh.org/ |
| rd | Reptile Database: database taksonomi reptil (Reptilia) | https://reptile-database.reptarium.cz/ |
| wsc | World Spider Catalog: database taksonomi laba-laba (Araneae) | https://wsc.nmbe.ch/ |
| wac | World Arachnid Catalog: database taksonomi untuk ordo arakhnida selain Araneae, Scorpiones, Opiliones, Acariformes, Parasitiformes, dan Xiphosura | https://wac.nmbe.ch/ |
| wco | World Catalogue of Opiliones: database taksonomi laba-laba penuai (Opiliones) | https://www.wcolite.com/ |
| powo | Plants of the World Online: database taksonomi tumbuhan vaskuler (Tracheophyta) | https://powo.science.kew.org/ |
| wf | World Ferns/Checklist of Ferns and Lycophytes of the World: database taksonomi tumbuhan pakis (Polypodiopsida) | https://www.worldplants.de/world-ferns/ferns-and-lycophytes-list |
| cb | Chilobase: database taksonomi lipan (Chilopoda) | https://chilobase.biologia.unipd.it/ |
| mb | Millibase: database taksonomi kaki seribu (Diplopoda) | https://millibase.org/ |
| worms | World Register of Marine Species: database taksonomi hewan laut | https://www.marinespecies.org/ |
| psf | Phasmida Species File: database taksonomi serangga tongkat (Phasmida) | https://phasmida.speciesfile.org/ |
| msf | Mantodea Species File: database taksonomi belalang sembah (Mantodea) | http://mantodea.speciesfile.org |
| osf | Orthoptera Species File: database taksonomi Orthoptera | https://orthoptera.speciesfile.org/ |
| fb | FishBase: database taksonomi dan ekologi ikan (Pisces) | https://www.fishbase.us/ |
| birdlf | HBW / BirdLife Taxonomic Checklist: database taksonomi burung  | https://avibase.bsc-eoc.org/checklist.jsp?lang=EN |
| ioc | The IOC World Bird List: database taksonomi burung | https://www.worldbirdnames.org/new/ |

## Mobilisasi data

### **Pengisian data**

Data diisi ke Google Spreadsheet yang di-host ISES. Selanjutnya, data yang sudah ready di taruh di GitHub. Detail nya akan dijelaskan di skema mobilisasi data. 

### **Pemaketan Data**

#### Konten Paket

Human readable CSV  
Machine readable JSON  
Metadata YAML  
Foto: WEBP (Konversi menggunakan parser)  
GitHub Release format: TAR.GZ (TBD. Butuh uji rasio kompresi terbaik)

### **Skema Mobilisasi Data**

Data di Google Spreadsheet dikelola masing-masing KK Kurasi Data. Kemudian data yang sudah siap untuk dirilis ditaruh di GitHub repository Biodiv-INA. Masing kelompok taksa akan memiliki repository tersendiri. Data GitHub dikelola KK Kurasi Data bekerja sama dengan KK Teknologi Informasi dan Komite Inti. Data dirilis secara berkala dengan skema penomoran Semantic Versioning Versi 2 (SemVer V2, https://semver.org/). Skema ini memungkinkan perubahan data kita terstruktur, dapat diprediksi, dan bisa ditelusuri. Skema ini jamak digunakan dalam pengembangan perangkat lunak.

Secara umum format SemVer v2: \<major\>.\<minor\>.\<patch\>. Untuk rilis pertama merupakan versi 1.0.0. Nomor major ditingkatkan jika terjadi perubahan signifikan di datanya. Misalnya, data yang sekarang berisi data taksonomi murni, ditingkatkan dengan data karakter untuk menjadi panduan lapangan. Versinya akan menjadi 2.0.0. Untuk revisi spesies, maka penomoran yang ditingkatkan nomor minor. Misalnya dari v1.0.0 menjadi v1.1.0. Nomor patch ditingkatkan untuk revisi kecil, misalnya perbaikan typo, kesalahan isian data, dsb. Nomor v1.0.0 akan menjadi v1.0.1

Setiap rilis data, Git repository-nya akan ditandai dengan tag, contohnya git tag v1.0.0. Kita akan kembangkan GitHub Action script yang akan otomatis memaketkan datanya dan dirilis ke halaman rilis GitHub. Kita juga akan menyiapkan repository khusus yang berisi metadata semua data taksa. Aplikasi akan mengindeks repository ini untuk mengetahui data apa saja yang tersedia. Informasi ketersediaan update data akan diketahui dari perubahan versi di halaman rilis GitHub.

## Geographic Information System (GIS) 

Target awal kita bisa menyiapkan poligon ekoregion dalam format GeoJSON.

MAP: [https://gadm.org/about.html](https://gadm.org/about.html)  
Rust crates: [https://georust.org/](https://georust.org/)

## Referensi

[https://www.legumedata.org/](https://www.legumedata.org/)  
[https://www.mammaldiversity.org/](https://www.mammaldiversity.org/)  
[https://www.fishbase.org.au/v4](https://www.fishbase.org.au/v4)  
[https://amphibiaweb.org/](https://amphibiaweb.org/)  
[https://wsc.nmbe.ch/](https://wsc.nmbe.ch/)  
[Occurrence download formats :: Technical Documentation (gbif.org)](https://techdocs.gbif.org/en/data-use/download-formats)  
[New Zealand Organisms Register (nzor.org.nz)](https://www.nzor.org.nz/)  
[https://www.globalbioticinteractions.org/](https://www.globalbioticinteractions.org/)

