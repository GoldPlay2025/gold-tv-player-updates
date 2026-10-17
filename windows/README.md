# Gold TV Player — Windows

Versão Windows separada da distribuição Android, sem alteração no OTA Android.

## Gold TV Player Windows Edition 1.1.2

**Status:** instalador publicado e validado no GitHub Releases.

- [Baixar instalador EXE — Windows 10/11 x64](https://github.com/GoldPlay2025/gold-tv-player-updates/releases/download/windows-v1.1.2/Gold-TV-Player-Setup-1.1.2.exe)
- [Ver Release Windows 1.1.2](https://github.com/GoldPlay2025/gold-tv-player-updates/releases/tag/windows-v1.1.2)
- **Arquivo:** `Gold-TV-Player-Setup-1.1.2.exe`
- **Tamanho:** 10.953.728 bytes
- **SHA-256:** `e9469907b4352992fff6f11a8017afd5c0005e98a7cca63c365dea082cb2a40b`

## Organização desta pasta

A pasta `parts/` contém 14 partes binárias do instalador para contornar o limite do conector.
O workflow [windows-release.yml](../.github/workflows/windows-release.yml) junta automaticamente as partes, confere tamanho e SHA-256 e envia o EXE inteiro para a Release Windows. Os usuários **não precisam juntar arquivos**, basta baixar o instalador da Release.

O manifesto Windows [gold_windows_update.json](../gold_windows_update.json) indica a versão e o download oficiais, separadamente do Android.

**Distribuição Android preservada:** o workflow de Windows publica com `--latest=false` para não substituir a Release Android marcada como Latest.
