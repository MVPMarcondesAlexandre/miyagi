# Laboratório 3.1: Containerização da interface Miyagi e do serviço de recomendações no Azure Kubernetes Service (AKS)

### Duração Estimada: 60 minutos

Neste laboratório, você irá conteinerizar e implantar a UI e os serviços de recomendação do Miyagi no Azure Kubernetes Service (AKS). Você começará configurando o Kubernetes e construindo imagens Docker para ambos os serviços. O processo envolve o envio (push) dessas imagens para o Azure Container Registry (ACR) e, em seguida, a implantação delas em um cluster AKS. Isso garante que os serviços sejam integrados e operacionais de forma fluida em um ambiente conteinerizado e escalável, aplicando configurações do Kubernetes, atualizando os endereços IP dos serviços e verificando a implantação acessando os serviços através de seus respectivos endpoints.

## Objetivos do Laboratório
Você será capaz de completar as seguintes tarefas:

- Tarefa 1: Implantar os Serviços no AKS.
- Tarefa 2: Criar uma Imagem Docker para a UI do Miyagi.
- Tarefa 3: Criar Imagens Docker para o serviço de Recomendação.
- Tarefa 4: Enviar a Imagem Docker do serviço de Recomendação para o Registro de Contêiner.
- Tarefa 5: Implantar os Pods no AKS.

### Tarefa 1: Implantar os Serviços no AKS

Nesta tarefa, você implantará os serviços de recomendação e da UI do Miyagi em um cluster do Azure Kubernetes Service (AKS). Isso envolve fazer login no portal do Azure, aplicar as configurações do Kubernetes e atualizar os arquivos de configuração com os endereços IP externos dos serviços.

1. Navegue de volta para a janela de código do Visual Studio e vá para **miyagi/deploy (1)/infrastructure (2)/kubernetes/manifests (3)/50-miyagi (4)**, clique com o botão direito em **50-miyagi** e, no menu, selecione **Abrir no Terminal Integrado (5)**.

   ![](../Media/aks-01.png)

1. Execute o seguinte comando para fazer login no portal do Azure.

    > **Observação**: substitua [ClusterName] por **<inject key="aksname" enableCopy="true"/>** e [ResourceGroupName] por **<inject key="rgname" enableCopy="true"/>**

    ```
    az aks get-credentials -n [ClusterName] -g [ResourceGroupName]
    ```

    > **Observação** : O comando `az aks get-credentials -n [ClusterName] -g [ResourceGroupName]` é usado na interface de linha de comando (CLI) do Azure para recuperar e mesclar os arquivos de configuração do Kubernetes de um cluster AKS especificado no arquivo kubeconfig local.

1. Após o comando ser concluído, você deverá ter acesso ao cluster e poderá executar os seguintes comandos para implantar os serviços da aplicação.

    ```
    kubectl apply -f ./miyagi-recommendation-service.yaml
    ```
    ```
    kubectl apply -f ./miyagi-ui-service.yaml
    ```

    >**Observação**: Após a execução bem-sucedida dos comandos acima, o Kubernetes lerá o arquivo YAML e aplicará suas configurações ao cluster. Ele criará os serviços `miyagi-recommendation-service` e `miyagi-ui`.

1. Assim que os serviços forem implantados, execute o comando abaixo e acompanhe os **IPs externos do serviço**. Pode levar alguns minutos para que os **IPs externos** apareçam, então aguarde um pouco antes de executar o comando.

    ```
    kubectl get svc
    ```

    ![](../Media/external-ip.png)

1. De seguida, navegue até a pasta **miyagi** e expanda **services (1)/recommendation-service (2)/dotnet (3)** e abra o arquivo **appsettings.json (4)**.

   ![](../Media/aks-02.png)

1. Copie o endereço IP externo **miyagi-ui** do console, cole-o na seção **CorsAllowedOrigins** formatado como um endpoint **http://** e salve o arquivo com **Ctrl+S**.

   ![](../Media/ui-cors.png)

