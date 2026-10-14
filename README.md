# Mezun Derneği Web Sitesi

Keçiören Vatansever Şehit Tümgeneral Aydoğan Aydın Fen Lisesi Mezunlar Derneği için geliştirilmiş kurumsal web sitesi ve yönetim paneli. Site; dernek faaliyetlerini, duyuruları, etkinlikleri ve üyelik ile aidat süreçlerini ziyaretçilerle paylaşır. Tüm içerik, yönetim paneli üzerinden koda dokunmadan güncellenebilir.

## Özellikler

### Ziyaretçi Tarafı

- **Ana Sayfa:** Karşılama alanı, öne çıkan duyurular, yaklaşan etkinlikler, galeri seçkisi ve sıkça sorulan sorular.
- **Duyurular:** Arşiv sayfası ve detay kartları.
- **Etkinlikler:** Yaklaşan ve geçmiş etkinlikler, tarih, saat ve konum bilgileriyle.
- **Galeri:** Grid ve carousel görünümü, tam ekran büyütme desteği.
- **Kurumsal Sayfalar:** Başkanın Mesajı, Hakkımızda, Tüzük, Vizyon ve Misyon, Şehit Aydoğan Aydın sayfası, Yönetim ve Denetim Kurulları.
- **Üyelik ve Aidat:** Başvuru adımları, PDF üyelik formu, banka bilgileri ve tek tıkla IBAN kopyalama.
- **İletişim:** İletişim formu, Google Maps haritası, e-posta ve telefon yönlendirmeleri.
- **Yasal Sayfalar:** KVKK Aydınlatma Metni, Gizlilik Politikası, Çerez Politikası ve Kullanım Koşulları.

### Yönetim Paneli

- **Güvenli Giriş:** Supabase Auth ve Next.js middleware ile korunur.
- **İletişim Mesajları:** Toplam, okunmuş ve okunmamış sayıları; arama, filtreleme ve tümünü okundu işaretleme.
- **Duyurular:** Ekleme, düzenleme, görsel yükleme ve silme.
- **Etkinlikler:** Ekleme, tarih, saat ve konum düzenleme, yaklaşan veya geçmiş durumunu yönetme ve silme.
- **Kurul Üyeleri:** Üye ekleme, görev ve fotoğraf güncelleme.
- **Galeri:** Çoklu yükleme, sürükle bırak ile sıralama ve silme.
- **SSS:** Soru ekleme, düzenleme ve silme.

## Teknolojiler

| Alan | Teknoloji |
|---|---|
| Framework | Next.js 16.3.0, App Router |
| UI | React 19.0.0 |
| Dil | TypeScript, strict mod |
| Stil | Tailwind CSS 4.0.0 ve özel CSS tokenları |
| İkonlar | Lucide React |
| Backend | Supabase PostgreSQL, Auth ve Storage |
| Güvenlik | Row Level Security ve Next.js middleware |

## Proje Yapısı

```text
mezun-dernegi/
├── public/          # Logo, SVG ve PDF dosyaları
├── src/
│   ├── app/         # Kamu ve admin rotaları
│   ├── components/  # Admin, Cards, Forms, Home, Layout, Shared
│   ├── config/      # Navigasyon ve içerik ayarları
│   ├── lib/         # Supabase istemcisi ve sorgular
│   └── styles/      # Stil tanımları ve tasarım tokenları
├── supabase/        # SQL migration dosyaları
└── next.config.mjs
```

## Kurulum

Node.js 18 veya üzeri ve npm gerekir.

```bash
git clone https://github.com/pclelif/mezun-dernegi.git
cd mezun-dernegi
npm install
```

Kök dizinde `.env.local` dosyası oluşturup Supabase anahtarlarını ekleyin, ardından:

```bash
npm run dev
```

Uygulama `http://localhost:3000` adresinde açılır.

### Environment Variables

| Değişken | Açıklama |
|---|---|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase projesinin API adresi |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonim istemci anahtarı |

Örnek yapılandırma için `.env.example` dosyasına bakabilirsiniz.

## Kullanım

- **Ziyaretçiler:** Duyuruları, etkinlikleri, galeriyi ve kurumsal bilgileri inceler, üyelik formunu indirir, iletişim formuyla mesaj gönderir.
- **Yöneticiler:** `/admin/login` adresinden giriş yapar; mesajları, duyuruları, etkinlikleri, kurul üyelerini, galeriyi ve SSS içeriklerini yönetir.

### Sıralama Mantığı

- **Duyurular:** En yeniden en eskiye doğru, `created_at` ve `date` alanlarına göre.
- **Etkinlikler:** Yaklaşanlar en yakın tarihten ileriye doğru, geçmişler gerçekleşme tarihine göre arşivlenir.
- **Galeri:** Panelde sürükle bırak ile belirlenen sıra `display_order` alanında saklanır. İstenirse tarihe göre sıralamaya geçilebilir.

## Yönetim Paneli

Panel `/admin` adresindedir.

- **Erişim Koruması:** `proxy.ts`, oturumsuz kullanıcıları `/admin/login` sayfasına yönlendirir. Oturum Supabase Auth jetonuyla doğrulanır.
- **Veri Güvenliği:** Güncelleme ve silme işlemleri Row Level Security politikalarıyla korunur.

## Veritabanı

| Tablo | İçerik |
|---|---|
| `announcements` | Duyuru başlığı, içerik, görsel ve tarih |
| `events` | Etkinlik başlığı, açıklama, tarih, saat, konum ve durum |
| `board_members` | Kurul üyelerinin ad, görev, unvan ve görseli |
| `gallery_images` | Görsel adresleri ve sıralama |
| `faqs` | Sorular ve cevaplar |
| `site_content` | Ana sayfa, kurumsal sayfalar ve genel metinler |
| `contact_messages` | İletişim mesajları, okundu bilgisi ve gönderim tarihi |

## Deployment

Vercel veya Node.js destekleyen herhangi bir sunucuda yayınlanabilir.

```bash
npm run build
npm start
```

## Tasarım

Dernek kimliğini yansıtan sade ve kullanıcı odaklı bir arayüz hedeflenmiştir.

- Vurgu rengi dernek kırmızısı `#EC1C24` olarak kullanılmıştır.
- Okunabilirliği yüksek tipografi tercih edilmiştir.
- Mobilde 44px dokunma hedefleri, çekmece menü ve dokunmatik kartlar uygulanmıştır.

## Geliştirme Notları

- **TypeScript:** Tüm bileşen ve veri modelleri tiplidir. Yeni eklemelerde tür tanımlarına uyun.
- **Middleware:** Admin yetkilendirmesi `src/proxy.ts` içindedir. Rota değiştirirken eşleşme kurallarını kontrol edin.
- **Client ve Server ayrımı:** Supabase istemcileri `src/lib/supabase/client.ts` ve `server.ts` dosyalarında ayrılmıştır.

## Lisans

Bu proje Keçiören Vatansever Şehit Tümgeneral Aydoğan Aydın Fen Lisesi Mezunlar Derneği adına özel olarak geliştirilmiştir. Tüm hakları saklıdır.

**İletişim:** kaaflmezunder@gmail.com
