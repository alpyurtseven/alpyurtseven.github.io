---
layout: post
title:  "Gitlabflow"
date:   2024-12-14 12:54:00 +03
---


## GitLab Flow Nedir?
GitLab Flow, GitFlow ve GitHub Flow modellerine kıyasla daha sade ve esnek bir iş akışı sunar. Continuous Integration (CI) ve Continuous Deployment (CD) süreçleriyle kolayca entegre olur. GitLab Flow, özellikle çeşitli ortamlar (ör. geliştirme, test, üretim) arasında geçişi ve kod dağıtımını daha düzenli hale getirmek için idealdir.

---

## Temel Prensipler

1. **Main branch, her zaman üretime hazırdır.**
   - `main` dalı dağıtıma hazır ve stabil kod içerir.

2. **Branch'ler özelleştirilmiş iş akışlarına göre oluşturulur.**
   - Özellik geliştirme, hata düzeltme ve diğer işler için kısa ömürlü branch'ler kullanılır.

3. **Ortamlarla uyumlu dağıtım dalları kullanılır.**
   - `production`, `staging`,  `development` gibi ortamlar için ayrı dallar bulunur.

4. **Merge işlemleri Merge Request (MR) ile yapılır.**
   - Her branch, `main` dalına merge edilmeden önce bir Merge Request (MR) oluşturulur ve kod gözden geçirilir.

---

## GitLab Flow İş Akışı

### 1. Yeni Branch Oluşturma
```bash
git checkout main
git checkout -b feature/feature-name
```

### 2. Geliştirme Yapma
- Kod geliştirme sırasında düzenli olarak commit işlemleri yapılır:
```bash
git add .
git commit -m "Add feature-name"
```

### 3. Branch'i Push Etme
```bash
git push origin feature/feature-name
```

### 4. Merge Request (MR) Açma
- GitLab üzerinden Merge Request (MR) oluşturulur.
- MR açıklamasına yapılan değişiklikler ve detaylar eklenir.

### 5. Kod Gözden Geçirme ve Merge
- Kod incelenir ve onaylanır.
- MR tamamlandıktan sonra `main` dalına merge edilir:
```bash
git checkout main
git merge feature/feature-name
```

### 6. Dağıtım (Deployment)
- Merge işlemi sonrası CI/CD pipeline otomatik olarak çalıştırılır ve ilgili ortama dağıtım yapılır.

### 7. Branch'i Silme
- Merge sonrası branch silinir:
```bash
git branch -d feature/feature-name
git push origin --delete feature/feature-name
```

---

## Ortam Yönetimi (Environment Management)

GitLab Flow, ortam yönetimini desteklemek için `main` dalı yanında ek dallar kullanılmasını önerir:

- **Production**
  - Üretim ortamındaki kodu tutar.
- **Staging**
  - Üretim öncesi testlerin yapıldığı ortamı temsil eder.
- **Development**
  - Aktif geliştirme dallarının birleştirildiği test ortamını ifade eder.

### Ortam Dalları ile İş Akışı

1. Yeni özellikler `development` dalına merge edilir.
2. Testler tamamlandıktan sonra kod `staging` dalına aktarılır.
3. Son onay ve testlerden sonra kod `production` dalına merge edilir.

---

## Best Practices

1. **Branch İsimlendirmesi**
   - `feature/add-login`
   - `fix/timeout-error`
   - `release/1.2.0`

2. **Merge Request Kullanın**
   - Tüm merge işlemleri MR üzerinden yapılmalı.

3. **Ortam Geçişlerini Yönetmek**
   - Ortam dalları ile kod dağıtım sürecini kontrol altında tutun.

5. **Otomatik Dağıtım**
   - Merge sonrası `staging` ve `production` dalları için otomatik dağıtım yapılandırılmalı.

---

## Avantajlar
- Ortamlar arası geçiş ve dağıtım kolaylığı.
- CI/CD ile güçlü entegrasyon.
- Daha sade ve esnek bir iş akışı.
- Geliştirme, test ve üretim süreçlerinin daha net yönetimi.