1. Depois, navegue até **miyagi/ui/typescript (1)** e abra o arquivo **. env (2)**.

   ![](../Media/aks-03.png)

1. Copie o endereço IP externo **miyagi-recommendation-service** do console, cole-o no valor de  **NEXT_PUBLIC_RECCOMMENDATION_SERVICE_URL** e salve o arquivo com **Ctrl + S**.

   ![](../Media/miyagi-ui-env.png)

### Tarefa 2: Criar uma Imagem Docker para a UI do Miyagi
Nesta tarefa, você construirá e executará o contêiner Docker da UI do Miyagi localmente. Comece abrindo o Docker Desktop e completando a configuração inicial. Em seguida, use o Visual Studio Code para construir a imagem Docker para a UI do Miyagi. Assim que a imagem for criada, verifique-a e execute-a no Docker. Configure a porta do host e acesse a aplicação localmente através da URL fornecida.

1. Navegue até a aplicação Docker Desktop na barra de tarefas. Se não estiver aberta, você pode abri-la clicando duas vezes no aplicativo **Docker** na área de trabalho da VM do Laboratório.

   ![](../Media/docker1.png)

1. Se a janela **Docker Subscription Service Agreement**, clique em **Accept**.

   ![](../Media/docker2.png)

1. Na janela **Welcome to Docker Desktop**, clique em **Continue without signing in**.

   ![](../Media/without-signin.png)

1. Na janela **Sign in**, clique em **Skip**.

    ![](./Media/sign-01.png)

1. Navegue de volta para a janela **Visual Studio Code** e em **miyagi/ui/typescript**, clique com o botão direito e, no menu, selecione **Abrir no Terminal Integrado**.

    ```
    docker build . -t miyagi-ui
    ```

    > **Observação**: Por favor, aguarde, pois este comando pode levar algum tempo para ser concluído.

    > **Observação**: Este comando lê as instruções do Dockerfile, processa-as para criar uma imagem Docker e, em seguida, atribui a tag `miyagi-ui` à imagem resultante.

1. Execute o seguinte comando para ver a imagem recém-criada.

    ```
    docker images
    ```

    ![](../Media/miyagi-image32.png)

1. Navegue de volta para **Docker desktop** e, no painel esquerdo, selecione **Images**.

   ![](../Media/miyagi-image33.png)

1. No painel **Images**, observe que a imagem **miyagi-ui (1)** foi criada, selecione o ícone **Run (2)** .

   ![](../Media/miyagi-image34.png)

1. Na janela **Run a new container**, selecione na seta suspensa.

   ![](../Media/miyagi-image43.png)

1. Em **Run a new container**, em **Ports** para **Host Port** insira **3000 (1)** e clique em **Run (2)**.

   ![](../Media/miyagi-image35.png)

1. Clique no link da URL: **3000:3000**.

   ![](../Media/miyagi-image36.png)

1. Você deverá ver a aplicação rodando localmente.

   ![](../Media/miyagi-image37.png)

### Tarefa 3: Criar Imagens Docker para o serviço de Recomendação

1. Navegue de volta para o **Visual Studio Code**, vá para a pasta **miyagi** e expanda **services (1)/recommendation-service (2)/dotnet (3)**, clique com o botão direito em `dotnet` e selecione **Abrir no terminal Integrado (4)**.

   ![](../Media/aks-04.png)

1. Execute o seguinte comando para construir uma **imagem Docker**.

    ```
    docker build . -t miyagi-recommendation
    ```

    > **Observação**: Por favor, aguarde, pois este comando pode levar algum tempo para ser concluído.

1. Execute o seguinte comando para ver a **imagem Docker** recém-criada.

    ```
    docker images
    ```

    ![](../Media/miyagi-image40.png)

1. Navegue de volta para o **Docker desktop** e, no painel esquerdo, selecione **Images**.

   ![](../Media/miyagi-image33.png)

1. No painel **Images**, observe que a imagem **miyagi-recommendation (1)** foi criada, clique no ícone **Run (2)**.

   ![](../Media/miyagi-image41.png)

