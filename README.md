# Makine Launcher — Eklenti Kayıt Defteri

Açık kaynak kodlu **[Makine Launcher](https://github.com/MakineCeviri/Makine-Launcher)** eklenti ekosisteminin merkezi deposu. Makine Launcher, Türkçe oyun çeviri paketlerini yöneten ücretsiz bir masaüstü uygulamasıdır.

Bu depo, Launcher'ın başlangıçta kontrol ettiği `index.json` dosyasını barındırır. Eklentiler bu liste aracılığıyla keşfedilir, güncellenir ve kurulur.

## Nasıl Çalışır

```
Geliştirici eklentisini GitHub'a yükler
    ↓
index.json'a eklenir (id, versiyon, indirme bağlantısı, SHA-256)
    ↓
Makine Launcher başlangıçta index.json'u kontrol eder
    ↓
Kullanıcı "Kur" der → .makine paketi indirilir → eklenti kurulur
```

## index.json Formatı

```json
{
  "version": 1,
  "updatedAt": "2026-03-16T00:00:00Z",
  "plugins": [
    {
      "id": "com.makineceviri.live",
      "version": "0.1.0",
      "githubRepo": "MakineCeviri/Makine-LauncherPlugin-Live",
      "downloadUrl": "https://github.com/.../releases/download/v0.1.0/makine-live.makine",
      "sha256": "abc123...",
      "size": 2500000
    }
  ]
}
```

| Alan | Açıklama |
|------|----------|
| `id` | Eklentinin benzersiz kimliği (`com.gelistirici.eklenti-adi`) |
| `version` | Semantik versiyon (`1.0.0`) |
| `githubRepo` | GitHub repo yolu (`Kullanici/Repo`) |
| `downloadUrl` | `.makine` dosyasının doğrudan indirme bağlantısı |
| `sha256` | Paketin SHA-256 sağlama toplamı |
| `size` | Paket boyutu (byte) |

## Resmi Eklentiler

| Eklenti | Repo | Açıklama |
|---------|------|----------|
| Makine Live | [Makine-LauncherPlugin-Live](https://github.com/MakineCeviri/Makine-LauncherPlugin-Live) | Gerçek zamanlı ekran OCR ve çeviri overlay |
| Makine Hook | [Makine-LauncherPlugin-Hook](https://github.com/MakineCeviri/Makine-LauncherPlugin-Hook) | GDI hooking, asset parsing, bellek tarama |

## Topluluk Eklentisi Nasıl Eklenir

1. [Makine-LauncherPlugin-Template](https://github.com/MakineCeviri/Makine-LauncherPlugin-Template) şablonunu kullanarak eklentinizi oluşturun
2. GitHub'da yayınlayın ve `makine-plugin` etiketini ekleyin
3. Bu depoda bir [issue](https://github.com/MakineCeviri/Makine-LauncherPlugins/issues/new) açarak eklemenizi talep edin
4. `index.json`'a eklenmek için PR gönderin

## Güvenlik

- Tüm indirmeler yalnızca **HTTPS** üzerinden
- Her paket **SHA-256** sağlama toplamı ile doğrulanır
- `.makine` formatı (MKPK v2) — zstd sıkıştırmalı tar arşivi
- ZIP yol geçişi koruması (path traversal engeli)
- Tehlikeli dosya türleri engellenir (.exe, .bat, .cmd, .ps1)
- DLL imza doğrulaması (Authenticode)

## Lisans

GPL-3.0
