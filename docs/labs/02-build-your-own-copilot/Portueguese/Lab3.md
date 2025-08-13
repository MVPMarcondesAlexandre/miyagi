# Laboratório 4 – Expor o OpenAI por meio do Serviço de Gerenciamento de API do Azure (APIM)

### Duração: 60 minutos

Neste laboratório, você se aprofundará na configuração e verificação de APIs no Gerenciamento de API do Azure (APIM), com foco na integração do serviço Azure OpenAI. Isso envolve a configuração de APIs HTTP, a garantia da configuração correta e a obtenção de uma URL de gateway para acesso externo e integração perfeitos. Você também explorará a criação de políticas, a definição de funções (roles) e o gerenciamento de assinaturas para operar as APIs de forma segura. Este laboratório destaca as melhores práticas em gerenciamento de API, garantindo autenticação, autorização e testes operacionais robustos dentro do ecossistema abrangente do Azure.

## Objetivos do Laboratório

Você será capaz de completar as seguintes tarefas:

- Tarefa 1: Verificar o serviço de Gerenciamento de API implantado e criar uma API.
- Tarefa 2: Criar Políticas e Funções no Gerenciamento de API.
- Tarefa 3: Atualizar a Imagem Docker para o serviço de Recomendação.
- Tarefa 4: Revisão do serviço de Recomendação no AKS.
- Tarefa 5: Configurar logs no Hub de Eventos e validar os dados de entrada.

### Tarefa 1: Verificar o serviço de Gerenciamento de API implantado e criar uma API

Nesta tarefa, você configurará uma API HTTP dentro do Gerenciamento de API do Azure para interagir com o serviço Azure OpenAI. Isso garante que a API esteja configurada corretamente e fornece uma URL de gateway para acesso externo e integração com outros serviços.

1. Navegue até ao portal do Azure, abra o **Grupo de Recursos** chamado **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** e selecione o serviço de Gerenciamento de API **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** na lista de recursos.

   ![](../Media/miyagi-image54.png)

1. No serviço de Gerenciamento de API **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, clique em **APIs** **(1)** em **APIs** no menu esquerdo e selecione **HTTP** **(2)** em **Definir uma nova API** para criar uma API HTTP.

   ![](../Media/miyagi-image55.png)

1. No painel **Create an HTTP API**, insira os seguintes valores:

    | **Parâmetro** | **Valores** |
    | -------------------- | -------------------- |
    | Tipo de API **(1)** | **Basic** |
    | Display name **(2)** | **miyagi-api** |
    | Name **(3)** | **miyagi-api** |
    | Web service URL **(4)** | Insira o Endpoint do Azure OpenAI **<inject key="OpenAIEndpoint" enableCopy="true"/>** |
    | API URL suffix **(5)** | **openai** |
    | Clique on **(6)** | **Create** |

    ![](../Media/miyagi-image56.png)

1. Assim que a API for criada, clique em **Visão Geral** **(1)** e copie o **URL da gateway** **(2)** do serviço de Gerenciamento de API. Guarde a **URL**, pois você precisará dela em uma tarefa futura.

   ![](../Media/miyagi-image57.png)

    > **Parabéns** por concluir a tarefa! Agora, é hora de validá-la. Siga os passos:
    > - Clique no botão Validar para a tarefa correspondente.
    > - Se receber uma mensagem de sucesso, pode avançar para a tarefa seguinte. Caso contrário, leia atentamente a mensagem de erro e repita o passo, seguindo as instruções do guia do laboratório.
    > - Se precisar de ajuda, contacte-nos através do e-mail labs-support@spektrasystems.com. Estamos disponíveis 24 horas por dia, 7 dias por semana para o ajudar.

 <validation step="f0747771-c830-4f46-8e46-2531ad40214a" />

### Tarefa 2: Criar Políticas e Funções no Gerenciamento de API

Neste laboratório, você configurará políticas de API, definirá funções e assinaturas, e integrará a API do Serviço OpenAI do Azure dentro do Gerenciamento de API do Azure. Isso garante a autenticação, autorização e testes operacionais adequados dos endpoints da API.

1. No serviço de Gerenciamento de API **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, no painel de navegação esquerdo, na seção **APIs**, selecione **APIs** **(1)**, clique nos **três pontos** **(2)** ao lado de `miyagi-api`, selecione **Import** **(3)** e clique em **OpenAPI** **(4)**.

   ![](../Media/miyagi-image58.png)

1. No pop-up **Import from OpenAPI specification**, cole o link abaixo na caixa de texto **OpenAPI specification (1)** e clique em **Import** **(2)**.

    ```
    https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json
    ```

   ![](../Media/miyagi-image59.png)

