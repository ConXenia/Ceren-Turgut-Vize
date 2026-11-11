# 3D Top Toplama Oyunu

Ad Soyad: Ceren Turgut
Öğrenci No: 2602020034
Ders: DOT6105 – Oyun İçin Kod Yazımı I (Vize Ödevi)  

## Oyunun Kısa Açıklaması
Unity ile yapılmış, üç seviyeli 3D bir top toplama oyunudur. Oyuncu küreyi WASD/yön tuşlarıyla hareket ettirir, yeşil toplarla +10 puan kazanır, kırmızı toplarla −5 puan kaybeder. Hedef puana ulaşınca çıkış alanından sonraki seviyeye geçer. Hedefler: Level 1 → 30, Level 2 → 50, Level 3 → 70. Üçüncü seviye bitince "Oyunu Tamamladınız!" yazar.

## Scriptlerin Görevleri
- **PlayerControls:** Rigidbody + AddForce ile hareket, zıplama, OnTriggerEnter + CompareTag ile top toplama.
- **ScoreManager:** Puanı tutar ve ekrana yazar.
- **SceneController:** Hedef puanı kontrol eder, SceneManager ile sonraki sahneyi yükler, mesajları gösterir.
- **LevelExit / FinishZone:** Çıkış alanları; oyuncu girince puanı SceneController'a gönderir.
- **AudioManager:** Arka plan müziğini ve 4 ses efektini çalar.

## Sahne Geçişi Algoritması
1. Oyuncu çıkış alanının Trigger'ına girer.
2. Etiketi "Player" değilse dur.
3. Skor, `TryCompleteLevel(skor)` metoduna gönderilir.
4. Skor ≥ hedef ise: sıradaki sahne `buildIndex + 1` ile bulunur.
5. Sıradaki sahne varsa "Level Tamamlandı!" yazılır, 1,5 saniye sonra `SceneManager.LoadScene` ile geçilir. Yeni sahnede skor 0'dan başlar.
6. Sıradaki sahne yoksa "Oyunu Tamamladınız!" yazılır.
7. Skor yetersizse "Yetersiz Puan!" yazılır, sahne değişmez.

## Karşılaşılan Hata ve Çözümü
**Hata:** Toplar toplanmıyor, skor artmıyordu. **Neden:** Tag adı kodla uyuşmuyordu (büyük-küçük harf duyarlı: `GreenBall` ≠ `greenball`) ve topun Collider'ında Is Trigger kapalıydı. **Çözüm:** Etiketler kodla birebir aynı yazıldı, Is Trigger işaretlendi.

## Nasıl Çalıştırılır?
1. Projeyi Unity 6 ile açın.
2. `Project Settings > Player > Active Input Handling` değerini **Input Manager (Old)** veya **Both** yapın.
3. `Assets/Scenes/Level1.unity` sahnesini açıp Play'e basın.
