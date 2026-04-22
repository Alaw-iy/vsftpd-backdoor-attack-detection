# Incident Report - Unauthorized Access via vsFTPd Backdoor

## 1. Executive Summary

Foi identificada atividade maliciosa explorando um serviço FTP vulnerável.  
O ataque resultou em execução remota de comandos sem necessidade de autenticação válida.

A análise confirmou comprometimento do sistema e exposição de comunicação em texto claro.

---

## 2. Scope

Ativo analisado  
Servidor FTP  

Endereço IP  
10.0.2.5  

Origem da atividade  
10.0.2.4  

Período  
Durante sessão de teste controlado em laboratório  

---

## 3. Detection

A atividade foi identificada através da análise de tráfego de rede.

Indicadores observados  

• Comando de autenticação com padrão anômalo  
• Tráfego FTP sem criptografia  
• Sequência de conexão fora do comportamento normal  
• Comunicação iniciada após tentativa de login  

Evidência principal  

USER test:)  

---

## 4. Attack Analysis

O atacante estabeleceu conexão com o serviço FTP e enviou um padrão específico no campo de usuário.

Esse padrão acionou um comportamento inesperado no serviço, resultando na abertura de uma nova porta de comunicação.

Após isso, foi possível interagir diretamente com o sistema remoto.

---

## 5. Evidence

### 5.1 Network Traffic

Foi identificado tráfego contendo:

USER test:)  
PASS test  

Os dados foram transmitidos em texto claro, permitindo inspeção completa.

---

### 5.2 Remote Command Execution

Comando executado  

echo test  

Resposta  

test  

Esse retorno confirma execução remota.

---

### 5.3 Anomalous Behavior

Após a tentativa de autenticação, foi observada nova conexão na porta 6200.

Essa porta não faz parte do funcionamento padrão do serviço FTP.

---

## 6. Impact Assessment

• Execução remota de comandos  
• Acesso sem autenticação  
• Exposição de dados sensíveis em rede  
• Possível controle total do sistema  

---

## 7. Root Cause

Uso de versão vulnerável do serviço FTP contendo backdoor conhecido.

Ausência de mecanismos de proteção e monitoramento de tráfego.

---

## 8. Detection Opportunities

O ataque pode ser identificado através de:

• Monitoramento de padrões de autenticação  
• Inspeção de tráfego FTP  
• Identificação de strings suspeitas  
• Conexões para portas não padrão  

---

## 9. Recommendations

• Atualizar ou remover o serviço vulnerável  
• Desativar FTP quando não necessário  
• Utilizar protocolos seguros  
• Monitorar tráfego de rede continuamente  
• Implementar soluções de detecção  

---

## 10. Lessons Learned

• Ferramentas automatizadas podem falhar  
• Entendimento do comportamento do serviço é necessário  
• Análise de tráfego fornece visibilidade completa  
• Testes manuais são essenciais para validação  

---

## 11. Conclusion

O incidente demonstrou que o serviço permite execução remota de comandos através de padrão específico de autenticação.

A ausência de criptografia e controle de acesso facilitou a exploração e a análise do ataque.
