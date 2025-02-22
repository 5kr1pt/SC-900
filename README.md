# Minha trilha para a Certificação SC-900

Passei na certificação SC-900 e quero compartilhar meu passo a passo para quem quiser estudar. Levei uma semana para me preparar e aqui vai meu processo:

1. **Decidi fazer a prova em um centro de treinamento**  
   Fiz isso porque sabia que não conseguiria entregar a infra necessária para realizar a prova.

2. **Optei pela prova em português**  
   Mas me arrependi durante a prova, pois a tradução estava bem fraca. Felizmente, a Microsoft libera a opção de ver a pergunta em inglês, o que ajudou bastante.

3. **Questões**  
   A maioria eram de verdadeiro ou falso.

4. **Nota**  
   Tirei 950 de 1000.

5. **Minha etapa de estudo**  
   Consistiu em ler todo o conteúdo do [Microsoft Learn SC-900](https://learn.microsoft.com/pt-br/credentials/certifications/security-compliance-and-identity-fundamentals/?practice-assessment-type=certification). Por mais que no começo possa ficar confuso pra algumas pessoas, ele já ajuda a ter uma base legal (em 3 dias consumi todo o conteúdo – é bem chato de ler se vc for estudar em português, pois a tradução é fraca). Recomendo fortemente realizar as avaliações práticas do MS Learn.  
   _Dica Extra:_ Entenda e grave **TODOS** os conceitos em português e inglês. Um exemplo que quebra bastante é quando a Microsoft decidiu traduzir o CSPM (Cloud Security Posture Management) para GPSN (??????????). Traduzir a sigla kkkkkkk. Mas de boa

6. **Complemento dos estudos**  
   Assisti às aulas do professor Marcus Vinicius ([link](https://www.youtube.com/watch?v=7rgljUIssu4&list=PLLmKXx1axFMxbEu75Ihc1ECDSLputnvag)) e o Exam Cram ([link](https://youtu.be/_df18yKYxVY)) (inclusive para esse, tenho ele legendado em português caso alguem queira, pode chamar no Linkedin) para complementar os estudos.

7. **Prática intensiva**  
   Realizei MUITAS questões e, quando senti que estava preparado, fiz a prova. (No meu obsidian tem bastante questões)

   Com isso, em apenas 1 semana consegui passar (quase que com nota máxima) nesse certificação!

---

Segue abaixo minhas anotações digitalizadas:

# 1. Segurança e Conformidade

## 1.1 Modelo de Responsabilidade Compartilhada

Divisão de responsabilidades entre o provedor de nuvem (Microsoft) e o cliente:

- **SaaS – Software como Serviço:**  
    A organização gerencia os dados, identidades e acessos, enquanto o provedor cuida da infraestrutura, plataforma e aplicativos.
- **PaaS – Plataforma como Serviço:**  
    Os aplicativos ficam por conta do provedor de nuvem; o restante é responsabilidade da organização, como desenvolver e manter o código, os dados e a lógica do aplicativo..
- **IaaS – Infraestrutura como Serviço:**  
    Toda a infraestrutura (parte física, rede, etc.) é responsabilidade do provedor de nuvem.
- **Local:**  
    Tudo, desde os dados até os servidores, é de responsabilidade da organização.

## 1.2 Defesa em Profundidade

Defesas implementadas em camadas para aumentar o nível de segurança da organização.  
Exemplos:

- Ativar multifator
- Não deixar os NSGs muito abertos

## 1.3 Criptografia e Hash

**Criptografia:**  
Método de "embaralhar" dados para que fiquem ilegíveis a quem não tem autorização.

- **Tipos:**
    - **Criptografia Simétrica:**  
        Usa a mesma chave para criptografar e descriptografar.
    - **Criptografia Assimétrica:**  
        Utiliza um par de chaves (pública e privada).
        - _Exemplo:_ Na organização Contoso IT, ao enviar um e-mail para a Fabrikan, você criptografa com a chave pública da Fabrikan; apenas eles podem descriptografar, pois possuem a chave privada.
        - Você não possui a chave privada deles, apenas a pública (usada para criptografar).
        - Ambos os lados possuem suas chaves públicas.

**Aplicações dos tipos de criptografia:**

- **Em repouso:** Banco de dados, file servers
- **Em uso:** Memória RAM
- **Em trânsito:** HTTPs

**Hash:**  
Utiliza um cálculo (ex.: MD5, SHA256) para gerar um código de tamanho fixo, garantindo a integridade dos dados e o armazenamento seguro de senhas.

- _Exemplo:_
    - Para a senha `pass123`:
        - Em MD5 gera: `32250170a0dca92d53ec9624f336ca24`
        - Alterando para `Pass123` (com "P" maiúsculo) gera: `2f23fa3579f3f75175793649115c1b25`
- Bancos de dados usam hash para não armazenar senhas em texto plano, comparando a hash enviada pelo usuário com a armazenada.
- As hashes devem ser irreversíveis, mas ataques (ex.: Dicionário ou Tabela Arco Iris) podem ocorrer.
- **Salt:**  
    Técnica que adiciona caracteres ou números (antes ou depois da senha) para dificultar a quebra da hash.

**Assinatura Digital:**  
Algoritmo matemático (assimétrico) usado para validar a autenticidade e integridade de uma mensagem.

## 1.4 GRC – Governança, Risco e Conformidade

- **Governança:**  
    Gestão e ciclo dos dados.
- **Risco:**  
    Probabilidade de algo estar vulnerável ou sob ameaça.
- **Conformidade:**  
    Processo de aderir a padrões ou regulamentos.

---

# 2. Identidade

## 2.1 Evolução do Acesso

- Antigamente, para acessar uma organização era necessário estar fisicamente na rede (cabo, switch, VPN).
- Atualmente, com o Home Office e a migração da rede para a nuvem, o acesso é feito com base na identidade, que se tornou o perímetro principal de segurança.
- **Modelo Zero Trust:**
    - "Não confie em ninguém, desconfie de tudo"
    - Verificação explícita a todo momento
    - Pressuposição de violação ("Estou sendo invadido!")
    - Princípio do Least Privilege (privilégio mínimo)

## 2.2 Autenticação x Autorização

- **Autenticação (AuthN):**  
    Processo de confirmar que a pessoa é quem diz ser. ("Quem é você?")
- **Autorização (AuthZ):**  
    Define até onde a pessoa pode ir ou quais recursos pode acessar, após ser autenticada.

## 2.3 Provedor de Identidade (idP)

- Sistema que entrega e gerencia identidades de usuários, dispositivos e aplicativos.
- Deve estar ligado à autenticação moderna, possuir SSO e gestão de identidades.
- **SSO:**  
    Com apenas um login, o usuário acessa vários aplicativos e recursos permitidos.
- _Exemplo:_ Microsoft Entra ID.

## 2.4 Active Directory

- Serviço de diretório (AD DS) configurado em um Domain Controller.
- Gerencia identidades, mas não possui permissão nativa para aparelhos móveis, aplicações SaaS e LOB.

## 2.5 Federação

- Permite que usuários de outras organizações acessem recursos da sua organização (e vice-versa) por meio de uma relação de confiança.

---

# 3. Entra ID – Funções e Identidades

## 3.1 Entra ID

- IdP da Microsoft baseado em nuvem.
- **Tipos de Dispositivos:**
    - **Dispositivos Registrados (Registered):**  
        Modelo BYOD ("Traga seu aparelho"); são dispositivos pessoais.  
        Pode-se usar MAM para gerenciar apenas os aplicativos da empresa.
    - **Dispositivos Ingressados (Joined):**  
        Dispositivos exclusivos e gerenciados pela empresa; utilizam MDM para gerenciar tudo.
    - **Entra Ingressados Hibridamente (Hybrid Joined):**  
        Aparelhos que estão ingressados no Entra e também no AD DS on-premises.

## 3.2 Identidades Externas

- **B2B – Business-to-Business:**  
    Colaboração entre empresas.
- **B2C – Business-to-Customer:**  
    Voltado para o produto final, conectando clientes ao ambiente da empresa.
- **Tipos de Identidade:**
    - Internal Member
    - Internal Guest
    - External Member
    - External Guest
- Os tipos de identidades abrangem usuários, aplicativos e dispositivos; para usuários, os tipos (userType) são apenas Guest ou Member.

---

# 4. Métodos de Autenticação

- **Password:**  
    Considerado fraco.
- **Password + SMS ou Voice:**  
    Nível médio (mas SMS possui vulnerabilidades e é desconsiderado).
- **Password + Authenticator App / Software OATH / Tokens OTP:**  
    Maior segurança.
- **Passwordless** (FIDO2, biometria via Windows Hello). -> Melhor

---

# 5. Identidade Híbrida

![hybrid](https://learn.microsoft.com/pt-br/training/wwl-sci/explore-basic-services-identity-types/media/entra-cloud-sync-inline.png)

- A sincronização entre o AD Local e o Entra é feita pelo **Entra Connect Sync** ou **Entra Cloud Sync**.
- **Tipos de Sincronização:**
    - **Sincronização de Hash:**
        - O Entra ID sincroniza automaticamente com o AD Local.
        - Os usuários autenticam diretamente no Entra, sem a necessidade de consultar o AD Local, mesmo se este cair.
        - Em alguns regulamentos, essa sincronização de hash não é recomendada.
    - **Passthru-Authentication:**
        - A autenticação se comunica com o AD Local para validar a hash informada pelo usuário no Entra ID.

---

# 6. Windows Hello for Business

- **Windows Hello for Business:**  
    Meio de autenticação para dispositivos gerenciados (joined), utilizando chaves de acesso e certificados.
- **Windows Hello:**  
    Utiliza PIN e biometria, voltado para dispositivos pessoais e/ou registrados na empresa.

---

# 7. Entra ID SSPR

- **Entra ID SSPR:**  
    Feature do Entra ID que permite aos usuários resetarem suas senhas sem precisar abrir chamado com a TI.
- Funcionalidades:
    - Trocar a senha caso o usuário a conheça e queira alterá-la.
    - Resetar a senha quando esquecida.
    - Desbloquear a conta em caso de bloqueio.
    - **Observação:** Não ativa contas desativadas.


---
# 8. Riscos e Proteção de Identidade

**User e Sign-in Risks**

- **User Risk:**  
    "A conta tá OK, mas o uso está estranho."  
    Credenciais Vazadas  
    Login de um dispositivo diferente
- **Sign-in Risk:**  
    "Essas tentativas falhas estão estranho"  
    Viagem atípica  
    IP malicioso

**Proteções de Identidade**

- **ID Protection**
- **Entra ID Protection:**  
    Trabalha junto às Conditional Access
    - Detected: Categoriza o risco em: baixo, médio e alto (entre sign-in risk e user risk)
    - Investigate: Investigação de riscos.
    - Remediate: Remédios auto ou manual.
    - Export: Exportar para análise futura.

**Autenticação e Controle de Acesso**

- **Password Protection (Central > Métodos de autenticação > Password Protection):**
    - Impede ataque de pulverização
    - Lista de senhas fracas (Global e Custom)
    - Smart Lockout: Bloqueia conta com risco.
- **Acesso Condicional (Central > Acesso Condicional):**  
    (If/Then) Se, então faça.  
    Ex: Se você está autenticando de fora da empresa (IP público desconhecido), faça uma prova que é você: MFA.  
    Ex: Se houver acesso fora do Brasil, quero que bloqueie.
- **RBAC (Role-Based Access Control):**  
    Menor privilégio que o usuário tem que ter – acesso baseado em função.  
    Just enough.
- **Identity Governance (Governança):**
    - Ciclo de vida da identidade: Contratado, 1º Cargo, 2º Cargo, demissão/aposentadoria.
    - Access Reviews: Exemplo – pessoa na equipe sem acesso por 90 dias; deve continuar?  
        Garante que apenas quem deve acessar, acesse e resolve problemas de acesso excessivo.
- **PIM (Privileged Identity Management):**  
    Garante que X usuário só terá X acesso por um tempo específico, permitindo remover quando quiser ou sob aprovação.  
    Tudo isso é auditável.

---

# 9. Proteção de Rede e Infraestrutura

**Defesa de Tráfego e Ameaças Externas**

- **DDoS Protection:**  
    Analisa o tráfego e é adaptável, bloqueando acesso suspeito.  
    Vnet já tem proteção por padrão sem precisar ativar (Básico/Licença).  
    Na versão Standard há muitas outras proteções de DDoS.
- **Azure Firewall:**  
    Apenas um firewall básico, mas robusto e escalável, com DNAT, SNAT, alta disponibilidade e logs detalhados..  
    DNAT e SNAT: Diversos IP públicos.  
    É escalável (numa caixa Fortigate 60F – se a empresa crescer, vai precisar de um 80 ou 200F) o Firewall do Azure você nao se preocupa com isso, ele se ajusta automaticamente no Azure.  
    Além de ser HA.
- **WAF (Web Application Firewall):**  
    Protege App Web de ações suspeitas e vulnerabilidades.

**Segmentação e Controle da Rede**

- **Network Segmentation (VNET):**  
    Impedir a comunicação de rede X para Y.  
    Acesso para rua precisa ser segmentado.
- **NSGs (Network Security Groups):**  
    Funciona como um pseudo firewall, aplicado à interface de rede ou subnet.  
    Ex.: Quero um site e quero que ele vá para a rua (V'm com IIS); para isso, criamos uma regra no NSG.  
- **Azure Bastion:**  
    Permite acesso seguro a VMs via SSH e RDP por VNET.  
    A plataforma recebe a VM para que você acesse via IP público (SSH e RDP via navegador), sem que as VMs precisem ter IP público.
- **Azure Key Vault:**  
    Recurso para armazenar senhas, certificados e credenciais.  
    Exemplo: Tenho uma aplicação que se conecta no banco de dados; para acessar as credenciais, usamos o Key Vault com uma referência de conexão (URL) – o dev não saberá a senha.  
    Via RBAC, não damos permissão para acesso direto.

---

# 10. Gestão e Conformidade de Recursos

**Controle e Configuração dos Recursos no Azure**

- **Azure Resource Locks:**  
    Implementa bloqueios para evitar que recursos sejam alterados ou deletados.  
    Ao configurar o pai, os filhos herdam:
    - Read Only: Restringe modificações.
    - CanNotDelete: Impede exclusão acidental.  
        Pode ser automatizado.  
        (Aplicável a VMs, contas de armazenamento, bancos de dados, VNet, etc.)
- **Azure Blueprints:**  
    Uma “caixinha” onde são adicionados itens de configuração para deploys – um modelo pronto que reúne:
    - Resource Group
    - Policy
    - RBAC
    - ARM Template  
        Exemplo: Se o Alberto precisa de um servidor com especificações XYZA (sql, mariaDBX, apache), crio um blueprint; sempre que necessário, pego na “caixinha” e o ambiente fica pronto (não modifica recurso / não adiciona CPU, RAM – destinado apenas para Grupos DEV, por exemplo.).
- **Azure Policy (Não faz deploy):**  
    Semelhante a GPO, para adicionar TAGs aos recursos.
    - Remediation: Ação que corrige automaticamente (quando disponível).
    - Evaluation: Verifica se os recursos estão em conformidade com a policy.

---

# 11. Soluções de Segurança e Monitoramento

**Proteção e Gestão de Postura de Segurança**

- **Defender for Cloud:**  
    Protege ambientes multinuvem (GCP, AWS) e é um CNAPP.  
    Possui modo gratuito e, em CSPM (postura de segurança), dá dicas como:  
    "Pô cara, tá sem MFA aí!", "VM sem patch de segurança", "Regra NSG muito aberta".
    - Modo pago (CSPM Plan) pode cobrar por núcleo/mês.  
        Complementa com CWPP (proteção de banco SQL, Storage, Key Vault) e DevSecOps (proteção a nível de código – PAGO).  
        Também conta com o Microsoft Cloud Security Benchmark para garantir conformidade (ISO, MS...).
- **SIEM e SOAR (Microsoft Sentinel):**  
    Coleta e correlaciona logs (SIEM) e, com base nisso, automatiza respostas (SOAR).  
    Ciclo: Coleção, detecção, investigação, resposta, automação (dados de toda a nuvem), com uso de IA, playbooks (automatização) e workbooks (painéis analíticos).
- **Security Copilot:**  
    Analisa o ambiente e direciona a ação conforme o prompt.
- **Suite 365 (Microsoft 365 Defender):**  
    Conjunto que inclui:
    - MS Defender for Office 365 (protege email, apps 365, links, anexos, OneDrive – com Service EOP em modos P1 e P2, Email Auth, Teams, SharePoint, simulação de ataques, safe links/attachments)
    - MS Defender for Endpoint
    - MS Defender for Cloud Apps
    - MS Defender for Identity
    - MS Defender Vuln Management
    - MS Defender Threat Intelligence

---

# 12. Ferramentas de Proteção de Endpoints e Identidade

**Defesa nos Endpoints e na Detecção de Ameaças**

- **Microsoft Defender for Endpoint:**  
    Por padrão, máquinas Windows já vêm com firewall e Defender antivírus, mas sem painel centralizado.  
    Protege Windows, IOS, Android e Linux com um cliente.
    - ASR (Surface Reduction): "Amigo, porque você tá com porta que permite execução do PSExec?"
    - Next Gen Protection: Atua além de um simples antivírus.
- **Microsoft Defender for Cloud App:**
    - Atua como CASB (CIS e NIST estão em conformidade para achar Shadow IT).
    - Analisa tráfego de apps para detectar o que o usuário faz “nas sombras” (ex: bloqueia Dropbox – web ou app – se for para transferir arquivos).
- **Microsoft Defender for Identity:**
    - Traz para o ambiente local o que o Entra ID Protection faz na nuvem, usando sensor (MDI) no AD DS ou AD FS para identificar riscos.
- **Vulnerability Management:**
    - “Essa máquina tá vulnerável” – verifica vulnerabilidades (em IOS, Windows, Linux) e orienta a correção com um passo-a-passo.
- **Defender TI (Threat Intelligence):**  
    Especialistas analisam vulnerabilidades; Microsoft envia para o Defender for TI em primeira mão (busca em fóruns e até na Deep Web – CVE, 0-day).
- **Defender Portal:**  
    Consolida todas as funcionalidades de proteção e monitoramento.
- **Admin Center:**  
    Exibe métricas como Secure Score (365), Compliance Manager Score, Azure Score, além de alertar para senhas fracas.

---

# 13. Consolidação de Portais de Segurança

**Portal do Microsoft Defender**

- Conjunto de tudo que se pode fazer com o Defender:  
    Incidentes/alertas (Sentinel), busca, ações, Threat Intelligence, classificação de segurança, hub de aprendizado, email/colaboração, ativos (endpoints) e apps de nuvem (CASB).
- Acesso via: security.microsoft.com

**Portal de Confiança (STP)**

- Site público com relatórios de auditoria e conformidade dos serviços da Nuvem Microsoft.
- Biblioteca com certificações, relatórios, whitepapers, artefatos e recursos setoriais.
- Exibe os 6 princípios de privacidade.

**Microsoft Priva Fam**

- Melhora a visibilidade dos dados do ambiente.
- Trata de solicitações de direito (“Quero Excluir meus Dados da minha organização”), dados confidenciais sem proteção e riscos de privacidade (ex.: arquivos não rotulados).

**Microsoft Defender XDR**

- Conjunto de ferramentas de segurança integradas:  
    X – extendida, D – detecção, R – resposta.

---

# 14. Ferramentas de Colaboração e Endpoint (Office 365)

**Microsoft for Office 365**

- Defesa para ferramentas de colaboração.
- Protege ameaças por e-mail (malware, phishing, anti-spam).
- Abrange EOP (Exchange Online Protection – modos P1 e P2), Teams, SharePoint, OneDrive e simulações/investigações de ataques.

**Microsoft Defender for Endpoint (Reforço)**

- Plataforma para proteger endpoints (PCs, Notebooks, VMs).
- Pilares:
    1. Gestão de Ameaças e Vulnerabilidade
    2. Redução da Superfície de Ataque (USB, porta aberta, ASR)
    3. Proteção Next-Gen: Não é só antivírus (use code with caution)
    4. XDR
    5. Investigação e correção automatizada
- Suportado por uma equipe global (mais de 3000 especialistas) e uma biblioteca de Threat Intelligence.

---

# 15. Microsoft Sentinel e Copilot Security

**Microsoft Sentinel**

- SIEM: Coleta e correlação de logs (mapa).
- SOAR: Automatiza a resposta baseada no SIEM.
- Ciclo: Coleção, detecção, investigação, resposta e automação (em toda a nuvem), com uso de IA.
- Inclui playbooks (automatização) e workbooks (painéis analíticos).

**Copilot (Security)**

- “For Security” – Gerencia a proteção de segurança, resposta a incidentes e correlação.
- Proporciona análise em escala e orienta sobre o que fazer por meio de prompts (Copilot sec).

---

# 16. Compliance, Governança e Proteção de Dados

**Portal da Conformidade**

- Reúne ferramentas para medir a conformidade:  
    Ambiente com ações, linhas base e políticas de alerta – quantos quiser.

**Privacy Score**

- Mede o quão seguro é o ambiente e o progresso na implantação de controles.

**Microsoft Purview**

- Conhece e analisa os dados atuais, protege com rótulos e evita perdas.
- Classificação dos dados:
    - Tipos de informações confidenciais, classificações treináveis, explorer de conteúdo e atividade.
    - Rótulos de confidencialidade (personalizável, marcação de texto, persistente, alguns grupos, confidencial, pessoas restritas).
    - Rótulo de retenção: Reter por X anos, depois excluir.

---

# 17. Gerenciamento de Registros e Risco Interno

**Gerenciamento de Registros**

- Define quem pode excluir (ex.: não e-mails) para cumprir as normas.
- Registro normativo: NÃO PODE EXCLUIR.
- Exemplo: Uma caixa de e-mail compartilhada – se usada de manhã e à noite, cria-se um registro para não excluir.

**Governança no Purview**

- No ambiente local (AD): produtores, consumidores, responsáveis pelos dados.
- Na nuvem: patrimônio, políticas e catálogo de dados, compartilhamento.

**MAPA DE DADOS**

- Mapeia e classifica os dados; funciona como catálogo para localização.

**Políticas**

- Define compartilhamento de dados com outras organizações e os controles.

**Gerenciamento de Risco Interno (IRM)**

- Ferramenta do Purview que monitora vazamentos, violações de confidencialidade e roubos.
- Aplica ações (Conditional Access) – ex.: se Fulano, descobre que será demitido e com raiva, exclui arquivos importantes de um SharePoint, o IRM dispara e bloqueia o usuário (responder).

---

# 18. eDiscovery e Auditoria

**Content Explorer**

- Identifica quais itens foram classificados (tire um snap).

**Activity Explorer**

- Mostra o que está sendo feito com os arquivos classificados.

**eDiscovery (Content Search)**

- "Quero investigar o cara" – abre-se o caso de auditoria.
    - Procura por emails e informações; os dados são jogados no eDiscovery.
    - Os acusadores impedem que se apaguem os dados.
    - Necessário para manter a cadeia de custódia (não modificação).
    - Inclui eDiscovery Premium (guardião/custódia, auditoria, registros de ações, logs e pesquisas por atividade – por padrão 90 dias, via Cmdlet, GUI ou API).
    - Auditoria Premium: Tudo, com tempo customizado e API inteligente.

---

# 19. Outros Recursos e Controles Adicionais

**Sensitive Information Types**

- Explora a atividade para mostrar informações ocorrendo.
- A política identifica informações por meio do Content Explore e Sensitive Label.

**Information Barriers**

- Exemplo: Helpdesk com o CEO – impede que determinados grupos ou usuários conversem.
- Impede que o X chame o Y (ex.: SharePoint/Teams – “não se fale”).

**Customer Lockbox**

- Exemplo: Ao abrir um chamado, você não quer que os dados sejam vistos.
- Nesse cenário, informa-se em conformidade o que será feito – sem impedir que o engenheiro atue no seu ambiente.
- ------
