# vsftpd Backdoor Attack Detection

## Visão geral

Este projeto demonstra a exploração de uma vulnerabilidade real no serviço FTP vsFTPd 2.3.4 e a detecção do ataque através da análise de tráfego de rede.

O objetivo é mostrar não apenas a exploração, mas a capacidade de investigar falhas, corrigir erros e identificar o ataque como um analista de segurança.

---

## Ambiente do laboratório

Máquina atacante  
Kali Linux  
IP: 10.0.2.4  

Máquina vítima  
Metasploitable 2  
IP: 10.0.2.5  

Configuração  
Ambiente isolado com ambas as máquinas na mesma rede  
Comunicação validada via ICMP  

---

## Reconhecimento

Foi realizada varredura de portas para identificar serviços expostos.

Serviços encontrados  
• 21 FTP  
• 22 SSH  
• 80 HTTP  
• 445 SMB  

Decisão  
O serviço FTP foi priorizado devido ao histórico de vulnerabilidades públicas conhecidas.

---

## Vulnerabilidade

O vsFTPd versão 2.3.4 contém um backdoor que pode ser ativado com um padrão específico no login.

Comando utilizado na exploração  

USER test:)

Essa ação pode ativar uma porta oculta no sistema.

---

## Tentativa de exploração

Foi utilizada a ferramenta Metasploit para explorar a vulnerabilidade.

Problema encontrado  
O módulo exigia configuração de LHOST devido ao payload reverso padrão.

Ação tomada  
Foi configurado o LHOST com o IP da máquina atacante.

Aprendizado  
Payloads reversos dependem de configuração correta da origem da conexão.

---

## Falha do exploit automático

Mesmo com a execução correta, o exploit não gerou sessão ativa.

Análise  
A vulnerabilidade não foi ativada automaticamente.

Decisão  
Foi necessário investigar o comportamento do serviço manualmente.

---

## Exploração manual

Foi realizada conexão direta ao serviço FTP utilizando telnet.

Passos executados  

telnet 10.0.2.5 21  
USER test:)  
PASS test  

Resultado  
A ação ativou o backdoor e abriu uma nova conexão na porta 6200.

---

## Execução remota

Foi possível executar comandos remotamente no sistema.

Comando utilizado  

echo test  

Resultado  

test  

Isso confirma execução remota de comandos.

---

## Limitação

A shell obtida é limitada.

Observação  
A interação não permite uso completo de comandos do sistema.

---

## Análise de rede

O ataque foi capturado utilizando Wireshark.

Evidências encontradas  

• Tráfego FTP em texto claro  
• Comando USER test:) visível  
• Solicitação de senha  
• Comunicação sem criptografia  

Trecho identificado  

USER test:)  

Importância  
Esse padrão é conhecido por ativar o backdoor do vsFTPd 2.3.4.

---

## Impacto

• Execução remota de comandos  
• Acesso não autenticado  
• Exposição de credenciais  
• Comprometimento do sistema  

---

## Mitigação

• Atualizar o serviço vsFTPd  
• Desativar serviços desnecessários  
• Monitorar tráfego de rede  
• Bloquear portas suspeitas  
• Implementar ferramentas de detecção  

---

## Aprendizados

• Nem todo exploit funciona automaticamente  
• Entender o comportamento da vulnerabilidade é essencial  
• Análise de rede permite identificar ataques claramente  
• Erros fazem parte do processo real  

---

## Estrutura do projeto

/prints  
Capturas de tela do processo  

/report  
Relatório do incidente  

/notes  
Dúvidas e aprendizados  

---

## Conclusão

A vulnerabilidade permite execução remota de código e representa risco crítico.

O projeto demonstra capacidade prática de exploração e detecção de ataques em ambiente controlado.
