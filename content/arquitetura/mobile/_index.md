---
title: Arquitetura Mobile
---
## Propósito

Este documento provê uma visão geral sobre a arquitetura mobile de referência do Banco do Nordeste do Brasil (BNB).

## Acessos de Rede para Desenvolvimento

Rede Interna
https://docs.dreads.bnb/guias/desenvolvimento-mobile-interno/

Desenv. Remoto
https://docs.dreads.bnb/guias/desenvolvimento-mobile-remoto/

## Padrões

{{< hint info >}}
**Padrão Novos Projetos**

- React Native/Typescript/NodeJs
- Android (Kotlin ou Java) e iOS (Swift) nativos
- Flutter/Dart
{{< /hint >}}


{{< notice info >}}
**Padrão Novos Projetos**

- React Native/Typescript/NodeJs
- Android (Kotlin ou Java) e iOS (Swift) nativos
- Flutter/Dart
{{< /notice >}}

{{< notice  warning >}}
**Padrões Legados**

- iOS com Objective-C
{{< /notice >}}

{{< notice danger >}}
**Padrões Desenv. Descontinuados**

- Xamarim
- ionic
{{< /notice >}}

## Processo Mobile

### **Manutenção de Apps Mobile**

![fluxograma](uploads/fluxograma.png)


{{< details title="Ver mais" open=false >}}


1. **Permissões**
Todos os devs devem estar nos devidos grupos de rede  de desenvolvimento mobile e incluídos na PA do projeto

2. **Permissões Apple**
A equipe de projeto solicita via serviço a inclusão de devs e testadores nas lojas.

3. **Qualidade de código**
A equipe do projeto de desenvolvimento tem acesso aos Jobs do Sonar e devem proceder com a correção dos erros apontados, sempre que efetuarem checkin na stream de desenvolvimento.

4. **Entrega do código** Após pacote de código aceito, o analista do projeto procede com a subida do código para a stream de atendimento, e executa o Jobs Sonar VS.

5. **Testes**
Os Jobs Sonar VS irão executar nova validação de Sonar e gerar no RAM a versão que pode ser utilizada para testes nos dispositivos.
Para a Apple, testes em dispositivos (adhoc) necessitam do pré-cadastro da UUID do dispositivo na loja.

6. **Validação de Segurança**
O ASC (Ambiente de Segurança Corporativa) requer uma validação de todos as versões dos apps antes da publicação para o público.

7. **Teste pré-produção**
Os Jobs de Integração geram um pacote assinado para publicação na loja, a nível de teste Interno (Google) e TestFlight (Apple). Esses Jobs se baseiam na stream de Integração.

8. **Publicação**
A equipe de projeto cria uma publicação via RTC web, contendo pelo menos a versão do app, um resumo sobre a nova versão, e o número do relatório de Vulnerabilidades do ASC que deseja disponibilizar para o público.

{{< /details >}}

### **Processo para novos Apps Mobile**

![fluxograma2](uploads/fluxograma2.png)

{{< details title="Ver mais" open=false >}}

1. **Jobs Jenkins**
Após ter uma versão inicial “buildável” no RTC, a equipe do projeto do app pode solicitar a criação dos Jobs do Jenkins para o novo app

2. **Cadastro Rascunho App**
A equipe de projeto abre um serviço para a equipe mobile iniciar o cadastro do app na(s) loja(s) Google Play e AppStore, passando os dados necessários.
O app pré-cadastrado fica em estado de Rascunho até que todos os dados sejam salvos na loja e a primeira versão do código fique pronta e seja publicada.

3. **Liberar Back Dreads**
A equipe trabalhando remoto vai necessitar da liberação na VPN dos servidores back de desenvolvimento (dreads). Isso pode ser feito pela equipe de projeto, através da configuração do Https do servidor e da abertura de uma Mudança (Demandas Internas).

4. **Identidade Visual**
A equipe de projeto solicita pra equipe de criação a definição da identidade visual do aplicativo (ícone, banners, etc), conforme os padrões das lojas e do BNB.

