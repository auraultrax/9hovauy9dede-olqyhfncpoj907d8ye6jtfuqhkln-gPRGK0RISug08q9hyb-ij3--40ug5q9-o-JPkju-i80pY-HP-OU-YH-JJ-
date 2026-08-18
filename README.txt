AURACELL

Bu uygulama Aura X ile AYNI Firebase projesini kullanır:
projectId: aura-ultra-x

KURULUM
1) Firebase Console > Authentication > Sign-in method > Email/Password'ı aç.
2) Sadece AuraCell için bir admin hesabı oluştur. Örn: auracell@senin-domainin (şifreyi güçlü seç).
3) Bu hesapla AuraCell/index.html üzerinden giriş yap.
4) Firebase Firestore Rules'a aşağıdaki kural mantığını, mevcut kurallarını silmeden, ekle.

AMAÇ
- AuraCell odaları gerçek zamanlı dinler.
- Seçilen odaya dakika verir veya YouTube erişimini kapatır.
- Aura X'in mevcut kullanıcı/admin sistemi değişmez.
- Video dosyaları Firebase Storage'a yüklenmez; Aura X'teki YouTube URL/queue mekanizması kullanılır.

ÖNEMLİ: file:// ile açmak bazı tarayıcı/Firebase ayarlarında sorun çıkarabilir. En sorunsuz yöntem klasörü küçük bir yerel sunucu ile açmaktır (ör. VS Code Live Server). Bu, AuraCell'i internette yayınlamak anlamına gelmez.

GÜVENLİK
Gerçek yetki Firebase Auth + Firestore Rules ile korunmalıdır. HTML/JS içine admin şifresi YAZILMAMALIDIR.

ÖRNEK KURAL MANTIĞI (UID'Yİ kendi AuraCell Auth hesabının UID'si ile değiştir):

match /rooms/{roomId} {
  allow read: if request.auth != null;
  allow update: if request.auth != null && request.auth.uid == 'AURACELL_ADMIN_UID';
}

Bu örnek yalnızca fikir verir. Mevcut odalar için kullandığın Rules mevcut özelliklere göre dikkatlice birleştirilmelidir; mevcut rules dosyasının tamamını görmeden silip değiştirme.
