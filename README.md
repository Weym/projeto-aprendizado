# 🌐 Resumo de Redes de Computadores

Este repositório contém um compêndio de anotações, conceitos e explicações práticas baseadas em 10 aulas de Redes de Computadores. O objetivo é servir como guia de consulta rápida sobre infraestrutura, protocolos, segurança e arquitetura web.

## 📚 Índice

1.  [Fundamentos e Topologias](#1-fundamentos-e-topologias)
2.  [Protocolos e Camada de Transporte](#2-protocolos-e-camada-de-transporte)
3.  [Endereçamento, IP e NAT](#3-endereçamento-ip-e-nat)
4.  [Aplicações Web e APIs](#4-aplicações-web-e-apis)
5.  [DNS: O Sistema de Nomes de Domínio](#5-dns-o-sistema-de-nomes-de-domínio)
6.  [Arquitetura de Rede e Roteamento](#6-arquitetura-de-rede-e-roteamento)
7.  [Modelos de Referência e Hardware](#7-modelos-de-referência-e-hardware)
8.  [Segurança e Criptografia](#8-segurança-e-criptografia)
9.  [Tendências Futuras (IoT, Blockchain, SDN)](#9-tendências-futuras)

---

## 1. Fundamentos e Topologias

**Redes de Computadores** são sistemas que permitem a comunicação e compartilhamento de recursos (dados, impressoras, internet) entre dispositivos. Seus pilares são: **Eficiência, Conveniência, Escalabilidade e Redundância**.

### Topologias de Rede
A topologia define o "mapa" físico ou lógico da rede.

* **Estrela:** Todos conectados a um ponto central (Switch/Hub). *Falha no central derruba tudo, mas falha no host não.* (Mais comum em LANs/Wi-Fi).
* **Barramento:** Um único cabo central. *Simples, mas se o cabo romper, a rede para.*
* **Anel:** Loop fechado, dados circulam em sentido único (Token Ring).
* **Malha (Mesh):** Dispositivos interconectados. *Alta redundância e custo elevado.* (Usada em Backbones).
* **Ponto a Ponto:** Conexão direta entre dois dispositivos.

### Evolução da Web
* **Web 1.0:** Páginas estáticas.
* **Web 2.0:** Interatividade, Redes Sociais, AJAX (assincronismo), Foco em UI/UX.
* **Web 3.0:** Web Semântica, Descentralização, Blockchain, Contratos Inteligentes, IoT.

---

## 2. Protocolos e Camada de Transporte

Protocolos são conjuntos de regras que permitem a comunicação.

### TCP vs. UDP
A escolha depende do que é prioritário: Integridade ou Velocidade.

| Característica | **TCP (Transmission Control Protocol)** | **UDP (User Datagram Protocol)** |
| :--- | :--- | :--- |
| **Foco** | Confiabilidade e Ordem. | Velocidade e Baixa Latência. |
| **Conexão** | Orientado a conexão (Handshake). | "Fire and forget" (Sem conexão prévia). |
| **Garantia** | Garante entrega (retransmite pacotes). | Não garante entrega ou ordem. |
| **Cabeçalho** | Pesado, complexo (Flags, Seq, Ack). | Leve (4 campos: Portas, Tamanho, Checksum). |
| **Uso** | Web (HTTP), E-mail (SMTP), Arquivos. | Streaming, Jogos Online, VoIP, DNS. |

### Protocolos Importantes
* **HTTP/HTTPS:** Web.
* **SMTP/POP/IMAP:** E-mail.
* **FTP:** Transferência de arquivos.
* **RFCs:** Documentos que padronizam a internet (Ex: RFC 1918 para IPs privados).

---

## 3. Endereçamento, IP e NAT

### IPv4 vs. IPv6
* **IPv4:** 32 bits ($2^{32}$ endereços). Esgotado. Formato: `192.168.0.1`.
* **IPv6:** 128 bits. Virtualmente infinito. Suporte nativo a QoS e IPsec. Formato Hexadecimal.

### Máscara de Sub-rede
Define qual parte do IP é a **Rede** e qual é o **Host**.
* Exemplo doméstico: `/24` ou `255.255.255.0`.

### NAT (Network Address Translation)
Solução paleativa para a falta de IPv4. Permite que uma rede privada acesse a internet pública usando um único IP Público.

1.  Dispositivo envia pacote com IP Privado.
2.  Roteador troca IP Privado pelo IP Público + Porta Única na **Tabela NAT**.
3.  Servidor responde ao IP Público.
4.  Roteador consulta a tabela e devolve ao dispositivo correto.
* *Problema:* Quebra o princípio "fim-a-fim" e dificulta conexões de fora para dentro (exige Port Forwarding).

### Ferramentas de Diagnóstico
* **Ping:** Testa conectividade e mede latência.
* **Traceroute:** Mostra a rota (saltos) até o destino e onde há gargalos.

---

## 4. Aplicações Web e APIs

### Arquitetura
* **3 Camadas:** Apresentação (Front), Aplicação/Lógica (Back/API), Dados (DB).
* **Microsserviços:** Divisão do sistema em serviços pequenos e independentes. Melhora escalabilidade e tolerância a falhas.

### APIs e REST
* **RESTful:** Estilo arquitetural baseado em recursos, Stateless, Cacheável.
* **Verbos HTTP:** GET (Ler), POST (Criar), PUT (Atualizar tudo), PATCH (Atualizar parcial), DELETE (Remover).
* **Status Codes:** 200 (OK), 404 (Not Found), 500 (Server Error).

### Formatos de Dados
* **JSON:** Leve, padrão da web atual.
* **XML:** Verboso, estrito, suporte a esquemas complexos (usado em NFe, SOAP).
* **YAML:** Foco em legibilidade humana (Configurações).

---

## 5. DNS: O Sistema de Nomes de Domínio

O "catálogo telefônico" da internet. Traduz `google.com` -> `142.250.1.1`.

### Hierarquia e Resolução
1.  **Resolver (Cliente):** Pergunta "quem é x.com?".
2.  **Root Server (.):** Indica o servidor do TLD.
3.  **TLD Server (.com):** Indica o servidor autoritativo.
4.  **Authoritative Server:** Responde com o IP final.

### Segurança e Conceitos
* **Cache:** Armazena respostas para evitar consultas repetidas (controlado pelo TTL).
* **Cache Poisoning:** Ataque onde dados falsos são inseridos no cache do DNS para redirecionar usuários a sites maliciosos.
* **DNSSEC:** Assinatura digital para garantir autenticidade da resposta DNS.
* **DNS Reverso (PTR):** Traduz IP -> Nome (importante para anti-spam).
* **CDN & Anycast:** Usa o DNS para entregar o IP do servidor geograficamente mais próximo do usuário.

---

## 6. Arquitetura de Rede e Roteamento

* **ISP (Internet Service Provider):** Provedores de acesso.
* **Backbone:** As "autoestradas" da internet (fibra ótica submarina).
* **IXP (PTT):** Pontos de troca de tráfego.
* **Roteamento:**
    * **BGP:** Protocolo que roteia entre grandes redes autônomas (a "cola" da internet).
    * **OSPF:** Roteamento interno (menor escala).
    * **Unicast vs. Multicast:** Envio para um único destino vs. envio para grupo (IPTV).

---

## 7. Modelos de Referência e Hardware

### Classificação Geográfica
* **PAN:** Pessoal (Bluetooth).
* **LAN:** Local (Ethernet, Wi-Fi doméstico).
* **MAN:** Metropolitana (Cidade).
* **WAN:** Longa distância (Internet).

### Modelos de Camadas

![Modelo de camadas](https://encrypted-tbn1.gstatic.com/licensed-image?q=tbn:ANd9GcQ6Kt5D_SuRZka9AaKQwzcGYb-6iQ4VeQHIImwvt6Hq9hRsydGIZNxxXviiKZITIKrA6_CNfqX4kaggssDYeeysZEk6pKEh9lhgK_KXwmsAMsGIQcU)

* **OSI (7 Camadas):** Física, Enlace, Rede, Transporte, Sessão, Apresentação, Aplicação.
* **TCP/IP (4 Camadas):** Acesso à Rede, Internet, Transporte, Aplicação.

---

## 8. Segurança e Criptografia

### Ameaças
* **DDoS:** Negação de serviço distribuída (inundação de tráfego). Mitigação: Rate limiting, WAF, Anycast.
* **Phishing/Engenharia Social:** Enganar o usuário.
* **Malware:** Software malicioso.

### Defesa
* **Firewall:** Filtra tráfego baseado em regras (IP/Porta).
* **VPN:** Túnel criptografado. Garante confidencialidade e acesso remoto seguro.
* **WAF (Web Application Firewall):** Protege contra ataques na camada 7 (SQL Injection, XSS).

### Criptografia
* **Simétrica:** Mesma chave criptografa e descriptografa (Rápido, ex: AES).
* **Assimétrica:** Chave Pública (encripta) e Privada (decripta).
* **Hash:** Mão única, verifica integridade (Ex: SHA-256).
* **HTTPS (SSL/TLS):**
    1.  **Handshake:** Servidor envia certificado.
    2.  Troca de chaves assimétricas para criar uma chave de sessão.
    3.  Transmissão de dados usando criptografia simétrica (mais rápida).

### Legislação
* **LGPD:** Lei Geral de Proteção de Dados. Exige consentimento, HTTPS, anonimização e notificação de vazamentos.

---

## 9. Tendências Futuras

* **IoT (Internet das Coisas):** Tudo conectado. Desafios: Segurança fraca e uso em botnets. Protocolos: MQTT.
* **SDN (Redes Definidas por Software):** Separação entre plano de controle (software) e plano de dados (hardware).
* **Blockchain & Web 3.0:** Descentralização. Uso de Hash (SHA-256) para imutabilidade.
* **Cloud vs. On-Premise:** Migração para nuvem (AWS, Azure) vs. Servidores locais.