---
description: fungsi dan tugas dasar token NIFTSY
---

# ARSITEKTUR PROYEK DAN PERAN TOKEN

Jadi, Arsitektur Proyek adalah sebagai berikut:

![](<../../.gitbook/assets/Снимок экрана 2022-02-05 в 11.17.58.png>)

Penting untuk memperhatikan prinsip-prinsip pembentukan model berikut:

1. Tautan antara Protokol - Oracle - Indeks awalnya dibentuk dari bawah ke atas, tetapi kemudian Proyek bekerja dari ketiga elemen tersebut.
2. Oracle dan Indeks dapat dibuat di luar Proyek, Protokol tidak.
3. Ketiga entitas didasarkan pada model reputasi transaksional primitif, yaitu mereka mempertimbangkan a) kuantitatif; b) sementara; c) kriteria subjektif.
4. Semua elemen beroperasi atas dasar keterbukaan, desentralisasi dan mempertimbangkan semua entitas sebagai aktor yang mungkin dalam Proyek: skrip, AI, pengguna, dll.
5. Ketiga entitas berinteraksi satu sama lain melalui fungsi Token, yang merupakan elemen penting dari ekosistem Proyek.

Fitur Token dibahas secara lebih rinci di bawah ini.
