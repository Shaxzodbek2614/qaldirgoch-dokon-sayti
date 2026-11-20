# "Qaldirg'och" maishiy texnika do'koni — onlayn do'kon rejasi

> Hozirgi bosqich: faqat **HTML, CSS, JavaScript** (frontend).
> Backend keyinroq qo'shiladi.

---

## 1. Sayt kim uchun va nima uchun

Sayt "Qaldirg'och" do'konining xaridorlari uchun. Ular uydan chiqmasdan maishiy texnikani ko'rib chiqishi, solishtirishi va buyurtma berishi mumkin bo'ladi.
Do'kon uchun sayt mahsulotlarni bir joyda ko'rsatadi va buyurtmalarni onlayn qabul qilish imkonini beradi.

---

## 2. Sahifalar

| № | Fayl | Sahifa | Nima bo'ladi |
|---|------|--------|--------------|
| 1 | `index.html` | Bosh sahifa | Header (logo, menyu, qidiruv, savat belgisi), banner, asosiy kategoriyalar (muzlatkich, kir yuvish mashinasi, konditsioner, televizor, mayda texnika va h.k.), "Yangi kelganlar" va "Chegirmadagilar" bloklari, footer |
| 2 | `catalog.html` | Katalog | Barcha mahsulotlar kartochka ko'rinishida; kategoriya, brend va narx oralig'i bo'yicha filtr; saralash (arzon → qimmat, qimmat → arzon, yangi); qidiruv natijalari ham shu sahifada |
| 3 | `product.html?id=...` | Mahsulot sahifasi | Rasmlar galereyasi, nomi, brend, model, narx, mavjudligi, kafolat, tavsif, texnik xususiyatlar jadvali, soni tanlanadi, "Savatga qo'shish" tugmasi, o'xshash mahsulotlar |
| 4 | `cart.html` | Savat | Tanlangan mahsulotlar ro'yxati, sonini o'zgartirish, o'chirish, umumiy summa, "Buyurtma berish" tugmasi |
| 5 | `checkout.html` | Buyurtma berish | Forma: ism, telefon, yetkazib berish yoki do'kondan olib ketish, manzil, izoh; buyurtma xulosasi; tasdiqlash xabari |
| 6 | `about.html` | Biz haqimizda | Do'kon haqida qisqacha ma'lumot, afzalliklar (kafolat, yetkazib berish va h.k. — do'kondan aniqlanadi) |
| 7 | `contact.html` | Aloqa | Manzil, telefon, ish vaqti, xarita — **barchasi do'kondan olinadi**, hozircha bo'sh joy qoldiriladi |
| 8 | `404.html` | Topilmadi | "Sahifa topilmadi" xabari va bosh sahifaga havola |

**Barcha sahifalarda umumiy:** header, footer, savatdagi mahsulotlar soni belgisi.

---

## 3. Bitta mahsulot haqidagi ma'lumotlar

| Maydon | Turi | Izoh |
|--------|------|------|
| `id` | son | Takrorlanmas raqam |
| `nomi` | matn | Masalan: "Muzlatkich ..." |
| `kategoriya` | matn | muzlatkich, kir-yuvish, konditsioner, televizor, ... |
| `brend` | matn | Ishlab chiqaruvchi |
| `model` | matn | Model kodi |
| `narx` | son | So'mda, faqat raqam (formatlash JS'da) |
| `eskiNarx` | son / `null` | Chegirma bo'lsa — avvalgi narx |
| `rasmlar` | matnlar ro'yxati | Rasm fayllari yo'llari, birinchisi asosiy rasm |
| `qisqaTavsif` | matn | Kartochkada ko'rinadigan 1–2 gap |
| `tavsif` | matn | To'liq tavsif |
| `xususiyatlar` | obyekt | Kalit–qiymat: quvvat, hajm, o'lcham, rang, energiya sinfi, ... |
| `kafolat` | son | Kafolat muddati (oyda) |
| `omborda` | son | Mavjud soni (`0` = tugagan) |
| `yangi` | mantiqiy | "Yangi" belgisi uchun |
| `qoshilganSana` | sana | Saralash uchun |

