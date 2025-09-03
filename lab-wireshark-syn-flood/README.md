# Laboratório: Análise de Ataque SYN Flood com Wireshark

## Objetivo
Analisar um ataque de negação de serviço (DoS) do tipo SYN flood usando logs do Wireshark.

## O que aprendi
- Como funciona o handshake TCP (SYN → SYN-ACK → ACK)
- Como um ataque SYN flood sobrecarrega o servidor
- Identificar tráfego malicioso em logs
- Diferença entre tráfego legítimo (green) e ataque (red)

## Conclusão
O servidor foi inundado com pacotes SYN do IP 203.0.113.0. Após a entrada 125, ele parou de responder aos funcionários. Isso é um ataque DoS direto.

> Esse tipo de ataque pode ser mitigado com limitação de conexões ou uso de firewalls.
