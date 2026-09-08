# VM nova — preparação da POC

## Sistema recomendado

- Ubuntu Server 24.04 LTS x86_64
- 2 vCPU mínimo; 4 vCPU recomendado
- 4 GB RAM mínimo; 8 GB recomendado
- 40 GB disco mínimo
- IP LAN fixo ou reserva DHCP
- NTP sincronizado

## Portas da POC

- `15002/tcp`: entrada do DTU/controladora para o RC Gateway
- `25002/tcp`: consumidor local; deve permanecer em `127.0.0.1`
- `18080/tcp`: administração/health do Gateway; deve permanecer em `127.0.0.1`
- `1881/tcp`: interface FUXA; inicialmente restrita à LAN/VPN, não à Internet pública

## Artefatos locais

Criar fora do Git:

```text
/opt/monitorgerador-poc/
├── gateway/
├── fuxa/
├── configs/
├── evidence/
└── backups/
```

Copiar para a VM, sem publicar no GitHub:

- `RC_Gateway_Standalone_6af76e6_linux_amd64.zip`
- `v1.3.4-2890.zip`

Conferir os hashes com `artifacts/SHA256SUMS.txt` antes da instalação.

## Ordem de execução

1. preparar sistema, NTP e firewall;
2. validar SHA-256 dos dois pacotes;
3. instalar RC Gateway com zero túneis;
4. instalar FUXA Pro sem conexão de campo;
5. validar login/interface e persistência local;
6. criar configuração local do Gateway a partir de `configs/gateway.gen153.example.json`;
7. substituir o CIDR de documentação pelo peer real observado, usando `/32` quando aplicável;
8. validar `--check-config`;
9. ativar somente a porta 15002;
10. configurar no FUXA uma conexão Modbus TCP para `127.0.0.1:25002`, Unit ID 14;
11. começar com FC03 somente leitura;
12. validar os registradores do GEN153 e só então montar dashboard/histórico/alarmes.

## Não fazer

- não copiar configuração da VM de produção como está;
- não versionar licença, senha ou segredo do FUXA;
- não abrir `25002` ou `18080` na LAN;
- não habilitar comandos Modbus;
- não remover ou alterar a VM baseline durante a POC.

`PRODUCTION_VALIDATED=false`