**Namuna (qiymatlar — bo'sh joylar, haqiqiy ma'lumot do'kondan olinadi):**

```js
{
  id: 1,
  nomi: "[MAHSULOT NOMI]",
  kategoriya: "muzlatkich",
  brend: "[BREND]",
  model: "[MODEL]",
  narx: null,        // do'kondan olinadi
  eskiNarx: null,
  rasmlar: ["images/products/1-1.jpg"],
  qisqaTavsif: "[QISQA TAVSIF]",
  tavsif: "[TO'LIQ TAVSIF]",
  xususiyatlar: {
    "Hajmi": "[...]",
    "Rangi": "[...]",
    "Energiya sinfi": "[...]"
  },
  kafolat: null,
  omborda: 0,
  yangi: true,
  qoshilganSana: "YYYY-MM-DD"
}
```

**Savatdagi element** (localStorage'da saqlanadi): `{ id, soni }` — qolgan ma'lumot `id` orqali mahsulotlar ro'yxatidan olinadi.

---

## 4. Bosqichlar

### 0-bosqich — Tayyorgarlik
- Papka tuzilmasi:
  ```
  qaldirgoch/
  ├── index.html, catalog.html, product.html, cart.html,
  │   checkout.html, about.html, contact.html, 404.html
  ├── css/      style.css
  ├── js/       data.js, main.js, catalog.js, product.js, cart.js, checkout.js
  └── images/   logo, banner, products/
  ```
- Git repozitoriy ochish, birinchi commit.

### 1-bosqich — HTML skelet
- Barcha sahifalarni semantik teglar bilan yozish (`header`, `nav`, `main`, `section`, `footer`).
- Mahsulotlar hozircha qo'lda yozilgan 2–3 ta kartochka.
- Sahifalar orasidagi havolalar ishlashi.

### 2-bosqich — CSS
- Umumiy uslub: ranglar, shriftlar, CSS o'zgaruvchilari (`:root`).
- Header, footer, kartochka, tugma, forma komponentlari.
- Flexbox / Grid bilan joylashuv.
- Responsive: telefon, planshet, kompyuter (media query).

### 3-bosqich — JavaScript: ma'lumotlar va chizish
- `data.js` — mahsulotlar massivi (3-bo'limdagi tuzilma bo'yicha).
- Bosh sahifa va katalogdagi kartochkalarni JS orqali chizish.
- Narxni chiroyli formatlash funksiyasi.

### 4-bosqich — Qidiruv, filtr, saralash
- Nomi bo'yicha qidiruv.
- Kategoriya, brend, narx oralig'i filtri.
- Saralash.
- "Hech narsa topilmadi" holati.

### 5-bosqich — Mahsulot sahifasi
- URL'dan `id` ni o'qish (`URLSearchParams`).
- Ma'lumotni topib chizish, rasm galereyasi.
- Mahsulot topilmasa — xabar yoki 404 ga yo'naltirish.
- O'xshash mahsulotlar (shu kategoriyadan).

### 6-bosqich — Savat
- Savatga qo'shish, sonini o'zgartirish, o'chirish.
- `localStorage` da saqlash (sahifa yangilansa ham yo'qolmaydi).
- Headerdagi savat belgisini yangilash.
- Umumiy summani hisoblash; `omborda` dan ko'p qo'shib bo'lmasligi.

### 7-bosqich — Buyurtma berish
- Forma va validatsiya (ism, telefon formati, majburiy maydonlar).
- Hozircha buyurtma `localStorage` ga / konsolga yoziladi.
- Tasdiqlash xabari, savatni tozalash.

### 8-bosqich — Sayqal va joylash
- Accessibility: `alt` matnlar, klaviatura bilan ishlash, kontrast.
- Turli brauzer va qurilmalarda tekshirish.
- Rasmlarni siqish, kodni tozalash.
- GitHub Pages'ga joylash.

### 9-bosqich — Backend (keyinroq)
- Mahsulotlar va buyurtmalar uchun API.
- `data.js` o'rniga `fetch()` orqali API'dan olish.
- Buyurtmalarni bazada saqlash, do'konga xabar yuborish (masalan, Telegram).
- Admin panel: mahsulot qo'shish, tahrirlash, buyurtmalarni ko'rish.

---

## Do'kondan olinadigan ma'lumotlar

Quyidagilar **o'ylab topilmaydi** — do'kon egasidan so'raladi:

- [ ] Mahsulotlar ro'yxati, narxlari va rasmlari
- [ ] Do'kon manzili va ish vaqti
- [ ] Telefon raqami(lari) va ijtimoiy tarmoqlar
- [ ] Logotip va brend ranglari
- [ ] Yetkazib berish shartlari
- [ ] To'lov usullari
- [ ] Kafolat shartlari