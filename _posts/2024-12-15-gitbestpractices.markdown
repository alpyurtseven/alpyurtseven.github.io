---
layout: post
title:  "Git Best Practices"
date:   2024-12-15 12:45:00 +03
---

## Temel Kavramlar: Rebase ve Merge

### Rebase Nedir?
Rebase, bir branch'teki commit geçmişini başka bir branch'in en son haliyle birleştirir ve commit geçmişini düzenler. Bu işlem, daha temiz ve doğrusal bir commit geçmişi sağlar.

- **Kullanımı:**
  ```bash
  git checkout feature/branch-name
  git rebase main
  ```
- **Avantajları:**
  - Temiz ve kolay okunabilir bir commit geçmişi.
  - Commit'lerin sırasını düzenler.

### Merge Nedir?
Merge, bir branch'teki değişiklikleri başka bir branch'e dahil etmek için kullanılır. Bu işlem, commit geçmişini olduğu gibi bırakır ve birleştirme işlemi için yeni bir merge commit oluşturur.

- **Kullanımı:**
  ```bash
  git checkout main
  git merge feature/branch-name
  ```
- **Avantajları:**
  - Tüm commit geçmişini korur.
  - Takım çalışmasında hangi değişikliklerin birleştirildiğini açıkça gösterir.

---

## Best Practices

### 1. Private branchte rebase, Public branchte merge
- **Rebase:** Kendi branch'in üzerinde çalışıyorsan ve başkalarının erişimi yoksa rebase kullan.
- **Merge:** Paylaşılan branch'ler (ör. `main`, `develop`) için merge kullan ve takım arkadaşlarının commit geçmişine müdahale etme.

### 2. Commit Öncesi Her Zaman Pull Çek
Kodu commit etmeden önce her zaman en güncel değişiklikler için pull çek.

- **Adımlar:**
  ```bash
  git fetch origin
  git pull origin main
  ```
- Bu işlem, olası çatışmaları (conflicts) önler ve en güncel kodla çalışmanı sağlar.

### 3. Commit Öncesi Derleme ve Test Yap
Her commit'ten önce kodu derle ve test et. Böylece hatalı kodun repository'ye girmesini önlersin.

- **Adımlar:**
  ```bash
  # Örnek test komutu
  npm run build && npm test
  ```

### 4. Binary Dosyaları Commit Etmekten Kaçın
Binary dosyaları (`.exe`, `.dll`, `.zip`, vs.) git'e commit etme. Bunun yerine, binary dosyaları oluşturmak için gereken kaynak kodunu veya script'leri paylaş.

- **Yapılması Gerekenler:**
  - `.gitignore` dosyasını kullanarak binary dosyaları hariç tut.
  ```
  *.exe
  *.dll
  *.zip
  ```

### 5. Sürümleme İçin Tag Kullan
Yeni sürümleri belirlemek için git tag'lerini kullan. Tag'ler belirli bir commit'e anlamlı bir isim verir.

- **Tag Oluşturma:**
  ```bash
  git tag -a v1.0.0 -m "First release"
  git push origin v1.0.0
  ```

- **Tag Listeleme:**
  ```bash
  git tag
  ```

### 6. Anlamlı Commit Mesajları Yaz
Commit mesajları kısa, açıklayıcı ve anlamlı olmalıdır.

- **İyi bir commit mesajı formatı:**
  ```
  Başlık: Kısa ama açıklayıcı (ör. "Fix login issue")

  ```

### 7. Feature Branch Kullan
Yeni özellikler, hata düzeltmeleri ve iyileştirmeler için her zaman ayrı branch'ler oluştur. Bu, kodun düzenli ve takip edilebilir olmasını sağlar.

- **Feature Branch Örnekleri:**
  - `feature/user-authentication`
  - `fix/payment-bug`

### 8. Büyük Commit'lerden Kaçın
Büyük ve karmaşık commit'lerden kaçın. Değişikliklerinizi küçük ve anlamlı parçalara böl.

- **İdeal commit:** Tek bir değişikliği veya küçük bir grup ilgili değişikliği temsil eder.

### 9. Pull Request Kullanarak Code Review Yap
Kodu repository'ye merge etmeden önce her zaman bir Pull Request oluştur ve takım arkadaşlarının kodunu gözden geçirmesini sağla.

### 10. Merge Konfliklerini Dikkatlice Çöz
Merge sırasında oluşan çatışmaları dikkatlice incele ve çöz.

- **Conflict çözme adımları:**
  ```bash
  git fetch origin
  git merge origin/main
  # Conflict çöz ve commit et
  git add .
  git commit -m "Resolve merge conflicts"
  ```

---

## Ekstra

- **Küçük ve anlamlı branch isimleri kullan:**
  - `feature/add-login`
  - `fix/header-alignment`

- **Sık sık push yaparak ilerlemenizi kaydet:**
  ```bash
  git push origin feature/branch-name
  ```

- **Eski branch'leri temizle:** İşi tamamlanmış branch'leri düzenli olarak silerek repository'yi düzenli tut.
  ```bash
  git branch -d branch-name
  git push origin --delete branch-name
  ```

---