1. Agora deverá ver uma série de APIs.

   ![](../Media/miyagi-image60.png)

1. Em **All APIs**, na API **Azure OpenAI Service API**, navegue até a aba **Settings**, na seção **Subscription**, atualize a configuração do **Helder name** para **api-key** **(1)** e clique em **Save** **(2)**.

   ![](../Media/miyagi-image61.png)

1. No serviço de Gerenciamento de API, **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** em **APIs**, clique em **Produtos** **(1)** e selecione **+ Adicionar** **(2)**.

   ![](../Media/miyagi-image62.png)

1. Na janela **Adicionar produto**, especifique **Nome de exibição** como **OpenAi** **(1)**, **Descrição** como **OpenAI** **(2)* *. No menu **APIs**, clique no sinal de mais** **(3)** selecione **Azure OpenAI Service API** **(4)** e pressione Enter e por fim, clique em **Criar** **(5)**.

   ![](../Media/api-product2.png)

1. No serviço de Gerenciamento de API **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, em **APIs**, selecione **Assinaturas** **(1)** e clique em **+ Adicionar assinatura** **(2)**.

   ![](../Media/miyagi-image63.png)

1. No Janela **Nova assinatura**, forneça **Nome** como **aoai-test** **(1)** e **Nome de exibição** como **AOAI Test** **(2)** e clique em **Criar** **(3)**.

   ![](../Media/miyagi-image64.png)

1. Assim que a assinatura **Teste AOAI** for criada, clique nos **três pontos** **(1)** junto ao **Teste AOAI** e depois clique em **Mostrar\ocultar chaves** **(2)**. Copie a **Chave primária** **(3)** e guarde-a para mais tarde.

   ![](../Media/miyagi-image(65).png)

1. Navegue até **Azure OpenAI** no Portal Azure, selecione o **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**.

1. Em **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**, selecione **IAM (Controle de acesso)** **(1)**, clique em **+ Adicionar** **(2)** e selecione **Adicionar atribuição de função** **(3)**.

   ![](../Media/miyagi-image66.png)

1. Na página **Adicionar atribuição de função**, pesquise e selecione **Usuário dos Serviços Cognitivos (1) (2)**, clique em **Próximo (3)**.

   ![](../Media/apinew3.png)

1. Na aba **Membros**, selecione **Identidade gerenciada** **(1)**, clique em **+ Selecionar membros** **(2)**.

   ![](../Media/miyagi-image82.png)

1. Na janela à direita, **Selecionar as identidades gerenciadas** em **Assinatura (1)**, aceite o valor padrão. Em **Identidade gerenciada**, selecione **Serviço de Gerenciamento de API** **(2)**, escolha **miyagi -apim-<inject key="DeploymentID" enableCopy="false"/>** **(3)** e clique em **Selecionar** **(4)**.

   ![](../Media/miyagi-image(68).png)

1. Clique em **Próximo**.

1. Na aba **Examinar + atribuir**, clique em **Examinar + atribuir**.

1. Navegue de volta para o **serviço de Gerenciamento de API** no Portal Azure e selecione o **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**.

1. No **serviço de Gerenciamento de API**, selecione **APIs** **(1)**, clique na API **Azure OpenAI Service API** **(2)**, selecione **All operations** **(3)** e clique em **Policies**</> **(4)** em **Inbound processing**.

   ![](../Media/api-inbound.png)

1. No editor de código, copie a política abaixo para sobrescrever apenas as tags **inbound** **(1)**, substitua por **&lt;&lt;Azure_OpenAI_Endpoint&gt;&gt;** **<inject key=" OpenAIEndpoint " enableCopy="true"/>** **(2)** que você copiou na Tarefa 1, Passo 4 e clique em **Save** **(3)**.

      ```
      <inbound>
         <base />
         <set-header name="api-key" exists-action="delete" />
         <authentication-managed-identity resource="https://cognitiveservices.azure.com" output-token-variable-name="msi-access-token" ignore-error="false" />
         <set-header name="Authorization" exists-action="override">
            <value>@("Bearer " + (string)context.Variables["msi-access-token"])</value>
         </set-header>
         <set-backend-service base-url="https://<<Azure_OpenAI_Endpoint>>/openai" />
      </inbound>
      ```


   ![](../Media/api-inbound1.png)

    >**Observação**: Por favor, certifique-se de colar os valores do **OpenAIEndpoint** e eliminar qualquer duplicação de **https://**.

