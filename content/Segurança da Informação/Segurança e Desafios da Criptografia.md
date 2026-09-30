---
publish: true
---
Apesar de ser uma ferramenta poderosa, a criptografia não é infalível. Há vários desafios e ameaças que os especialistas em segurança devem considerar.
### Ataques de  força bruta
Um ataque de força bruta usa o método de tentativa de erro para advinhar informações de login, chaves de criptografia ou encontrar uma página da Web oculta.  Invasores trabalham com todas as combinações possíveis na esperança de acertar.
Esses ataques são feitos por "força bruta" reles utilizam tentativas excessivamente fortes para tentar "forçar" a entrada em suas contas privadas. Diferentes de outros ciberataques, que exploram vulnerabilidades de software, os ataques de força bruta utilizam poder computacional e automação para advinhar senhas ou chaves.
### Criptografia Quântica
A criptografia quântica se refere a vários métodos de cibersegurança  para criptografar e transmitir dados seguros com base nas leis naturalmente ocorrentes e imutáveis da mecânica quântica.
Computadores quânticos que estão em desenvolvimento podem resolver problemas matemáticos, como grandes números de maneira exponencialmente mais rápida que computadores normais. Os computadores quânticos podem processar dados com técnica matemáticas inacessíveis aos computadores clássicos . Isso significa que eles conseguem dar estruturas aos dados e ajudar a descobrir padrões que os algoritimos clássicos deixam passar. O risco quântico se materializará de forma assimétrica, o que significa que alguns sistemas criptográficos falharão mais cedo que outros , dependendo do projeto do algoritimo e do tamanho da chave. Ao contrário do Y2K(termo para descrever a ameaça da computação quântica aos sistemas criptográficos atuais.) não haverá um único momento em que tudo quebrará de uma só vez; em vez disso, o risco quântico será percebido ao longo do tempo, abrangendo vários anos,  à medida que diferentes sistemas criptográficos se tornem vulneráveis em momentos diferentes.
Mesmos os supercomputadores mais poderosos do mundo exigiriam milhares de anos para quebrar algoritimos de criptografia modernos, como Advanced Encryption Standard(AES) ou o RSA. 
De acordo com o algoritimo de Shor,  fatorar um número grande em um computador clássico exigiria tanto poder computacional que um hacker levaria vidas antes de se aproximar. Enquanto um computador quântico totalmente funcional. caso seja aperfeiçoado, pode potencialmente encontrar em apenas alguns minutos.
Por esse motivo, os casos para criptografia quântica são tão infinitos quanto existem casos de uso para qualquer forma de criptografia. Se algo, desde informações corporativas até segredos estatais, deve ser mantido seguro, quando a computação quântic otorna obsoletos os algoritimos criptográficos existentes. A criptografia quântica pode ser nosso único recurso para proteger dados privados.
#### Criptografia Pós-Quântica
O projeto d Post-Quantum Cryptography(PQC) do [Nist](https://csrc.nist.gov/projects/post-quantum-cryptography) lidera o esforço nacional e global para garantir a segurança eletrônica contra a futura ameaça dos computadores quânticos, máquinas que estão anos ou décadas de distancia eventualmente pode quebrar diversos sistemas que utilizam sistemas de criptografia. 
Os algoritimos de criptografia  pós-quântica são baseados em diversos problemas matemáticos que seriam difíceis de resolver tanto computadores convecionais quanto para computadores quânticos.
Essas são as seis áreas primárias da criptografia quântica segura:
- Criptografia baseada em rede
- Criptografia multivariada
- Criptografia baseada em hash
- Criptografia baseada em código
- Criptografia baseada em isogenia
- Resistência quântica de chave simétrica

### Gerenciamento de chaves
A segurança da criptografia depende do gerenciamento seguro das chaves criptográficas, perder uma chave privada pode resultar em perdas de acesso aos dados ou na impossibilidade de decriptar informações. As práticas recomendadas para o gerenciamento de chaves pe o uso de hadware seguro, como módulos de segurança de hardware(HSM) para gerar, armazenar e proteger chaves criptográficas, implementando políticas de rotação e backup das chaves.
#### Como funciona os módulos HSM para armazenamento de chaves
Os módulos impedem que um aplicativo carregue uma cópia de uma chave privada na memória de um servidor web. Isso é porque enquanto uma chave privada estiver no servidor web, ela estará vulneráveis à ataques Hackers.
Mas ao implementar o seu próprio sistema HSM ou um modelo HSM como serviço, você fecha a para hackers que tentam colocar as mãos nos dados durante a transmissão, ocorrem dentro de um HSM, onde os dados são protegidos contra invasores. A maneira como um HSM é projetado torna impossível um invasor afetar os processos que ocorrem dentro da unidade do hardware. Embora o HSM aceita entradas de usuários, eles não tem acesso ao seu funcionamento interno.
#### Tipos de módulos de segurança de hardware
##### Módulos de segurança de hardware para fins gerais
Os HSMs de uso geral usam algoritimos de criptografia comuns e são usados principalmente com carteiras de criptografia, infraestrutura de chave pública e na segurança de dados confidenciais básicos. Alguns dos algoritimos comuns que os HSMs de uso geral usam incluem CAPI, PKCS#11, CNG e outros.
##### Módulos de segurança de hardware de pagamento
Em pagamentos e transações os HSMs são projetados para proteger informações de cartões de crédito e pagamento, bem como outras informações confidenciais envolvidas nas transações financeiras. Esses tipos de HSM desempenham um papel significativo na proteção as organizações a cumprir padrões de segurança de dados do setor de cartões de pagamento (PCI DSS).

#### Opções do módulo de segurança de hardware
##### Dispositivos físicos
Embora todos os HSMs sejam dispositivos físicos, o termo "HSM físico" refere-se a uma unidade que você compra e mantém em algum lugar que escolher, como em um data center. Nesse caso você mesmo compra o HSM diretamente e lida com. sua implantação e gerenciamento durante todo o seu ciclo de vida.

##### HSMs baseados em nuvem
Um HSMs baseados em nuvem ainda é um dispositivo físico, mas é mantido em um data center na nuvem, que abriga os componentes que compõem um ambiente de nuvem. Como um HSMs baseado em nuvem, você aluga um HSM do provedor de nuvem ou paga para acessar suas funcionalidades conforme a necessidade.


### Aplicações da criptografia
A criptografia é aplicada em várias áreas para garantir a segurança e integridade dos dados
#### Comunicações seguras
-  Protocolo SSL/TLS:  usados para proteger a comunicação na web, garantindo que os dados transmitidos entre o navegador e o servidor sejam criptografados.
- Mensagens criptografas: Aplicativos de comunicação como o WhatsApp, utilizam criptografia de ponta ponta para assegurar que apenas os participantes da conversa possam ler as mensagens.
	
#### Transação financeira
- Criptografia em pagamento online: Assegura que dados sensíveis, como informações de cartão de crédito, sejam transmitidos de forma segura entre o cliente e o servidor.
- Protocolo 3D Secure: usado para autenticar transações online, adicionando uma camada extra de segurança .

####  Armazenamento de dados:
- Criptografia de discos: Protege os dados armazenados em dispositivos contra acessos não autorizados.	
- Proteção de dados em servidores: banco de dados criptografados, protegem informações sensíveis contra roubo ou acesso não autorizado
 
#### Assinaturas Digitais:
- Autenticidade e integridade: as assinaturas digitais garantem que um documento não foi alterado desde que foi assinado e que a assinatura é autêntica.
- Algoritimos usados: RSA e ECC comumente usados para criar assinaturas digitais fornecendo um meio seguro de verificação.