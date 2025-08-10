# Laboratório 1:  Verificar e Recuperar Valores dos Recursos Azure (opcional)

**Duração Estimada: 20 minutos**

Neste laboratório, você irá verificar e recuperar valores específicos, como Ponto de Extremidade, String de Conexão e Chave, para diversos recursos do Azure. Essa etapa é fundamental para garantir a configuração correta e a conectividade desses recursos.

 - Azure OpenAI: **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**
 - Conta do Azure Cosmos DB: **cosmos-<inject key="DeploymentID" enableCopy="false"/>**
 - Serviço de Pesquisa (Search Service): **acs-<inject key="DeploymentID" enableCopy="false"/>**

1. Para verificar os nomes dos modelos de implantação para "**deploymentOrModelId**" e "**embeddingDeploymentOrModelId**", siga os passos abaixo:

    - Na página inicial do Portal Azure, clique em **Grupos de recursos** no painel **Navegação**.

      ![](../Media/miyagi-image6.png)

    - Na página de grupos de recursos, clique em **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

      ![](../Media/miyagi-image7.png)

    - No **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, na aba **Visão Geral (1)**, selecione o **OpenAIService-<inject key="DeploymentID" enableCopy="false"/> (2)**.

      ![](../Media/miyagi-image118.png)

    - Na página **OpenAI do Azure**, na seção **Visão geral**, clique em **Go to Azure AI Foundry portal**. Isso o levará para o **portal Azure AI Foundry**.

      ![](../Media/miyagi-image10.png)

    - No **portal do Azure AI Foundry**, no painel de navegação esquerdo, na seção **Recursos compartilhados**, selecione **Implantações**.

      ![](../Media/miyagi-image119.png)

    - Na aba **Implantações** do Azure AI Foundry, clique no nome da implantação **gpt-4** **(1)** e verifique o **nome da implantação** do modelo gpt-4 **(2)**.

      ![](../Media/miyagi-image(12).png)

      ![](../Media/miyagi-image(13).png)

    - Navegue de volta para a página de **Implantações (1)**.

    - Na aba **Implantações** do Azure AI Foundry, clique no nome da implantação **text-embedding-ada-002 (1)** e verifique o **nome da implantação** do modelo **text-embedding-ada-002 (2)**.

      ![](../Media/miyagi-image(14).png)

      ![](../Media/miyagi-image(15).png)

1. Para verificar os valores de **Ponto de Extremidade** e **Chave**, siga os passos abaixo:

    - Retorne à aba do **portal Azure**.

    - No recurso **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>** na seção **Gerenciamento de Recursos**, selecione **Chaves e Ponto de Extremidade (1)**, verifique o valor da **CHAVE 1 (2)** e do **Ponto de Extremidade (3)**.

      ![](../Media/miyagi-image16.png)

1. Para verificar os valores de "azureCognitiveSearchEndpoint", "azureCognitiveSearchApiKey", siga os passos abaixo:

    - Retorne ao grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

    - Na página **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, Selecione o recurso **acs-<inject key="DeploymentID" enableCopy="false"/>** na lista de recursos.

      ![](../Media/miyagi-image110.png)

    - No recurso **acs-<inject key="DeploymentID" enableCopy="false"/>**, verifique a **URL**.

      ![](../Media/miyagi-image111.png)

    - No mesmo recurso **acs-<inject key="DeploymentID" enableCopy="false"/>**, na seção **Configurações**, selecione **Chaves (1)** e verifique o valor da **Chave de administração primária (2)**.

      ![](../Media/miyagi-image112.png)

1. Para verificar os valores de "**cosmosDbUri**" e "**cosmosDbName**", siga os passos abaixo:

    - No grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, selecione **cosmos-<inject key="DeploymentID" enableCopy= "false"/>** da lista de recursos.

      ![](../Media/miyagi-image113.png)

    - Em **cosmos-<inject key="DeploymentID" enableCopy="false"/>** verifique a **URL**.

      ![](../Media/miyagi-image114.png)

    - Em **cosmos-<inject key="DeploymentID" enableCopy="false"/>** na seção **Configurações**, selecione **Chaves (1)** e verifique o valor da **String de Conexão Primária do Cosmos DB (2)**.

      ![](../Media/miyagi-image115.png)

1. Para obter os valores de **blobServiceUri**, siga os passos abaixo:

    - Retorne ao grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, selecione **miyagiblobstorge<inject key="DeploymentID" enableCopy=" false"/>** da lista de recursos.

      ![](../Media/miyagi-image116.png)

    - Na conta de armazenamento **miyagiblobstorge<inject key="DeploymentID" enableCopy="false"/>** no menu esquerdo, selecione **Pontos de Extremidades** **(1)** na seção **Configurações**, verifique o **Serviço Blob** **(2)**.

      ![](../Media/miyagi-image117.png)

## Resumo
Neste laboratório, você irá verificar e recuperar valores de configuração como Endpoint, String de Conexão e Chave para vários recursos do Azure, como o Serviço OpenAI, Cosmos DB e Cognitive Search. Isso garante a configuração e a conectividade adequadas. Os passos envolvem acessar o Portal do Azure, navegar para grupos de recursos específicos e verificar os valores necessários.

### Agora, clique em Avançar no canto inferior direito para ir para a próxima página.