1. Na janela **Run a new container**, clique na seta suspensa.

   ![](../Media/miyagi-image42.png)

1. Em **Run a new container**, em **Ports**, para **Host Port**, insira **5224 (1)** e clique em **Run (2)**.

   ![](../Media/miyagi-image44.png)

1. Clique no link da URL **5224:8080**.

   ![](../Media/miyagi-image45.png)

1. Você deverá ver a aplicação rodando localmente.

   ![](../Media/miyagi-image46.png)

### Tarefa 4: enviar o serviço Docker Image of Recommendation para o Container Registry

Nesta tarefa, irá enviar imagens de recomendação miyagi para acr.

1. Navegue de volta para a janela **Visual Studio Code** e navegue até **miyagi/services/recommendation-service/dotnet** - clique com o botão direito do rato em dotnet no menu em cascata, seleccione **Abrir no terminal integrado**.

   ![](../Media/aks-04.png)

1. Execute o seguinte comando para iniciar sessão no **portal Azure**.

    ```
    az login
    ```

1. Isto irá redirecionar para **página de login da Microsoft**, selecione a sua conta do Azure **<inject key="AzureAdUserEmail"></inject>** e navegue de volta para **código do Visual Studio**.

   ![](../Media/azure-account-select.png)

1. Execute o comando seguinte para iniciar sessão num **Azure Container Registry (ACR)** utilizando a CLI do Azure.

    > **Nota**: Substitua **[ACRname]** **<inject key="AcrUsername" enableCopy="true"/>**.

    ```
    az acr login -n [ACRname]
    ```

    >**Nota**: O comando az acr login -n [ACRname] regista-o numa instância do Azure Contentor Registry (ACR). Autentica a sua sessão com o Registo de Contentores do Azure especificado, permitindo enviar e extrair imagens de contentores de e para o registo.

1. Execute o seguinte comando para adicionar a etiqueta.

    > **Nota**: Substitua **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**.

    ```
    docker tag miyagi-recommendation:latest [ACRname]/miyagi-recommendation:latest
    ```

    >**Nota**: o comando docker tag miyagi-recommendation:latest [ACRname]/miyagi-recommendation:latest marca uma imagem local do Docker com um novo nome que inclui o nome do Azure Container Registry (ACR). Ao marcar a imagem desta forma, prepara-a para ser enviada por push para o Registo de Contentores do Azure especificado.

1. Execute o seguinte comando para enviar a imagem para o registo do contentor.

    > **Nota**: Substitua **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**.

    ```
    docker push [ACRname]/miyagi-recommendation:latest
    ```

    ![](../Media/task2-6.png)

    >**Nota**: O comando docker push [ACRname]/miyagi-recommendation:latest carrega a imagem do Docker especificada, que foi marcada com o nome do Azure Container Registry (ACR), para o ACR. Isto disponibiliza a imagem no ACR para implementação e utilização em vários serviços Azure.

1. Navegue de volta para a janela **Visual Studio Code** e navegue até **miyagi/ui/typescript** - clique com o botão direito do rato no menu em cascata e selecione **Abrir no terminal integrado**.

1. Execute o seguinte comando para adicionar a etiqueta.

    > **Nota**: Substitua **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**.

    ```
    docker tag miyagi-ui:latest [ACRname]/miyagi-ui:latest
    ```

1. Execute o seguinte comando para enviar a imagem para o registo do contentor.

    > **Nota**: Substitua **[ACRname]** por **<inject key="AcrLoginServer" enableCopy="true"/>**.

    ```
    docker push [ACRname]/miyagi-ui:latest
    ```

### Tarefa 5: Implantar pods AKS

1. Navegue de volta para a janela de código do Visual Studio e navegue até **miyagi/deploy/infrastructure/kubernetes/manifests/50-miyagi** clique em **50-miyagi** no menu em cascata e seleccione **Abrir no Terminal integrado**.

   ![](../Media/aks-01.png)

