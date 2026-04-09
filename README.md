# simulado-implantacao-software
Respostas de um simulado para a prova de implantação de software

Tais Gomes – 6324004

Simulado de prova 

Parte 1 – questão 1
Explique o mecanismo que permite ao usuário executar comandos Docker no terminal Linux (WSL) sem a necessidade constante de utilizar o prefixo sudo.
Resposta - O Docker roda como root e só permite acesso via um socket protegido, logo adicionando o usuário ao grupo docker, você ganha permissão para acessar esse socket, podendo executar comandos Docker sem usar sudo.
Qual é o risco de segurança associado ao uso indiscriminado do usuário root no contexto de contêineres?
Resposta - Rodar containers como root aumenta o risco porque, em caso de falha ou invasão, o atacante pode ganhar privilégios elevados e até comprometer o sistema host.

Questão – 2
Diferencie o uso da tag latest do uso de tags semânticas (ex: v1.0.1 ou 3.14-alpine) em ambientes de produção.
Resposta - A tag latest é imprevisível e pode causar quebras inesperadas em produção, enquanto tags semânticas garantem controle, estabilidade e reprodutibilidade dos deploys.

Por que confiar na tag latest pode quebrar um pipeline de CI/CD ou um ambiente de orquestração?
Respostas - Confiar na tag latest pode quebrar um pipeline de CI/CD ou um ambiente de orquestração porque ela é dinâmica e pode apontar para versões diferentes da imagem ao longo do tempo, causando inconsistência e falhas inesperadas.

Questão – 3 
Compare os drivers de rede Bridge (padrão e customizada), Host e None.
Resposta - O Docker oferece diferentes drivers de rede para controlar como os containers se comunicam entre si e com o sistema host.
🔹 Bridge (padrão)
É a rede padrão do Docker.
•	Os containers recebem um IP interno 
•	Conseguem acessar a internet 
•	Comunicação entre containers é limitada (precisa de configuração) 
•	Usa NAT para comunicação externa 
👉 É a opção mais comum, mas não é a mais flexível.
🔹 Bridge (customizada)
É uma versão criada manualmente da bridge.
•	Permite comunicação automática entre containers pelo nome (DNS interno) 
•	Melhor isolamento entre grupos de containers 
•	Mais controle de configuração 
👉 Muito usada em ambientes reais, substituindo a bridge padrão.
🔹 Host
O container compartilha a rede do host diretamente.
•	Não há isolamento de rede 
•	Usa o mesmo IP do host 
•	Melhor desempenho (sem NAT) 
⚠️ Risco:
•	Pode causar conflitos de porta 
•	Menor segurança 
👉 Usado quando performance é crítica.
🔹 None
Não há rede.
•	Container não tem acesso à internet 
•	Não se comunica com outros containers 
•	Total isolamento de rede 
👉 Usado para cenários extremamente controlados ou seguros.

Em que cenário específico um arquiteto de sistemas escolheria o driver Host em vez de uma Custom Bridge, e qual é a principal desvantagem dessa escolha em termos de isolamento?

Resposta - Um arquiteto escolheria o driver Host quando precisa de máximo desempenho de rede e baixa latência, evitando o overhead de NAT presente na bridge.
A principal desvantagem é a perda de isolamento de rede, já que o container compartilha diretamente a rede do host.


# Simulado - Implantação de Software

## Pré-requisitos e Ambiente

- WSL2
- Docker
- Docker Compose

### Estrutura de diretórios

simulado_projeto/
├── app/
│   └── index.html
├── Dockerfile
└── docker-compose.yml

---

## Comandos de Execução e Validação

### Inicialização

```bash
docker-compose up -d --build

