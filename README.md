<p align="center">
  <a href="https://devsponsors.github.io">
    <img src="https://devsponsors.github.io/assets/badges/sponsor.svg" alt="DevSponsors Badge">
  </a>
</p>

<!-- DevSponsors Badges -->
<p align="center">
  <a href="https://devsponsors.github.io"><img src="https://img.shields.io/badge/DevSponsors-Verified_OSS-6366f1?style=for-the-badge&logo=github" alt="DevSponsors Verified"></a>
  <a href="https://devsponsors.github.io"><img src="https://img.shields.io/badge/Sponsor-DevSponsors_Hub-emerald?style=for-the-badge&logo=github-sponsors" alt="DevSponsors Sponsor"></a>
  <a href="https://devsponsors.github.io/mediakit.html"><img src="https://img.shields.io/badge/Infrastructure-DevSponsors_Cloud-ec4899?style=for-the-badge&logo=server" alt="DevSponsors Cloud"></a>
</p>

# Iran Open Cafe & Screening Venues Data API
دیتابیس آزاد و جامع کافه‌ها، سالن‌های اکران و ایونت‌روم‌های ایران با بیش از ۱۹,۸۰۰ کافه و ۵,۷۰۰ مکان دارای ویدیو پروژکتور، منوی آنلاین دیجیتال، شماره تماس و اطلاعات اینستاگرام.

طراحی شده برای استفاده آسان، سریع و بدون نیاز به کلید دسترسی (Free Public API / Zero-Auth / CORS-Enabled) در کلیه پروژه‌های وب، موبایل، فریمورک‌های ری‌اکت، ویو، پایتون و ابزارهای تحلیلی.

🔗 **وب‌سایت آنلاین:** [https://m4tinbeigi-official.github.io/CafeBloggers.github.io/](https://m4tinbeigi-official.github.io/CafeBloggers.github.io/)  
👥 **لینک گروه تلگرامی جامعه کافه:** [https://t.me/+zBvYCfwduwE5MzI0](https://t.me/+zBvYCfwduwE5MzI0)

---

## 🌐 اندپوئینت‌های آماده (Live REST Endpoints)

آدرس پایه (Base URL):
`https://m4tinbeigi-official.github.io/CafeBloggers.github.io/api/v1`

| اندپوئینت | نوع خروجی | کاربرد | حجم تقریبی |
| :--- | :--- | :--- | :--- |
| `/projector-cafes.json` | JSON | تمامی کافه‌های دارای پروژکتور و پرده اکران (با شماره تماس، اینستاگرام، اولویت و سیستم پخش) | ۴.۴ مگابایت |
| `/projector-cafes.csv` | CSV (UTF-8 BOM) | دانلود مستقیم برای اکسل، گوگل شیت یا تحلیل پایتون/پانداس | ۲.۷ مگابایت |
| `/cities.json` | JSON | ایندکس تفکیک شهرها به همراه تعداد کافه‌ها و آدرس اندپوئینت اختصاصی | ۱۵ کیلوبایت |
| `/cities/{city_slug}.json` | JSON | دیتای کامل کافه‌های یک شهر خاص (مانند `tehran.json`, `mashhad.json`, `isfahan.json`, `shiraz.json`) | ۵۰ تا ۴۰۰۰ کیلوبایت |
| `/all-cafes.min.json` | JSON (Minified) | دیتابیس کل ۱۹,۸۰۰ کافه ایران با آدرس دقیق و شماره تلفن‌ها | ۱۱ مگابایت |
| `/stats.json` | JSON | متادیتا و آخرین وضعیت به‌روزرسانی دیتابیس | ۱ کیلوبایت |

---

## 💻 نحوه استفاده در پروژه‌ها (Code Snippets)

### ۱. جاوا اسکریپت / مرورگر (Fetch API / React / Vue)
```javascript
// دریافت سریع لیست کافه‌های دارای پروژکتور
fetch('https://m4tinbeigi-official.github.io/CafeBloggers.github.io/api/v1/projector-cafes.json')
  .then(res => res.json())
  .then(cafes => {
    console.log(`Loaded ${cafes.length} screening venues`);
    cafes.forEach(c => {
      console.log(c.name, c.city, c.telephone, c.instagram, c.menu_url);
    });
  });
```

### ۲. پایتون (Requests / Pandas)
```python
import pandas as pd

# خواندن مستقیم فایل CSV بدون نیاز به ذخیره محلی
url = 'https://m4tinbeigi-official.github.io/CafeBloggers.github.io/api/v1/projector-cafes.csv'
df = pd.read_csv(url)

# فیلتر کافه‌های دارای منوی آنلاین و شماره تماس در تهران
tehran_cafes = df[(df['city'] == 'تهران') & df['menu_url'].notna() & df['telephone'].notna()]
print(tehran_cafes[['name', 'telephone', 'instagram', 'menu_url']].head())
```

### ۳. دریافت کافه‌های یک شهر خاص (مثلاً اصفهان یا مشهد)
```bash
curl -s "https://m4tinbeigi-official.github.io/CafeBloggers.github.io/api/v1/cities/isfahan.json" | jq '.[0:5]'
```

---

## 📋 ساختار آبجکت داده (Schema Fields)

هر کافه در فایل‌های JSON دارای کلیدهای زیر است:

```json
{
  "id": 18,
  "name": "کافه سینما باغ فردوس",
  "city": "تهران",
  "province": "تهران",
  "district": "تجریش",
  "address": "خیابان ولیعصر، نرسیده به میدان تجریش، باغ فردوس",
  "telephone": "02122756531",
  "instagram": "@cinemacafe.ir",
  "website": "https://cinemacafe.ir",
  "menu_url": "https://menudigital.ir/cinemacafe",
  "has_projector": 1,
  "projector_priority": 1,
  "screening_type": "فیلم و سینمایی، نقد فیلم، فوتبال",
  "screen_hardware": "Epson EB-2250U Full HD",
  "capacity": 75,
  "rating": 4.6,
  "rating_count": 890,
  "working_hours": "09:00 - 23:30",
  "latitude": 35.8034,
  "longitude": 51.4241,
  "map_url": "https://balad.ir/p/..."
}
```

---

## 🛠 منابع و پایپ‌لاین تولید داده
- **نقشه بلد (Balad POI):** واکشی کامل ژئوداده‌های ۱۸,۵۰۰ صنف کافی‌شاپ، سینما و ایونت
- **نقشه نشان (Neshan API & Places):** استخراج منوهای آنلاین (`menu_url`)، پیج اینستاگرام و ساعات کاری
- **BoxAPI:** اعتبارسنجی بیزینس پروفایل‌ها، شماره‌های مستقیم بیو و شبکه‌های اجتماعی
- **اکران‌های اعتبارسنجی‌شده میدانی:** ۳۹ کافه شاخص اکران با مشخصات دقیق سالن و تجهیزات پخش