1. No Serviço de Gerenciamento de API, clique em **Test** **(1)**, selecione **Creates a completion for the chat message** **(2)**, introduza o nome de implementação gpt-4 **<inject key="CompletionModel" enableCopy="true"/>** **(3)** no campo de `deployment-id`, insira **2023-05-15** **(4)** em `api-version`.

   ![](../Media/new-api-test.png)

1. Role para baixo até a seção **Request body (1)**, substitua o código existente pelo código abaixo e clique em **Send** **(2)**.

    ```
    {"model":"gpt-4","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
    ```

   ![](../Media/new-api-body.png)

1. Role a resposta para baixo e você deverá ver uma resposta `200` e uma mensagem de volta do seu serviço OpenAI.

   ![](../Media/new-api-result.png)

### Tarefa 3: Atualizar a Imagem Docker para o serviço de Recomendação

Nesta tarefa, você atualizará a configuração do serviço de recomendação, reconstruirá a imagem Docker, a enviará para o ACR e garantirá que a imagem atualizada esteja pronta para implantação no ambiente Azure.

1. Navegue até ao Visual Studio Code, expanda o diretório **miyagi/services (1)/recommendation-service (2)/dotnet (3)** e selecione o arquivo **appsettings.json (4)**.

   ![](../Media/open-appsettings.png)

1. No arquivo `appsettings. json`, você deve substituir o valor de **endpoint** do **recurso OpenAI** pela **URL do Gateway de API** que você copiou na Tarefa 1, Passo 4, o valor **apiKey** pela **chave de assinatura** que foi copiada na Tarefa 2, Passo 9 e salve o arquivo.

   ![](../Media/miyagi-image(72).png)

1. Retorne para o **Visual Studio Code**, navegue até a pasta **miyagi/services (1)/recommendation-service (2)/dotnet (3)**, clique com o botão direito em `dotnet` e selecione **Abrir no terminal Integrado**.

   ![](../Media/aks-04.png)

1. Agora, você precisa reconstruir a imagem docker para o serviço de recomendação executando o comando docker abaixo. Certifique-se de usar o mesmo nome da imagem docker que foi criada anteriormente.

    ```
    docker build . -t miyagi-recommendation
    ```

    >**Observação**: Este comando cria uma imagem Docker chamada Miyagi-recommendation a partir do Dockerfile e dos arquivos associados no diretório atual.

