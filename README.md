# NorteSoft Tecnologia — Projeto Integrado de Rede Empresarial

**Faculdade Serra Dourada · ADS · Redes de Computadores**
**Trabalho 4 · 2º semestre de 2026 · Professor: Guibson Krause**

| Campo | Valor |
|---|---|
| Integrantes | *Lucas Moura* · *Davi Mota* · *Henrique dos Santos* |
| Ferramenta | Cisco Packet Tracer |

## Resumo da solução

Rede corporativa de uma software house com **6 VLANs** (5 setores/serviços + gerência), **3 switches 2960**
e **1 roteador 2911** fazendo **Router-on-a-Stick** (subinterfaces 802.1Q). Todo o endereçamento sai de
**192.168.50.0/24 com VLSM** (máscaras /26, /27 e /28), com IP estático documentado em todos os equipamentos.

| VLAN | Nome | Setor / finalidade | Sub-rede | Gateway |
|---|---|---|---|---|
| 10 | DEV | Desenvolvimento | 192.168.50.0/26 | 192.168.50.1 |
| 20 | SUP | Suporte técnico | 192.168.50.64/27 | 192.168.50.65 |
| 30 | ADM | Administrativo / Financeiro | 192.168.50.96/27 | 192.168.50.97 |
| 40 | COM | Comercial | 192.168.50.128/27 | 192.168.50.129 |
| 50 | SRV | Servidor e recursos compartilhados | 192.168.50.160/28 | 192.168.50.161 |
| 99 | GER | Gerência dos switches (VLAN nativa do trunk) | 192.168.50.176/28 | 192.168.50.177 |

Totais: **16 PCs + 1 servidor + 1 impressora = 18 dispositivos finais**, 3 switches e 1 roteador.

## Estrutura do repositório

```
.
├── README.md                  ← este arquivo
├── packet-tracer/             ← arquivo .pkt final (NorteSoft_T4.pkt)
├── documentacao/
│   └── RELATORIO.md           ← relatório completo (mesma estrutura do PDF entregue no NAV)
├── configs/                   ← comandos CLI de cada equipamento + tabela de hosts
│   ├── R1-NORTESOFT.txt
│   ├── SW-CORE.txt
│   ├── SW-DEV.txt
│   ├── SW-ADM.txt
│   └── hosts-e-servidor.txt
└── evidencias/                ← capturas de tela dos testes e do troubleshooting
```

## Como abrir e testar o projeto

1. Abra `packet-tracer/NorteSoft_T4.pkt` no Cisco Packet Tracer.
2. Aguarde a convergência (links verdes). Em PCs, o primeiro ping pode dar *timeout* por causa do ARP; repita.
3. Execute os testes descritos na seção 7 de [`documentacao/RELATORIO.md`](documentacao/RELATORIO.md).
   Exemplos rápidos:
   - `PC-DEV-01` → `ping 192.168.50.2` (mesma VLAN)
   - `PC-DEV-01` → `ping 192.168.50.101` (VLAN 10 → VLAN 30, passa pelo roteador)
   - `PC-COM-01` → navegador em `http://192.168.50.162` (servidor)
   - Nos switches: `show vlan brief`, `show interfaces trunk`
   - No roteador: `show ip interface brief`, `show ip route`
4. Para recriar do zero, cole os arquivos de `configs/` em cada equipamento (modo CLI) e configure os hosts
   conforme `configs/hosts-e-servidor.txt`.

## Observação

O repositório, o PDF entregue no NAV e o arquivo `.pkt` representam **a mesma versão** do projeto.
