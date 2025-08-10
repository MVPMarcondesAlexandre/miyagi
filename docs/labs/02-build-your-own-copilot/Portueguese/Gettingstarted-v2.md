# Desenvolva Aplicações Inteligentes com o Microsoft Copilot Stack e o Azure OpenAI

### Duração Estimada: 4 Horas

## Visão Geral

Neste laboratório, você obterá uma sólida compreensão dos fundamentos da IA Generativa, do Azure OpenAI, dos padrões de *Retrieval Augmented Generation* (RAG), do Semantic Kernel e de como aplicar esses conceitos para criar seu próprio Copilot para as necessidades do seu negócio. Você também explorará casos de uso que demonstram as experiências de produtos Copilot. Utilizando o Copilot Stack da Microsoft e exemplos práticos, este laboratório irá guiá-lo na concepção e criação de sistemas inteligentes que integrem modelos de fundação, resultando em maior produtividade e experiências de produto hiperpersonalizadas.

## Objetivo

- **Verificar e Recuperar os valores dos Recursos do Azure**: Este exercício prático visa verificar e recuperar os valores para garantir a configuração e a conectividade adequadas dos recursos do Azure.
- **Executar o aplicativo Miyagi localmente**:  Este exercício prático tem como objetivo configurar o aplicativo Miyagi, implementar o serviço de recomendações, implantar o frontend localmente, otimizar a recuperação de dados com o Azure AI Search e explorar o aplicativo e o serviço para oferecer uma experiência de usuário personalizada.
- **Containerização da interface Miyagi e do serviço de recomendações no Azure Kubernetes Service (AKS)**: Este exercício prático tem como objetivo empacotar em contêiner e implantar a interface Miyagi e o serviço de recomendações no AKS, configurando o Kubernetes, enviando imagens Docker para o ACR e verificando a implantação por meio dos endpoints de serviço.
- **Explorar e verificar a interface Miyagi e o serviço de recomendações no AKS**: Este exercício prático tem como objetivo implantar e validar a interface Miyagi e o serviço de recomendações no AKS, testando APIs e acessando a interface por meio de Ingress endpoints para garantir o funcionamento. Esse exercício aprimora a compreensão sobre gerenciamento e roteamento de tráfego em ambientes Kubernetes.
- **Expor o OpenAI por meio do API Management (APIM)**: Este exercício prático tem como objetivo validar e criar APIs no serviço de gerenciamento de APIs para atualizar a imagem Docker do serviço de recomendações, garantindo a otimização e manutenção de aplicações em contêiner. 
- **Iniciando o Desenvolvimento do Seu Próprio Copilot**: Este exercício prático tem como objetivo integrar Large Language Models (LLMs) com linguagens como C#, Python e Java, permitindo a criação de plugins facilmente encadeáveis.
  
## Pré-requisitos

Os participantes devem ter:

- Compreensão dos fundamentos de IA Generativa
- Familiaridade com o Azure OpenAI
- Experiência com o Semantic Kernel

## Arquitetura

A arquitetura do Miyagi utiliza IA para interações de usuário hiperpersonalizadas, transformando aplicações com recursos do **Semantic Kernel** e técnicas avançadas de engenharia de prompt. Ela incorpora microsserviços escaláveis e uma espinha dorsal orientada a eventos, evoluindo continuamente com novos modelos de IA. O frontend oferece experiências personalizadas semelhantes ao Microsoft Copilot.

A solução integra Azure Functions, AKS e Apache Kafka para comunicação contínua, com dados gerenciados pelo Cosmos DB e pelo Azure Storage. O Miyagi é um exemplo de aplicação inteligente e preparada para o futuro, combinando IA avançada com serviços do Azure.

## Diagrama de Arquitetura

   ![](../docs/Lab-Scenario-Preview/sk-memory-orchestration-1.png)

## Explicação dos Componentes

A arquitetura para este laboratório envolve os seguintes componentes principais:

- **Azure OpenAI**: Integra os modelos de linguagem da OpenAI na nuvem Azure da Microsoft, possibilitando soluções escaláveis de IA para processamento de linguagem natural e automação.
- **AI Search**: Serviço na nuvem que oferece recursos poderosos e flexíveis de busca, incluindo busca por texto completo e funcionalidades impulsionadas por IA.
- **Azure Functions**: Executa código em resposta a eventos sem a necessidade de gerenciar servidores, com escalabilidade automática conforme a demanda.
- **AKS (Azure Kubernetes Service)**: Serviço gerenciado de Kubernetes para orquestração e escalonamento de contêineres.
- **Apache Kafka**: Responsável pelo processamento de eventos e streaming de dados em tempo real.
- **Cosmos DB**: Banco de dados multimodelo, globalmente distribuído, com baixa latência e alta disponibilidade.
- **Azure Storage**: Armazenamento escalável para blobs, arquivos, filas e tabelas.
- **Bing Search**: Permite adicionar funcionalidades de busca do Bing aos seus aplicativos, oferecendo APIs para pesquisas na web, imagens, vídeos e notícias.

## Iniciando o laboratório

Seja bem-vindo(a) ao workshop Desenvolva Aplicações Inteligentes com o Microsoft Copilot Stack e o Azure OpenAI! Preparamos um ambiente integrado para que você explore e aprenda sobre os serviços Azure. Vamos aproveitar ao máximo essa experiência:

