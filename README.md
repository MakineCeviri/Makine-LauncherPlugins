# MakineAI Plugin Registry

Official plugin registry for [MakineAI Launcher](https://github.com/MakineCeviri/MakineAI-Launcher).

## How It Works

This repository serves as the central index for approved MakineAI plugins. The launcher checks `index.json` on startup to discover available plugins and updates.

## For Plugin Developers

1. Create your plugin using the [plugin template](https://github.com/MakineCeviri/makineai-plugin-template)
2. Build and package as `.makine` format
3. Publish on GitHub with the `makineai-plugin` topic
4. [Submit for review](https://github.com/MakineCeviri/makineai-plugins/issues/new?template=plugin-submission.md)

## Plugin Index Format

```json
{
  "version": 1,
  "plugins": [
    {
      "id": "com.makineceviri.live",
      "version": "1.0.0",
      "githubRepo": "MakineCeviri/makineai-plugin-live",
      "downloadUrl": "https://github.com/MakineCeviri/.../releases/download/v1.0.0/live.makine",
      "sha256": "abc123...",
      "size": 2500000
    }
  ]
}
```

## Approval Criteria

- Open source (GPL-3.0 or compatible)
- No malicious code, no data collection without consent
- Follows [Plugin API](https://github.com/MakineCeviri/MakineAI-Launcher/tree/main/core/include/makineai/plugin) conventions
- manifest.json complete and valid
- Builds cleanly with MinGW GCC 13.1+

## License

GPL-3.0