5. **Funcionário Responsável pelo app**
A equipe de projeto define um responsável para finalizar o preenchimento dos dados (imagens, descrição, resumo, links) do app, abrindo um serviço para que a equipe mobile conceda o acesso.
Esse responsável definido, pode ter acesso também aos relatórios de estatísticas do app e também à comunicação que a loja disponibilizar sobre pendências do app.

{{< /details >}}

## Opções arquiteturais

Para o desenvolvimento de aplicativos mobile do BNB, são possíveis os seguintes tipos de arquitetura: aplicativo nativo, aplicativo nativo-híbrido, aplicativo web-híbrido e aplicativo web (ver Figura 1). A seguir, são escritas sucintamente as características essenciais de cada uma.

![figura1](uploads/tiposDeArquiteturaMobile.png)

{{< tabs "1" >}}

{{< tab "Aplicativo Nativo" >}}

Executa diretamente sobre a plataforma mobile. Ele tende a ter bom desempenho e alta capacidade de controle dos itens de segurança, assim como acesso total aos recursos do dispositivo.
O aplicativo acessa recursos nativos diretamente por meio da API nativa ou por meio de uma camada de abstração construída sobre a API nativa. Por ex.: Um app desenvolvido diretamente com SDk do Android ou do iOS, ou um app criado com um framework multiplataforma, como o ReactNative, que compila para um aplicativo nativo.
{{< /tab >}}
{{< tab "Aplicativo web" >}}
Possui apenas código web e executa em um Browser. Ele possui alta portabilidade, facilidade e agilidade na publicação de atualizações e agilidade em caso de necessidade de mudança arquitetural. Um de seus principais pontos negativos é a baixa capacidade de acessar recursos do dispositivo, como câmera e GPS (essa capacidade vai depender do suporte de cada browser), e a impossibilidade de disponibilização dele via lojas públicas de aplicativos (Play Store e App Store). Por ex: Um site web desenvolvido com html ou asp com css compatível com mobile.
{{< /tab >}}
{{< tab "Aplicativo web-hibrido" >}}

Possui essencialmente código web que executa em uma WebView (componente nativo). Essa arquitetura tende a possuir características similares às da aplicação web, com o adicional de presença nas lojas de aplicativos mobile. Deve-se atentar que o acesso aos recursos de segurança é mais limitado do que em apps nativos ou nativo híbridos.
{{< /tab >}}
{{< tab "Aplicativo nativo-hibrido" >}}

Possui código nativo, que executa diretamente sobre a plataforma mobile, e código web, que executa em uma WebView (componente nativo). Ele possibilita uma ampla gama de possibilidades, pois possui código nativo e web, embora também seja a arquitetura mais complexa das quatro. Por ex.: BNB Mobile, desenvolvido originalmente em asp, com comunicação para recursos nativos, e funcionalidades desenvolvidas nativamente como o Login, leitor de código de barras que acessam recursos nativos.

{{< /tab >}}
{{< /tabs >}}

## Escolha arquitetural

Para cada situação, é necessário analisar as características desejadas da aplicação para, dessa forma, identificar a arquitetura mais indicada. Levantamos aqui algumas situações que servirão para nortear a escolha arquitetural da aplicação a ser desenvolvida.

Caso haja um site pré-existente que possa ser reutilizado e haja interesse em reutilizá-lo, podemos identificar as seguintes situações:

- Se a aplicação não exigir publicação nas lojas de aplicativos, tiver como requisito ser on-line e não possuir a necessidade de acessar recursos nativos do dispositivo, a recomendação é a criação de um aplicativo web.

- Se a aplicação exigir publicação nas lojas de aplicativos, a recomendação é:
  - A criação de um aplicativo web-híbrido caso não haja necessidade de se acessar recursos nativos;
  - A criação de um aplicativo nativo-híbrido nos demais casos.

Caso a aplicação não tenha a necessidade de acessar recursos nativos do dispositivo, não possua restrições relevantes de segurança, tenha como requisito ser on-line e não exija publicação nas lojas de aplicativos, recomendamos a criação de um aplicativo web. Caso exija publicação nas lojas de aplicativos, recomendamos a criação de um aplicativo web-híbrido.