1. Após a configuração do ambiente, seu navegador carregará uma máquina virtual (JumpVM). Utilize esta máquina virtual ao longo do workshop para realizar o laboratório. Você pode ver os números na parte inferior do guia para alternar entre os diferentes exercícios.

   ![](../Media/gettingstartedpagenew1-v2.png)

1. Para obter os detalhes do ambiente de laboratório, pode selecionar a aba **Ambiente**. Além disso, as credenciais também serão enviadas para o seu endereço de e-mail registado. Também pode abrir o Guia do laboratório numa janela separada, selecionando **Janela dividida** no canto superior direito. Além disso, pode iniciar, parar e reiniciar máquinas virtuais no separador **Recursos**.

   ![](../Media/gettingstartedpagenew2-v2.png)

 > **Observação:** Você encontrará o valor **SUFFIX** na aba **Ambiente**; utilize esse valor sempre que vir referências a SUFFIX ou DeploymentID nas etapas do laboratório.

## Faça login no Portal Azure

1. Minimize o **Docker Desktop** clicando no botão **Minimizar**.

   ![](../Media/miyagi-image1.png)

   > **Observação:** Caso encontre o erro *WSL Update failed no Docker Desktop*, clique em **Quit** e abra novamente o aplicativo pelo Desktop.

   > **Observação:** Se aparecer a mensagem A WSL distro Docker Desktop relies on has exited unexpectedly — que geralmente ocorre quando uma entidade externa finaliza o WSL — clique no botão Restart para reiniciar.

1. Na JumpVM, clique no atalho do portal do Azure no navegador Microsoft Edge, que está na área de trabalho.

   ![](../Media/gettingstartpage3.png)

1. Na aba **Entrar no Microsoft Azure**, você verá a tela de login. Insira o seguinte e-mail ou nome de usuário e clique em **Avançar**.

     * **E-mail/Nome do Usuário**: **<inject key="AzureAdUserEmail"></inject>**

       ![](../Media/miyagi-image2.png)

1. Agora digite a senha fornecida e clique em **Entrar**.

    * **Senha**: **<inject key="AzureAdUserPassword"></inject>**

      ![](../Media/miyagi-image3.png)

   > **Observação:** Caso seja solicitado o MFA (Autenticação Multifator), siga as instruções descritas na seção Passos para configurar MFA caso a opção "Ask Later" não esteja visível.

1. Se aparecer o pop-up **Permanecer Conectado?**, selecione **Não**.

   ![](../Media/miyagi-image4.png)

1. Se uma janela pop-up **Bem-vindo ao Microsoft Azure**, selecione **Cancelar** para ignorar o tour.

   ![](../Media/miyagi-image5.png)

1. Agora que você vê o Painel do Portal do Azure, clique em **Grupos de recursos** no painel de Navegação para ver os grupos de recursos.

   ![](../Media/miyagi-image6.png)

1. Dentro de **Grupos de recursos**, clique no grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](../Media/miyagi-image7.png)

1. No grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, verifique os recursos presentes nele.

   ![](../Media/miyagi-image8.png)

## Passos para Configurar MFA Caso a Opção “Ask Later” Não Esteja Visível

   > **Observação:** Continue com os exercícios se o MFA já estiver habilitado ou a opção não estiver disponível.

1. Na tela **"Mais informações necessárias"** prompt, select **Next**.

1. On the **"Mantenha sua conta segura"** page, select **Next** twice.

1. **Observação:** Se você não tiver o aplicativo Microsoft Authenticator instalado no seu dispositivo móvel:

   - Abra **Google Play Store** (Android) ou **App Store** (iOS).
   - Procure por **Microsoft Authenticator** e instale o aplicativo.
   - Abra o aplicativo **Microsoft Authenticator**, selecione **Adicionar Conta**, então escolha **Conta corporativa ou de estudante**.

1. Um **QR code** será exibido na tela do computador.

1. No aplicativo Authenticator, selecione **Escanear código QR** e escaneie o código exibido.

1. Após escanear, clique em **Próximo** para prosseguir.

1. No telefone, insira o número mostrado na tela do computador no aplicativo e selecione **Próximo**.
       
1. Caso seja solicitado a permanecer conectado, selecione **Não**.

1. Se aparecer a janela de **Boas-vindas do Microsoft Azure**, clique em **Cancel** para ignorar o tour.
 
1. Agora clique em **Próximo** no canto inferior direito para avançar para a próxima página.

> ⚠️ **Importante:**
> **Para uma experiência mais fluida durante o laboratório prático, é fundamental ler atentamente tanto as instruções quanto as notas complementares. Isso ajudará você a realizar as tarefas com facilidade e segurança.**

## Contato de Suporte

A equipe de suporte da CloudLabs está disponível 24 horas por dia, 7 dias por semana, durante todo o ano, por e-mail e chat ao vivo, garantindo assistência contínua. Oferecemos canais dedicados tanto para alunos quanto para instrutores, assegurando que todas as suas necessidades sejam atendidas com rapidez e eficiência.

Contatos para suporte ao aluno:

- Suporte por e-mail: cloudlabs-support@spektrasystems.com.
- Chat ao vivo: https://cloudlabs.ai/labs-support

Agora, clique em Próximo no canto inferior direito para continuar para a próxima etapa.

![](./Media/next-page.png)

## Bons estudos!!
