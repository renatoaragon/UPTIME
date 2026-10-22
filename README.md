# UPTIME

Sinal de vida do monitor de sites da Aragon Tecnologia.

O monitor dos sites corre fora deste repo, com a lista de alvos privada. Este repo guarda só duas variáveis de Actions, que o monitor grava:

- `PC_HEARTBEAT`: a hora (epoch em segundos) da última verificação, de 5 em 5 minutos.
- `PC_QUEDA`: gravada quando o monitor volta depois de estar calado, **antes** do primeiro `PC_HEARTBEAT` da volta. Diz porque se calou:

  ```json
  {"desde": 1760000000, "ate": 1760004000, "motivo": "luz", "detalhe": "opcional, até 200 caracteres"}
  ```

  `desde` é o último `PC_HEARTBEAT` antes da queda e `ate` é a hora da volta. O `motivo` é um destes valores:

  | `motivo` | Quando |
  |---|---|
  | `luz` | arrancou depois do último sinal, com evento 41 (Kernel-Power) ou 6008 no Event Log: desligou sem aviso |
  | `desligado` | arrancou depois do último sinal, com evento 1074 de encerramento |
  | `reiniciado` | arrancou depois do último sinal, com evento 1074 de reinício (o `detalhe` diz quem pediu, ex.: Windows Update) |
  | `suspenso` | não arrancou, mas suspendeu ou hibernou (eventos 42 e 1 do Power-Troubleshooter) |
  | `internet` | não arrancou e as tentativas de gravar o sinal falharam por falta de rede |
  | `monitor` | o computador esteve ligado, mas o monitor não correu |

Quem vigia estas variáveis corre fora deste repo: avisa quando o sinal passa os 20 minutos sem chegar, e outra vez quando volta, com o motivo do `PC_QUEDA`.

O `keepalive.yml` faz um commit por mês, porque o GitHub desliga os agendamentos de um repo público ao fim de 60 dias sem atividade.
