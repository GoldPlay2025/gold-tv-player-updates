# Gold TV Player — publicação de APK e atualização automática

Este repositório distribui o **Gold TV Player**. A partir de agora, não é preciso editar `gold_update.json` manualmente após publicar uma nova versão.

## Publicação no Android Studio e GitHub

1. No Android Studio, aumente o `versionCode` e o `versionName`. A última versão publicada é `129 / 1.1.0.32.66`; portanto, a próxima deve usar `versionCode` maior que `130`.
2. Gere um **APK assinado com o mesmo certificado usado na versão anterior**. Evite usar um novo computador/perfil de assinatura sem preservar a chave existente. **Não publique AAB**, pois a atualização OTA usa APK.
3. Abra [Criar release](https://github.com/GoldPlay2025/gold-tv-player-updates/releases/new).
4. Use uma tag que corresponda ao `versionName` do APK. Aceitamos **`v1.1.0.32.66` ou `1.1.0.32.66`**; recomenda-se manter o prefixo `v` nas próximas versões por consistência.
5. Anexe o arquivo com o nome **exato `Gold-TV-Player.apk`**. Se necessário, renomeie o APK gerado antes de anexar, sem modificar seu conteúdo.
6. Publique como **Release**, e não como pré-release. O workflow [Gold TV Player - publicar OTA com seguranca](.github/workflows/gold-tv-player-ota.yml) inicia automaticamente.

## O que acontece automaticamente

- Baixa o APK recém-publicado e o APK da versão indicada pelo manifesto atual.
- Confere validade do APK, `applicationId = br.com.goldplay.iptv`, tag, `versionCode` superior, SHA-256 da versão anterior e **mesmo certificado de assinatura**.
- Se algum teste falhar, **não atualiza o manifesto**. Consulte a aba [Actions](https://github.com/GoldPlay2025/gold-tv-player-updates/actions) para o motivo.
- Se tudo passar, atualiza automaticamente `gold_update.json` com o novo `version_code`, `version_name`, `sha256` e endereço fixo daquela release, sem alterar a escolha anterior de atualização opcional/obrigatória.

O manifesto usa o **link fixo por tag**, evitando que `releases/latest` aponte para o novo APK antes de ser validado. O link de compartilhamento via WhatsApp continua estável:

https://github.com/GoldPlay2025/gold-tv-player-updates/releases/latest/download/Gold-TV-Player.apk

**Importante:** assim que uma Release é publicada, o arquivo fica publicamente disponível no GitHub. A validação protege a oferta automática de atualização, não desfaz a publicação manual de um arquivo inválido. Verifique o APK antes de clicar em *Publish release*.

## Após publicar

Aguarde a execução ficar verde em **Actions** e confirme que `gold_update.json` mostra o novo número de versão. Somente então considere a distribuição OTA concluída.

Para uma correção/reprocessamento, o workflow pode ser executado manualmente pela aba Actions com a tag de uma Release publicada. Isso não permite reaproveitar `versionCode` antigo.

Não remova releases anteriores: o fluxo compara a nova assinatura com o APK anterior, e usuários antigos podem precisar da referência da versão anterior.

## Recuperar uma Release ja publicada quando a automacao falhar

No GitHub, abra **Actions → Gold TV Player - publicar OTA com seguranca → Run workflow**; informe a tag exata ja publicada (com ou sem `v`). A automacao verifica o APK antes de disponibiliza-lo pelo manifesto. Os logs da execucao indicam falhas de assinatura, integridade, pacote, numeracao ou rede.