1. Execute o seguinte comando para fazer login no ACR.

    > **Observação**: Substitua **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**, **[uname]** por **<inject key= " AcrUsername" enableCopy="true"/>** e **[password]** com **<inject key="AcrPassword" enableCopy="true"/>**.

    ```
    docker login [ACRname] -u [uname] -p [password]
    ```

    >**Observação**: O comando `docker login [ACRname] -u [uname] -p [password] é usado para autenticar seu cliente Docker com o Azure Container Registry (ACR) especificado, utilizando o nome de usuário e a senha fornecidos. Essa autenticação é necessária para executar operações como enviar (push) e baixar (pull) imagens de contêiner para e a partir do ACR.

1. Execute o seguinte comando para adicionar a tag.

    > **Observação**: Substitua **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**.

    ```
    docker tag miyagi-recommendation:latest [ACRname]/miyagi-recommendation:latest
    ```

    >**Observação**: O comando `docker push [ACRname]/miyagi-recommendation:latest` envia uma imagem Docker da sua máquina local para o Azure Container Registry (ACR) especificado. Ao executar esse comando, você disponibiliza a imagem miyagi-recommendation:latest no ACR, permitindo que ela seja utilizada em diversos deployments e serviços dentro do Azure.

1. Depois de fazer login no ACR, execute o comando abaixo para enviar a imagem docker atualizada para o registro de contêiner.

    >**Observação**: certifique-se de que substitui **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**.

    ```
    docker push [ACRname]/miyagi-recommendation:latest
    ```

    >**Observação**: O comando `docker push [ACRname]/miyagi-recommendation:latest` envia a imagem Docker miyagi-recommendation:latest para o Azure Container Registry (ACR) especificado. Isso torna a imagem disponível no ACR para uso em implantações (deployments) e outras operações.

### Tarefa 4: Revisão do serviço de recomendação do AKS

Nesta tarefa, você gerenciará o ciclo de vida da implantação do serviço de recomendação no Azure Kubernetes Service (AKS), incluindo o início e a parada do serviço, bem como a verificação de sua funcionalidade após a revisão.

1. Navegue até o portal do Azure, abra o Grupo de Recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** e selecione  o serviço Kubernetes **env-miyagi-<inject key=" DeploymentID" enableCopy="false"/>**.

   ![](../Media/miyagi-image73.png)

1. Na aba Visão geral do serviço Kubernetes **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>**, clique no botão **Parar** e depois em **Sim**.

   ![](../Media/miyagi-image74.png)

    > **Observação**: Aguarde até que o serviço Kubernetes seja completamente parado.

1. Na aba Visão geral, **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>** no painel de serviço Kubernetes, clique no botão **Iniciar**.

   ![](../Media/miyagi-image75.png)

1. Assim que o serviço Kubernetes for iniciado, selecione **Serviços e regras de entradas** em **Recursos do Kubernetes** e clique em **IP externo** do serviço de recomendação miyagi.

   ![](../Media/miyagi-image76.png)

1. Isto irá navegar numa nova aba com a página web **miyagi-recommendation-service**.

   ![](../Media/miyagi-image77.png)

### Tarefa 5: Configurar logs no Hub de Eventos e validar os dados de entrada

Nesta tarefa, você configurará o logging do Hub de Eventos para o Gerenciamento de API, configurando os componentes necessários no Azure, implantando a configuração de logging usando um template Bicep e validando a integração através de testes e monitoramento.

1. No portal do Azure, pesquise e selecione **Hubs de Eventos**, e selecione **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](../Media/miyagi-image78.png)

1. No Namespace do Hub de Eventos **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, no menu esquerdo selecione **IAM (Controle de acesso)** **(1)** , clique em **+ Adicionar** **(2)** e selecione **Adicionar atribuição de função** **(3)**.

   ![](../Media/miyagi-image79.png)

1. Na página **Adicionar atribuição de função**, pesquise e selecione **Remetente de Dados dos Hubs de Eventos do Azure (1) (2)**, clique em **Próximo (3)**.

   ![](../Media/miyagi-image80.png)

1. Na aba **Membros**, selecione **Identidade gerenciada** **(1)**, clique em **+ Selecionar membros** **(2)**.

   ![](../Media/miyagi-image82.png)

1. Na janela à direita, **Selecionar as identidades gerenciadas** em **Assinatura (1)**, aceite o valor padrão. Em **Identidade gerenciada**, selecione **Serviço de Gerenciamento de API** **(2)**, escolha **miyagi -apim-<inject key="DeploymentID" enableCopy="false"/>** **(3)** e clique em **Selecionar** **(4)**.

   ![](../Media/miyagi-image(68).png)

1. Clique em **Próximo**.

1. Na aba **Examinar + atribuir**, clique em **Examinar + atribuir**.

1. No **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, no menu esquerdo, selecione **Hubs de Eventos** **(1)** em **Entidades** e clique em **miyagi-event-<inject key="DeploymentID" enableCopy="false"/> (2)**

   ![](../Media/miyagi-image86.png)

1. Na **Instância do Hubs de Eventos** de **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, no menu esquerdo selecione **Políticas de acesso partilhado** **(1)** em **Configurações**, clique em **apimLoggerAccessPolicy** **(2)** e copie a chave da**Cadeia de conexão primária** **(3)** cole-o num bloco de notas.

>>> Continuar aqui.
   ![](../Media/miyagi-image87.png)

1. Abra o **notepad** do jumpvm e copie e cole o código abaixo, atualize **&lt;&lt;API_MANAGEMENT_NAME&gt;&gt;** com o nome **miyagi-apim-<inject key="DeploymentID" enableCopy= "false "/>**  e o &lt;&lt;EVENT_HUB_CONNECTION_STRING&gt;&gt; copiado da etapa acima.

   ```
   resource existingApiManagement 'Microsoft.ApiManagement/service@2023-03-01-preview' existing = {
      name: '<<API_MANAGEMENT_NAME>>'
    }
    
    resource ehLoggerWithConnectionString 'Microsoft.ApiManagement/service/loggers@2023-05-01-preview' = {
      name: 'AOAILogger'
      parent: existingApiManagement
      properties: {
        loggerType: 'azureEventHub'
        description: 'Event hub logger with connection string'
        credentials: {
          connectionString: '<<EVENT_HUB_CONNECTION_STRING>>'
          name: 'ApimEventHub'
        }
      }
    }
   ```

   ![](../Media/miyagi-image121.png)

1. Na barra de menu do bloco de notas selecione **Arquivos** e clique em **Salvar como**.

1. Em **Salvar como**, navegue até ao caminho `C:\LabFiles\miyagi` **(1)**, introduza o nome do arquivo **aoai-logger.bicep** **(2)** , mude o tipo para **Todos os arquivos** **(3)** e clique em **Salvar** **(4)**.

   ![](../Media/bicepfile2.png)

1. No jumpvm, abra o terminal PowerShell e execute o seguinte comando para iniciar sessão no **portal Azure**.

    ```
    az login
    ```

1. Isso o redirecionará para a **página de login da Microsoft**. Selecione a sua conta do Azure **<inject key="AzureAdUserEmail"></inject>** e retorne para o **PowerShell**.

   ![](../Media/azure-account-select.png)

1. Execute o seguinte comando para mudar o diretório para a pasta raiz do `miyagi` no terminal e execute o arquivo bíceps.

    > **Observação**: Substitua &lt;&lt;RESOURCE_GROUP_NAME&gt;&gt; com **<inject key="rgname" enableCopy="true"/>**.

    ```
    cd C:\LabFiles\miyagi
    az deployment group create --resource-group <<RESOURCE_GROUP_NAME>> --template-file .\aoai-logger.bicep
    ```

    >**Observação**: Esta sequência de comando navega para o diretório C:\LabFiles\miyagi que contém o arquivo Bicep e, em seguida, implementa os recursos definidos nesse arquivo no grupo de recursos do Azure especificado.

1. Navegue até o portal do Azure, abra o Grupo de Recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** e selecione o serviço de Gerenciamento de API **miyagi-apim-<inject key=" DeploymentID" enableCopy ="false"/>**.

   ![](../Media/lab3-t1-s1.png)

1. No serviço de Gerenciamento de API **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, no menu esquerdo, clique em **APIs** **(1)** e selecione em **Azure OpenAI Service API** **(2)**, selecione **All Operations** **(3)** e em **outbound proccessing** clique em **Policies(4)** para edição.

   ![](../Media/api-outbound.png)

1. No editor de código,  copie a política abaixo para sobrescrever apenas as tags **outbound** e clique em **Salvar**.

      ```
      <outbound>
         <base />
         <choose>
            <when condition="@(!context.Variables.GetValueOrDefault<bool>("isStream"))">
                  <log-to-eventhub logger-id="AOAILogger" partition-id="0">@{
                  var responseBody = context.Response.Body?.As<JObject>(true);
                  return new JObject(
                     new JProperty("prompt_tokens", responseBody["usage"]["prompt_tokens"].ToString()),
                     new JProperty("total_tokens", responseBody["usage"]["total_tokens"].ToString())
                  ).ToString();
            }</log-to-eventhub>
            </when>
         </choose>
      </outbound>
      ```

   ![](../Media/miyagi-image88.png)

1. Em seguida, abra a **IU Miyagi** em uma aba separada, clique em **Personalize** e selecione o seu **Favorite Financial Advisor (1)** e escolha **GPT-4 (2)** para o **Mecanismo de raciocínio** no menu suspenso e clique em **Personalize (3)**. Repita o mesmo passo, selecionando diferentes **Consultores financeiros favoritos** 6 a 7 vezes para gerar registos logs adicionais.

   ![](../Media/miyagi-image126.png)

1. Volte para o Hub de Eventos e selecione o **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](../Media/api-product9.png)

1. No Namespace do Hub de Eventos **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, no menu esquerdo, selecione **Hubs de Eventos** **(1)** em **Entidade** e clique em **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](../Media/miyagi-image89.png)

1.  Na Instância do Hub de Eventos, **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, no menu esquerdo, selecione **Processar dados** **(1)**, role para baixo até encontrar **Processe seus dados do Hub de Eventos usando a linguagem de Consulta do Stream Analytics** e clique em **Iniciar** **(2)**.

   ![](../Media/miyagi-image90.png)

1. Clique em **Consulta teste** e, na consulta do Hub de Eventos, você deverá ver as informações de log dos tokens utilizados.

   ![](../Media/miyagi-image91.png)

### Resumo

Neste laboratório, você configurou um serviço de Gerenciamento de API para gerenciar APIs de forma eficiente. Inicialmente, o serviço foi implantado e uma API foi criada dentro dele. Subsequentemente, regras e funções foram estabelecidas para controlar o acesso à API. O logging do Hub de Eventos foi configurado para monitorar o uso da API de forma eficaz. Por último, a validação de entrada foi realizada para garantir que a API lidasse corretamente com várias entradas. No geral, este processo garantiu o gerenciamento eficaz, a segurança e o monitoramento do desempenho das APIs, contribuindo para um ecossistema de API bem organizado e seguro.

### Você concluiu este laboratório com sucesso. Agora, clique em Avançar no canto inferior direito para ir para a próxima página.
