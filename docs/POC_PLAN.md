# POC — RC Gateway + FUXA

## Baseline

A VM atual validada permanece intacta. Esta POC deve rodar em uma VM nova e isolada.

## Equipamento piloto

- Gerador: GEN153
- Controladora: ComAp InteliGen 200
- Porta de campo: 15002
- Modbus Unit ID: 14
- Escopo: somente leitura

## Valores de referência já observados em funcionamento

- RPM: ~1800
- Frequência: ~60.0 Hz
- Tensões L1/L2/L3: ~227 V
- Bateria: ~28.7 V
- Engine state: 7 / Running
- Breaker state observado: 1 / BrksOff

Esses valores são referências de teste, não valores sintéticos e não devem ser hard-coded na aplicação.

## Gates

A POC só será considerada tecnicamente bem-sucedida se provar:

1. sessão reverse TCP recebida pelo RC Gateway;
2. allowlist restrita ao peer efetivamente observado;
3. Unit 14 respondendo somente leitura;
4. FUXA exibindo RPM, frequência, tensões e bateria corretamente;
5. estado Running coerente;
6. histórico real;
7. alarmes/eventos básicos;
8. usuário/role de operação somente leitura;
9. perda e retorno de comunicação sem zeros inventados;
10. restart/reboot preservando configuração e coleta;
11. nenhum comando industrial habilitado.

## Arquitetura de teste

```text
DTU / Controladora
      ↓
VM POC :15002
      ↓
RC Gateway
      ↓
FUXA
```

## Regras de segurança

- `commandPlaneEnabled=false` no Gateway.
- Não usar FC06/FC16.
- Não habilitar comandos no FUXA durante esta POC.
- Não expor a interface FUXA diretamente à Internet.
- Pacote/licença FUXA Pro não deve ser commitado neste repositório público.

## Critério de decisão

Se o FUXA reproduzir a telemetria real, histórico, alarmes, usuários/roles e uma interface operacional satisfatória com menos componentes, será avaliado como substituto potencial do frontend/Monitor/Admin próprios e, em uma etapa posterior separada, do Rapid SCADA.

`PRODUCTION_VALIDATED=false`
