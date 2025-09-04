# Laboratório: Análise de Incidente de Cibersegurança  
## Falha na Resolução de DNS – "Porta UDP 53 Inacessível"

🔍 **Objetivo do Laboratório**  
Analisar um incidente de rede em que usuários não conseguiam acessar o site `www.yummyrecipesforme.com`, recebendo o erro *"destination port unreachable"*. O foco foi identificar a causa raiz por meio da análise de tráfego com ferramentas como `tcpdump`.

---

### 🧩 Cenário do Incidente

Vários clientes relataram que não conseguiam acessar o site **www.yummyrecipesforme.com**, recebendo a mensagem de erro:

> **"destination port unreachable"**

Ao tentar acessar o site, também obtive o mesmo erro. Para investigar, utilizei a ferramenta de análise de tráfego **tcpdump** para capturar e analisar os pacotes enviados durante a tentativa de carregamento da página.

---

### 🕵️‍♂️ Análise Técnica

Ao carregar a página, o navegador executa dois passos principais:
1. Envia uma consulta **DNS (UDP)** ao servidor DNS para obter o IP do domínio.
2. Usa esse IP para fazer uma requisição **HTTPS (TCP na porta 443)** ao servidor web.

A análise do tráfego revelou o seguinte:

- O cliente (`192.51.100.15`) enviou consultas DNS ao servidor DNS (`203.0.113.2`) na **porta 53 (UDP)**.
- Em vez de uma resposta DNS, o cliente recebeu pacotes **ICMP** com a mensagem de erro:

  > **"udp port 53 unreachable"**

---

### ⚠️ Conclusão da Análise

O erro **"udp port 53 unreachable"** indica que:
- O servidor DNS (`203.0.113.2`) **não está respondendo** nas consultas DNS.
- A porta 53 (usada pelo protocolo DNS) **está fechada, bloqueada ou o serviço está inativo**.

🔍 **Causa provável do incidente:**
> O serviço DNS no servidor estava **desativado, com falha ou não estava escutando na porta 53**. Isso impediu a resolução do domínio `www.yummyrecipesforme.com` para um endereço IP, tornando o site inacessível — mesmo que o servidor web estivesse funcionando.

---

### 🛠️ Impacto

- Usuários não conseguiam acessar o site porque o navegador **não conseguia traduzir o nome do domínio em um endereço IP**.
- O problema não estava no site em si, mas na **infraestrutura de rede (serviço DNS)**.

---

### ✅ Lições Aprendidas

1. **DNS é crítico**: Mesmo que o servidor web esteja online, sem DNS, o site fica "invisível".
2. **ICMP fornece pistas valiosas**: Erros como "port unreachable" ajudam a isolar rapidamente o ponto de falha.
3. **Monitoramento contínuo é essencial**: Ferramentas como `tcpdump` e logs de rede são fundamentais para diagnóstico rápido.

---

### 📎 Anexos
- [x] Relatório completo do incidente (PDF)
- [x] Logs de tráfego de rede (arquivo `.pcap`)

---

📌 **Próximos passos (recomendações)**  
- Reiniciar ou verificar o status do serviço DNS (ex: `systemctl status named`).
- Verificar regras de firewall que possam estar bloqueando a porta UDP 53.
- Configurar servidores DNS secundários para alta disponibilidade.

---

💼 Este laboratório faz parte do meu portfólio em cibersegurança.  
Estou desenvolvendo minhas habilidades em análise de tráfego, detecção de incidentes e troubleshooting de rede.  
Seja bem-vindo ao meu processo de aprendizado!
