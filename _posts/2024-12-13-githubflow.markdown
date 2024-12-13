---
layout: post
title:  "Githubflow"
date:   2024-12-13 13:10:00 +03
---


## GitHub Flow Nedir?
GitHub Flow, modern ve hafif bir branching modeli. Özellikle sürekli dağıtım (CD) süreçlerine uygun, sade bir iş akışı için kullanılır. Küçük ve sık deploy yapılacak projelerde çok etkili.

---

## Temel Prensipler
1. **Main her zaman dağıtıma hazır olmalı**
   - `main` dalı her zaman deploy edilebilir bir durumda tutulur.

2. **Her geliştirme yeni bir branch'te yapılır**
   - Tüm yeni özellikler ve düzeltmeler `main` dalından yeni bir branch açılarak geliştirilir.

3. **Pull Request ile geliştirme birleştirilir**
   - Branch tamamlandıktan sonra `main` dalına merge edilmeden önce Pull Request açılır ve kod gözden geçirilir.

4. **Kod gözden geçirildikten sonra merge edilir**
   - PR onaylandıktan sonra branch, `main` dalına merge edilir.

5. **Deploy, merge sonrası yapılır**
   - `main` dalına her merge işlemi yapıldığında deploy alınır.

---


### 1. Yeni Branch Açma
```bash
git checkout main
git checkout -b feature/feature-name
```

### 2. Geliştirme Yapma
- Geliştirme süresince düzenli commit:
```bash
git add .
git commit -m "Add feature-name"
```

### 3. Branch'i Push Etme
```bash
git push origin feature/feature-name
```

### 4. Pull Request Açma
- GitHub'da branch için PR oluşturulur.
- PR açıklamasına yapılacak değişiklikler ve ilgili detaylar eklenir.

### 5. Code review ve Merge
- Kod gözden geçirilir ve onaylanır.
- Merge işlemi yapılır:
```bash
git checkout main
git merge feature/feature-name
```

### 6. Dağıtım (Deployment)
- Merge işlemi sonrası kod otomatik veya manuel olarak dağıtıma alınır.

### 7. Branch'i Silme
- Merge sonrası artık ihtiyaç olmayan branch silinir:
```bash
git branch -d feature/feature-name
git push origin --delete feature/feature-name
```

---

## Best Practices

1. **Anlamlı Branch İsimlendirmesi**
   - `feature/add-login-page`
   - `fix/api-timeout`

2. **Küçük ve Odaklı Branch'ler**
   - Her branch sadece tek bir özelliği veya hatayı çözmeli.

3. **Düzenli Commitler**
   - Commitler küçük ve sık yapılmalı, her biri anlamlı bir değişiklik temsil etmeli.

4. **Code Review**
   - Merge işlemi öncesi her zaman PR oluşturulmalı ve kod incelenmeli.

5. **Sürekli Dağıtım (CD)**
   - `main` dalına yapılan her merge sonrası dağıtım yapılmalı.
---

## Avantajlar
- Basit ve kolay anlaşılır.
- Sürekli dağıtım için ideal.
- Küçük, sık değişikliklerle çalışma sağlar.
- Hızlı geri bildirim döngüsü.
