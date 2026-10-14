# UPTIME

Vigia do monitor de sites da Aragon Tecnologia.

O monitor dos sites corre fora deste repo, com a lista de alvos privada. De 5 em 5 minutos, grava a hora da última verificação na variável `PC_HEARTBEAT` deste repo.

O workflow `vigia.yml` corre aqui de 15 em 15 minutos, de forma independente do monitor. Se passarem mais de 20 minutos sem sinal, avisa no Telegram e por email (a execução fica a vermelho). Avisa outra vez quando o sinal volta.

O monitor, por sua vez, confere se este workflow tem corrido. Cada lado avisa se o outro parar.

- Secrets: `TELEGRAM_BOT_TOKEN` e `TELEGRAM_CHAT_ID`, os mesmos do monitor.
- Teste: **Actions → vigia.yml → Run workflow**, com "Mandar uma mensagem de teste".
- O `keepalive.yml` faz um commit por mês, porque o GitHub desliga os agendamentos de um repo público ao fim de 60 dias sem atividade.
