# Öz Derleyici

Ö programlama dilini Android'de düzenlemek, denetlemek ve cihaz üzerinde çalıştırmak için açık kaynaklı bir mobil derleyici. Uygulama **Expo Go gerektirmeyen Android APK** üretimi için GitHub Actions akışı da içerir.

## Özellikler

- UTF-8/Türkçe tanımlayıcı destekli `.oz` editörü; yazım/typo denetimi kapalıdır.
- Sözcüksel, sözdizimsel ve tür tanılamaları; satır numarasıyla kırmızı hata işaretleri. Derleyici hatası varken çalıştırma engellenir.
- Editör geçici olarak geçersiz taslak metne izin verir; tanılama hemen gösterilir ve kod düzeltilmeden çalıştırma başlatılmaz. Bu bir yazım/typo denetleyicisi değildir.
- Öz örnekleri, yerel derleme ve yorumlayıcı, çıktı paneli ve `oku` için uygulama içi giriş.
- Kullanıcı kodu cihaz içinde çalışır; sunucuya veya LLM'e gönderilmez ve bulut kredisi harcamaz.
- İlk sürümde izinli uygulama I/O dışında keyfî işletim sistemi çağrısı, shell komutu veya native syscall çalıştırılmaz.

> Dil özelliklerinin güncel uygulama kapsamı ve bilinen sınırlamalar için `lib/oz` kaynak koduna ve proje `TODO.md` dosyasına bakın. Pointer, keyfî OS erişimi ve belirtilmemiş C/C++ standart kütüphanesi özellikleri vaat edilmez.

## APK'yi GitHub Actions ile üretme

1. Bu kaynak ağacını kendi GitHub hesabınızda **public** bir depoya gönderin.
2. GitHub deposunda **Actions** sekmesini açın ve ilk çalıştırma için **Android APK → Run workflow** seçin. `main` dalına kaynak değişiklikleri gönderildiğinde de iş akışı çalışır.
3. Başarılı çalıştırma sayfasındaki **Artifacts → `oz-derleyici-android-apk`** bağlantısından APK'yı indirin.
4. APK'yı Android'e kurmak için indirme kaynağına uygulama yükleme izni verin. Play Store imzalı yayın anahtarı bu workflow'un kapsamı dışındadır.

İş akışı GitHub-hosted Ubuntu runner'da Node 22, pnpm 9.12 ve Java 17 kullanır, Expo Android projesini üretir ve `assembleRelease` ile APK oluşturur. Expo Go veya EAS hesabı istemez. Workflow, GitHub deposuna eklendikten sonra GitHub-hosted runner üzerinde çalışır.

## Yerel geliştirme

```sh
pnpm install --frozen-lockfile
pnpm test
pnpm exec tsc --noEmit
pnpm dev
```

Expo başlangıç uygulaması port 8081'i kullanır; APK oluşturma Android/Gradle gerektirir. Dili AI servisi yerine yerel TypeScript çekirdeği çalıştırır.

## Açık kaynak

Bu proje MIT lisanslıdır. Katkı öncesi `CONTRIBUTING.md`'yi okuyun. Güvenlik açığı bildirimleri için GitHub deposunun **Security → Report a vulnerability** özelliğini kullanın.
