# Monitor Gerador — POC FUXA + RC Gateway

POC isolada para avaliar uma arquitetura simplificada de monitoramento de grupos geradores usando **RC Gateway + FUXA**, sem alterar a stack validada atual.

## Objetivo

Validar inicialmente o **GEN153 / ComAp InteliGen 200 / Unit 14 / porta de campo 15002** usando somente leitura.

Arquitetura alvo da POC:

```text
Controladora / DTU
        ↓
    RC Gateway
        ↓
       FUXA
        ├── HMI / dashboards
        ├── alarmes
        ├── histórico
        └── usuários / roles
```

## Segurança

- `commandPlaneEnabled=false`.
- Somente leituras Modbus durante a POC.
- Não enviar FC06/FC16.
- Não habilitar START/STOP/RESET/TRANSFER/setpoints.
- Não versionar credenciais, tokens, certificados, arquivos de licença ou pacotes proprietários.

## Artefatos

Os binários não são armazenados neste repositório público. Consulte `artifacts/SHA256SUMS.txt` para identificar exatamente os pacotes usados na POC.

## Estado

`POC_ONLY=true`

`PRODUCTION_VALIDATED=false`
