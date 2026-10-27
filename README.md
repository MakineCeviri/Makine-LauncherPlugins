# Makine Launcher — Eklenti Kayıt Defteri

**[Makine Launcher](https://github.com/MakineCeviri/Makine-Launcher)** eklentilerinin resmî listeye girme kapısı. Eklenti eklemek ya da güncellemek isteyenler buraya PR açar; inceleme de burada yapılır.

Launcher bu depoyu **okumaz**. Kullanıcıların gördüğü liste CDN'deki imzalı dizindir:

```
https://cdn.makineceviri.org/assets/plugins/index.json      eklenti listesi
https://cdn.makineceviri.org/assets/plugins/index.json.sig  Ed25519 imzası
```

Launcher imzası tutmayan dizini reddeder. Dizinde yazan SHA-256 ile eşleşmeyen paketi de kurmaz. İmza anahtarı hiçbir depoda bulunmaz.

## Akış

```
Geliştirici: eklenti deposu + sürüm etiketi
    ↓  PR: plugins.json'a { id, repo, tag } satırı
Bakımcı: kodu inceler → etiketten derler → paketler
    ↓  python scripts/plugin_registry.py pack | add | sign   (Makine-Launcher deposu)
CDN: data/plugins/<id>/<sürüm>.mkplugin  +  imzalı assets/plugins/index.json
    ↓
Makine: Ayarlar → Eklentiler → Kur  (yetki onayı → indirme → SHA-256 → kurulum)
```

Ayrıntılı adımlar, eklenti yazma rehberi ve ABI:
[docs/plugins/README.md](https://github.com/MakineCeviri/Makine-Launcher/blob/dev/docs/plugins/README.md).
Tasarım gerekçesi: [ADR-0009](https://github.com/MakineCeviri/Makine-Launcher/blob/dev/docs/adr/0009-plugin-system-v2.md).

## plugins.json

```json
{
  "plugins": [
    { "id": "org.makineceviri.live", "repo": "MakineCeviri/Makine-LauncherPlugin-Live", "tag": "v1.0.0" }
  ]
}
```

| Alan | Açıklama |
|------|----------|
| `id` | Eklentinin `manifest.json` içindeki kimliği (ters alan adı: `org.ornek.eklenti`) |
| `repo` | Kaynak kodun GitHub deposu (`Kullanici/Repo`) |
| `tag` | İncelenip derlenecek sürüm etiketi; `null` = henüz yayımlanmadı |

## Eklenti nasıl eklenir

1. [Makine-LauncherPlugin-Template](https://github.com/MakineCeviri/Makine-LauncherPlugin-Template) şablonundan başlayın (ABI 2).
2. Eklentinizi `plugin_dev.py` ile deneyin, ardından Makine'de *Geliştirici modu → Dosyadan yükle* ile kurup test edin.
3. Deponuzda bir sürüm etiketi oluşturun ve bu depoya `plugins.json` satırını ekleyen bir PR açın.

Kurallar:
- Her yetki (`network`, `screen-capture`, `overlay`, `game-files-read`, `game-files-write`, `process-inject`) için kullanıcının okuyacağı Türkçe bir gerekçe yazılmalı.
- Hile koruması olan oyunlara bağlanmaya çalışan eklentiler listeye alınmaz.
- Listede olmayan eklentiler yalnızca dosyadan, geliştirici modunda ve *Doğrulanmamış* işaretiyle kurulabilir. GitHub etiketiyle (`makine-plugin`) keşif kaldırıldı.

## Resmî eklentiler

| Eklenti | Depo | Durum |
|---------|------|-------|
| Makine Live | [Makine-LauncherPlugin-Live](https://github.com/MakineCeviri/Makine-LauncherPlugin-Live) | ABI 2'ye taşınıyor |
| Makine Hook | [Makine-LauncherPlugin-Hook](https://github.com/MakineCeviri/Makine-LauncherPlugin-Hook) | Listede değil: yeniden yazılması gerekiyor (ADR-0009, *Rollout*) |

## Lisans

GPL-3.0