Caso a aplicação tenha como alvo apenas uma plataforma, a indicação é a criação de uma aplicação nativa.

Caso a aplicação tenha alta necessidade de desempenho e segurança, a recomendação é criar uma aplicação nativa ou nativa-híbrida.

Para os demais casos, recomendamos a criação de uma aplicação nativa-hibrida ou hibrida.

Essa é uma orientação geral que deve ser seguida, mas em determinados casos pode ser interessante a avaliação dos requisitos específicos do aplicativo a ser criado para a melhor tomada de decisão. Nesses casos, a decisão deve ser tomada em conjunto com a Célula de Arquitetura.

## Arquitetura de Referência Mobile

* [Mobile & Integrações](https://docs.dreads.bnb/arquitetura/mobile/testando-o-mermaid/)

## Escolha das Tecnologias

{{< tabs "2" >}}
{{< tab "Aplicativo Nativo" >}}

No caso de arquitetura nativa é importante identificar a quantidade de plataformas-alvo. Caso seja apenas uma plataforma-alvo, recomendamos o desenvolvimento com SDKs nativos (usando Android SDK e iOS SDK). Nesse caso, também é possível o desenvolvimento com React Native, caso a expertise dos desenvolvedores seja na plataforma web.

Caso haja mais de uma plataforma-alvo ou haja previsão de suporte para mais de uma plataforma, o desenvolvimento deve ser realizado utilizando o React Native.

No caso de desenvolvimento nativo, deve ser utilizado Android Studio + Java ou Kotlin para desenvolvimento para Android e XCode + Swift para desenvolvimento para iOS (ou XCode + Objective-C caso seja um projeto de manutenção de legado feito em Objective-C). No desenvolvimento com React Native, deve ser utilizada a linguagem typescript e o Visual Studio Code.
{{< /tab >}}

{{< tab "Aplicativo nativo-hibrido" >}}

No caso de aplicativo com arquitetura nativa-híbrida, há essencialmente dois tipos de código, o nativo e o web. Para o código nativo, a recomendação é a mesma do aplicativo com arquitetura nativa. Para o código web, devem ser utilizadas as linguagens HTML5, CSS3 e JavaScript. O código web pode ser um site armazenado localmente no dispositivo (site local) ou um site remoto hospedado em um servidor WAS ou IIS. Para o código web deve-se seguir os padrões de desenvolvimento web do BNB.

O acesso a recursos nativos do dispositivo (câmera, base de dados, GPS, ...) pelo código web deve ser através do código nativo, ou seja, o código web chama o código nativo e este chama o componente nativo e, após o recebimento do retorno, o código nativo passa esse retorno para a o código web.
{{< /tab >}}

{{< tab "Aplicativo web-hibrido" >}}

Um aplicativo web-híbrido deve ser desenvolvido utilizando as linguagens HTML5, CSS3 e JavaScript. O código web pode ser um site armazenado localmente ou um site remoto hospedado em um servidor WAS ou IIS. Para o código web deve-se seguir os padrões de desenvolvimento web do BNB.

Para a criação do build para as plataformas-alvo, devem ser utilizadas as mesmas ferramentas do aplicativo nativo.

{{< /tab >}}
{{< tab "Aplicativo web" >}}

Um aplicativo web deve ser desenvolvido utilizando as linguagens HTML5, CSS3 e JavaScript. O código web deve ser um site remoto hospedado em um servidor WAS ou IIS. Para o código web deve-se seguir os padrões de desenvolvimento web do BNB.

{{< /tab >}}

{{< /tabs >}}

### Banco de dados
  - Caso a aplicação necessite utilizar um banco de dados local, deve ser utilizado o SQLite com uso de um ORM (Core Data para iOS, Room para Android) ou o Realm DB


### Serviços

  - A implementação de serviços web a serem acessados pelo mobile devem do tipo REST e devem seguir os padrões de desenvolvimento web do BNB

### Segurança
  - **Https e ssl pinning:**
    O SSL Pinning é uma verificação que o aplicativo faz para verificar se o servidor com quem ele se comunica é confiável. Para isso ele verifica se o certificado recebido do servidor é o certificado que ele espera, o qual está armazenado localmente dentro do app.
    Para acesso a páginas e serviços do BNB, é obrigatório o uso de conexão segura (https) e, preferencialmente, o uso de ssl pinning (<https://owasp.org/www-community/controls/Certificate_and_Public_Key_Pinning>).
  - **Ofuscação:**
    É recomendada a aplicação de ofuscação (<https://owasp.org/www-community/controls/Bytecode_obfuscation>)( <http://s2ramg01:9080/ram/oslc/assets/7A4E9CB9-270A-E6BA-B593-7511221EFB93/1.0>) nos apps mobile para evitar o processo de engenharia reversa e análise do código dos apps. Para código nativo iOS, essa ofuscação não é necessária, pois o processo padrão de geração de builds do IOS já gera um pacote ofuscado.
  - **Deteção de Root/Jailbreak:**
    É recomendada a detecção de root/jailbreak dos dispositivos móveis que estejam executando apps do BNB. Caso seja detectado, é orientado um tratamento adequado, como bloquear o uso do app ou apenas alertar o usuário, conforme definição do projeto junto ao Ambiente de Segurança Computacional.


## Integração contínua

O processo e os detalhes referentes à integração contínua estão descritos nos documentos específicos de cada plataforma:

- Padrão de desenvolvimento [Android](/arquitetura/mobile/android/)
- Padrão de desenvolvimento [IOS](/arquitetura/mobile/ios/)
- Padrão de desenvolvimento [ReactNative](/arquitetura/mobile/react-native/)

## Jobs do Jenkins

Antes da implantação, para os testes e homologação do aplicativo, é recomendado que a equipe do sistema solicite a criação dos Jobs à equipe de Arquitetura Mobile.
Segue os tipos de Jobs para mobile:

{{< tabs "3" >}}
{{< tab "(Fábrica / Desenv)" >}}

Padrão: NomeComponente – Android – SXXX_ATD_XXXXXX_fabrica – Sonar
        NomeComponente – iOS – SXXX_ATD_XXXXXX_fabrica – Sonar

ex: S400_Digital_Mobile - Android - S400_ATD_509589_fabrica - Sonar VS

  - É executado automaticamente a cada incremento no RTC
  - Deve rodar a target do ambiente de Fabrica / Desenvolvimento (dev)
  - Assina com certificado ad hoc no caso do iOS (que possibilita instalar diretamente no dispositivo habilitado)
  - Faz build e roda sonar

{{< /tab >}}

{{< tab "(Atendimento - ATD)" >}}

Padrão: NomeComponente – Android – SXXX_ATD_XXXXXX – SonarVS
        NomeComponente – iOS – SXXX_ATD_XXXXXX – SonarVS

ex: S400_Digital_Mobile - iOS - S400_ATD_509589 - Sonar VS

  - É executado automaticamente a cada incremento no RTC
  - Deve rodar a target de Desenvolvimento (dev)
  - Assina com certificado ad hoc
  - Faz build e roda sonar

Padrão: NomeComponente – Android – SXXX_ATD_XXXXXX – Homolog - SonarVS
        NomeComponente – iOS – SXXX_ATD_XXXXXX – Homolog - SonarVS

ex: S400_Digital_Mobile - iOS - S400_ATD_509589 - Homolog - Sonar VS

  - Deve rodar a target de homologação (homolog/staging)
  - Aponta para os servidores de Homologação
  - Assina com certificado ad hoc
  - Faz build e roda sonar
  - Envia o binário para o RAM


Padrão: NomeComponente – Android – SXXX_ATD_XXXXXX – UserTest - SonarVS
        NomeComponente – iOS – SXXX_ATD_XXXXXX – UserTest - SonarVS

ex: S400_Digital_Mobile - iOS - S400_ATD_509589 – UserTest - Sonar VS

  - Deve rodar a target de Teste (test) apontando pros servidores de Teste
  - Assina com certificado ad hoc
  - Faz build e roda sonar
  - Envia o binário para o RAM

{{< /tab >}}

{{< tab "(Integração)" >}}

Padrão: NomeComponente – Android – SXXX – SonarIntegra
        NomeComponente – iOS – SXXX – SonarIntegra

ex: S400_Digital_Mobile - iOS - S400 - Sonar Integra

  - Sua execução é disparada automaticamente
  - Faz build e roda sonar
  - Deve rodar a target de produção


Padrão: NomeComponente – Android – SXXX – ASC
        NomeComponente – iOS – SXXX – ASC

ex: S400_Digital_Mobile – Android - S400 – ASC

  - Gera binários para análise de Vulnerabilidades do ASC
  - az build a partir da stream de integração
  - Envia para o RAM (atendimento) – Ativo especifico da Segurança
  - Assina com certificado ad hoc (para os testes no dispositivo)
  - Não roda Sonar
  - Deve rodar a target de homologação, se não existir: teste ou dev


Padrão: NomeComponente – Android – SXXX – GooglePlay
        NomeComponente – iOS – SXXX – TestFlight

ex: S400_Digital_Mobile - iOS - S400 - TestFlight
    S400_Digital_Mobile - Android - S400 - Google Play

  - Deve rodar a target de produção
  - Usa assinatura da loja
  - Faz build, mas não roda sonar
  - Envia para o RAM e para a loja de apps, para teste interno e testFlight

{{< /tab >}}
{{< /tabs >}}

| Tipo Job | Build Ambiente | Sonar | Enviar RAM? | Envia Loja? | Stream RTC |
| --- | --- | --- | --- | --- | --- |
|**Integração**|Produção (Flavor/Target:Prod)| Não realiza|Integração|Google Play/ Test Flight|Integração SXXX|
|**Validação ASC**| Desenv &#124; Testes &#124; Hom+Prod<br> (Dev &#124; Test &#124; Hom+Prod)|Não realiza|ASC|Não|Integração SXXX|
|**SonarVS**|Desenv+Prod (Flavor/Target:Test)|SonarVS|Atendimento|Não|Atendimento SXXX_ATD_XXXXXX|
|**SonarVS Teste**|Teste (Flavor/Target:Test)|SonarVS|Atendimento|Não|Atendimento SXXX_ATD_XXXXXX|
|**Sonar VS Homolog**|Homolog (Flavor/Target:homolog)|Sonar VS|Atendimento|Não|Integração SXXX|
|**Sonar**|Desenv (Flavor/Target:Dev)|Sonar|Não|Não|Fábrica ou Desenv SXXX_ATD_XXXXXX_fabrica SXXX_ATD_XXXXXX_desenv|

## Publicação

Destacamos aqui alguns passos de preparação para a aplicação que será implantada pela primeira vez, ou será atualizada:

### Preparação para uma primeira publicação

- O responsável do BNB pela aplicação deverá solicitar via Publicação do RTC os seguintes itens:
  - Preparação dos pré-requisitos de publicação, incluindo:
    - A criação das credenciais de publicação (iOS / Android), caso não tenham sido criadas ainda.
    - A criação do app e configuração dos dados do app nas lojas (nome, descrição, imagens, url de privacidade, ...) ou liberação de acesso nas lojas para que o próprio responsável pela aplicação ou o marketing mesmo possa alterar os dados da aplicação (exceto permissão para publicar em produção)

- Em seguida, a equipe mobile da Célula de Arquitetura deverá:
  - Criar as credenciais (senhas / certificados) de publicação (iOS / Android) caso elas ainda não existam.
  - Versionar os certificados Android no RTC (de acordo com o definido na integração contínua)
  - Salvar as senhas no repositório de credenciais do S095 (S095 – Gestão de Credenciais e Senhas).
  - Criar e configurar os dados do app nas lojas ou liberar o acesso nas lojas ao responsável do BNB pela aplicação (exceto permissão para publicar em produção)

- Obs.: caso a aplicação a ser publicada seja contratada pelo BNB, o Banco não tenha acesso ao código fonte e a app tenha que ser publicada na loja pública do BNB, o procedimento a ser realizado deverá ser o seguinte:
  - Compartilhamento das credenciais de assinatura através do envio dos certificados de assinatura por e-mail e do compartilhamento das senhas por telefone.


### Publicações de Manutenção

Após a etapa de preparação e testes, poderá ser realizado o processo de geração dos binários a serem implantados, que é o mesmo para uma primeira publicação ou atualização do aplicativo, e que consiste nas seguintes etapas:

- **Aplicação desenvolvida pelo BNB/fábrica:**
  - O responsável do BNB pelo sistema deverá:

    - Versionar as alterações na stream de atendimento do RTC
    - Subir as alterações até a stream de integração
    - Enviar versão para [Análise de Vulnerabilidades](https://docs.dreads.bnb/arquitetura/mobile/#an%c3%a1lise-de-vulnerabilidades)
    - Executar o job de integração para geração do binário publicável no RAM (obs. O job de integração já poderá publicar diretamente nos ambientes de teste das lojas, Teste Interno para Google Play e TestFlight para AppStore)
    - Criar uma [Publicação no RTC](https://docs.dreads.bnb/arquitetura/mobile/#cria%c3%a7%c3%a3o-da-publica%c3%a7%c3%a3o-no-rtc)

- **Aplicação contratada (sem acesso a código fonte e com publicação nas lojas públicas do BNB):**
  - A empresa responsável deverá:
    - Enviar os binários por e-mail para equipe responsável do sistema
  - A equipe do Sistema deverá:
    - Enviar a versão para para [Análise de Vulnerabilidades](https://docs.dreads.bnb/arquitetura/mobile/#an%c3%a1lise-de-vulnerabilidades)
    - Subir o binário do aplicativo para o RAM
    - Criar uma [Publicação no RTC](https://docs.dreads.bnb/arquitetura/mobile/#cria%c3%a7%c3%a3o-da-publica%c3%a7%c3%a3o-no-rtc)


**ATENÇÃO:** Qualquer publicação de aplicativo mobile em produção deverá passar primeiramente pela avaliação da equipe de Segurança – ASC. 

#### Análise de Vulnerabilidades

![vulnerabilidade](uploads/vulnerabilidade.png)

##### Envio para o Ambiente de Segurança (ASC)

- A cada nova versão do App
- O prazo para analise é de até 5 dias
- Solicitação via Demandas Internas
  - Criação de uma *Solicitação* no *Demandas Internas* (http://demandasinternas) utilizando a *área de solicitação* *AMBIENTE DE SEGURANÇA CORPORATIVA.SEGURANÇA DA INFORMAÇÃO.ANALISE DE VULNERABILIDADE*

##### Preparação do Ambiente

- Versão gerada preferencialmente a partir da Stream de Integração através do
  - Job Jenkins ASC

- Versão apontando para um serviço
  - Back-end de desenvolvimento, testes ou homologação

### Criação da Publicação no RTC

 Após a geração dos binários, e análise de vunerabilidades realizada, poderá ser realizada a implantação propriamente dita:

- O responsável pelo sistema deverá:
  - Criar uma *Publicação* no *RTC* na PA de *Serviços* solicitando a publicação do aplicativo (na lista de materiais deve ser informado “Arquitetura Mobile / Aplicativo Mobile”) informando os dados de publicação:
    - Versão do app
    - Novidades da versão
    - Imagens e outros itens
    - Um comentário do analista sobre o retorno da avaliação de vulnerabilidades, feita pelo ASC e se aprova a publicação ou não.
    - Checklist preenchido:
      - A versão a ser publicada em loja:
        1. [  ] tem origem na na stream do RTC de integração?
        2. [  ] passou por análise de Vulnerabilidades do ASC? (Favor incluir comentário sobre o retorno do ASC).
        3. [  ] passou por homologação da equipe/usuários do projeto?
        4. [  ] foi avaliada em beta? (TestFlight no iOS) ou (Teste Interno/Alfa/Beta no Android)?

  - A equipe mobile da Célula de Arquitetura deverá realizar a publicação do app nas lojas e mudar o status do app no RAM para publicado.

Cada aplicativo submetido para produção será analisado pela sua devida loja e estará sujeita ao tempo de avaliação definido por elas. A equipe mobile acompanhará o status até a aprovação da versão submetida.