1. Abra o ficheiro **miyagi-recommendation.yaml** e substitua o ficheiro &lt;ACR-NAME&gt; com **<inject key="acrUsername" enableCopy="true"/>** Nome do registo do contentor Azure e guarde o ficheiro por **Ctrl + S**.

   ![](../Media/miyagi-image47.png)

   ![](../Media/miyagi-image48.png)

1. Abra o ficheiro **miyagi-ui.yaml** e substitua o ficheiro &lt;ACR-NAME&gt; com **<inject key="acrUsername" enableCopy="true"/>** Nome do registo do contentor Azure e guarde o ficheiro por **Ctrl + S**.

   ![](../Media/miyagi-image49.png)

   ![](../Media/miyagi-image50.png)

1. Execute os seguintes comandos para implementar os pods de aplicações.

    ```
    kubectl apply -f ./miyagi-recommendation.yaml
    ```
    ```
    kubectl apply -f ./miyagi-ui.yaml
    ```

1. As aplicações devem agora ser implantadas. Para verificar, execute o comando abaixo e verá os dois pods em estado de execução.

    >**Nota**: Pode demorar alguns minutos até que a saída apareça, por isso aguarde alguns minutos antes de executar o comando.

    ```
    kubectl get pods
    ```

    ![](../Media/AKS-running.png)


    >**Parabéns** pela conclusão da tarefa! Agora é altura de validá-lo. Aqui estão os passos:
    > - Clique no botão Validar para a tarefa correspondente. Se receber uma mensagem de sucesso, validou o laboratório com sucesso.
    > - Caso contrário, leia atentamente a mensagem de erro e tente novamente o passo, seguindo as instruções do guia do laboratório.
    > - Se precisar de ajuda, contacte-nos através do e-mail labs-support@spektrasystems.com.

 <validation step="f50c7e4e-0b5a-4ae2-bd9e-ff29a023f1d2" />

# Laboratório 3.2: Explorar e verificar a UI Miyagi em contentor e o serviço de recomendação no AKS

Neste laboratório, irá explorar a implementação e verificação da UI Miyagi e dos serviços de recomendação no Azure Kubernetes Service (AKS). As tarefas envolvem testar APIs e aceder à UI através de pontos finais do Ingress, garantindo a funcionalidade adequada no ambiente AKS.

### Tarefa 1: Explorar o serviço de recomendação no AKS utilizando o Ingress Endpoint

1. Para testar a API, execute o comando abaixo para obter os endereços IP do serviço

    >**Nota**: Pode demorar alguns minutos até que a saída apareça, por isso aguarde alguns minutos antes de executar o comando.

    ```
    kubectl get svc
    ```

    ![](../Media/miyagi-image129.png)

1. Copie o endereço IP externo do **miyagi-recommendation-service** e introduza-o no browser. Agora deve ver o ponto final do swagger.

   ![](../Media/miyagi-image52.png)

### Tarefa 2: Explore a aplicação Miyagi no AKS utilizando o Ingress Endpoint

1. Para testar a UI, execute o comando abaixo para obter os endereços IP do serviço
 
    ```
    kubectl get svc
    ```

    ![](../Media/miyagi-image128.png)

1. Copie o endereço IP externo do **miyagi-ui** e introduza-o no browser. Agora deve ver a interface do Miyagi.

   ![](../Media/miyagi-image53.png)

### Resumo

Neste laboratório, implementou o Azure Kubernetes Service (AKS) para a UI Miyagi e para o serviço de recomendação Miyagi. Tudo começou com a construção de imagens Docker para estes serviços, contendo todos os componentes necessários, como código e ficheiros de configuração. Após a criação da imagem, o passo seguinte envolveu o envio da imagem Docker do serviço de recomendação para um registo de contentor, uma plataforma de armazenamento e implementação para clusters Kubernetes. Por fim, foram implementados pods AKS, representando contentores em execução no cluster Kubernetes, tornando operacional a UI Miyagi e o serviço de recomendação

### Concluiu este laboratório com sucesso. Agora clique em Seguinte no canto inferior direito para passar para a página seguinte.
