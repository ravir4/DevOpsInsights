---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrando o Deployment Risk Analytics à entrega contínua

É possível instrumentar pipelines para o {{site.data.keyword.contdelivery_full}} para usar recursos de análise do Deployment Risk do {{site.data.keyword.DRA_short}}. Em seguida, é possível publicar dados dessas tarefas e incluir portas que impingem políticas de riscos.

Para ver uma explicação de alto nível de análise do Deployment Risk do {{site.data.keyword.DRA_short}}, veja [Sobre o Deployment Risk](./about_risk.html).

Para obter mais informações sobre pipelines de entrega contínua, veja [a documentação oficial](../ContinuousDelivery/pipeline_working.html).

## Preparando estágios e tarefas de pipeline
{: #integrate_pipeline}

Para começar, é necessário instrumentar seu pipeline para se comunicar com o {{site.data.keyword.DRA_short}}. Você faz isso definindo variáveis de ambiente específicas para todas as suas tarefas de pipeline que constroem, testam ou implementam código. Também deve-se incluir variáveis de ambiente em tarefas de teste que impingem políticas de riscos usando o tipo de testador da Porta do DevOps Insights.

* Registros de construção
* Registros de implementação
* Resultados de teste

Os resultados de teste devem fornecer dados em um destes formatos suportados:

| Tipo de teste                | Formatos suportados                                               |
|------------------------------|-----------------------------------------------------------------|
| Teste de verificação funcional | Mocha, xUnit                                                    |
| Teste de unidade             | Mocha, xUnit, Karma/Mocha                                       |
| Cobertura de código          | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Varredura de app estático    | Varreduras de app estático fornecidas pelo IBM Application Security on Cloud  |
| Varredura de app dinâmico    | Varreduras de app dinâmico fornecidas pelo IBM Application Security on Cloud |
| SonarQube                    | Dados de varredura fornecidos pelas varreduras do SonarQube                      |

As variáveis de ambiente que você define no pipeline fornecem contexto para publicar esses registros. É possível defini-las usando o comando `export` nos scripts de suas tarefas. Também é possível configurá-las no menu Propriedades do ambiente de estágios de cada pipeline.

Variáveis de ambiente:

| Variável de ambiente  | Propósito | Necessária em |
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | O nome do app no painel. | Todas as tarefas que constroem, testam, implementam e impingem políticas de riscos do {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | O texto que é incluído como um prefixo nas construções do estágio. Esse texto também aparece no painel. | Todas as tarefas que constroem, testam, implementam e impingem políticas de riscos do {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | O ambiente no qual o aplicativo é executado. | Tarefas de teste e implementação. |

### Configurando tarefas de construção

Para a última tarefa de construção em um estágio, configure variáveis de ambiente para um nome do aplicativo e prefixo de construção. Um script de exemplo incluiria estes comandos:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Quando essa tarefa de construção for concluída, o pipeline publicará uma mensagem no {{site.data.keyword.DRA_short}} que uma construção SampleApp está concluída.

### Configurando tarefas de implementação

Para a última tarefa de implementação no estágio, configure um nome do aplicativo, prefixo de construção e nome do ambiente. Um script de exemplo incluiria estes comandos:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Quando essa tarefa de implementação for encerrada, o pipeline publicará uma mensagem no {{site.data.keyword.DRA_short}} que a construção e o app especificados foram implementados em um ambiente.

### Configurando tarefas de teste

Para todas as tarefas que produzem resultados de teste, configure um nome do aplicativo e prefixo de construção.

Se a tarefa gera resultados de teste de verificação funcional (FVT), deve-se também configurar o nome do ambiente lógico onde quer que esses testes sejam executados.

Um script de exemplo incluiria estes comandos:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

Certifique-se de que os nomes de aplicativos e ambientes correspondam onde apropriado. Por exemplo, você deseja que uma tarefa de teste de produção que é executada com relação a uma implementação de produção tenha valores `LOGICAL_ENV_NAME` idênticos.

## Publicando dados de teste no DevOps Insights
{: #configure_pipeline_jobs}

O {{site.data.keyword.DRA_short}} usa os resultados de teste de suas tarefas para gerar relatórios e impingir políticas de riscos. É possível publicar dados de teste de todos os tipos de tarefas.

Há duas opções para publicar os resultados de teste:

* Chamar uma interface da linha de comandos (CLI) simples no script de uma tarefa.

* Inclua uma tarefa de teste com o tipo de Testador avançado em seu pipeline.

Ao usar o método Testador avançado, você não publica os resultados de teste usando a CLI. Em vez disso, você especifica o local dos arquivos de resultado na tarefa de pipeline e a tarefa faz upload dos resultados à medida que eles se tornam disponíveis.

Qualquer que seja o método de publicação usado, os resultados de teste devem estar em um dos formatos suportados pelo {{site.data.keyword.DRA_short}}:

<table><thead>
<tr>
<th>Tipo de teste</th>
<th>Formatos suportados</th>
</tr>
</thead><tbody>
<tr>
<td>Teste de verificação funcional</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Teste de unidade</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Cobertura de código</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

### Publicando dados de teste de qualquer tipo de tarefa

Em um pipeline, é possível usar qualquer tipo de tarefa para executar um teste. Depois de executar esse teste, é possível fazer upload de seus resultados para o {{site.data.keyword.DRA_short}}. Você faz upload dos resultados chamando uma CLI no shell script da tarefa. 

É possível fazer upload desses tipos de resultados de teste por meio da CLI:

* Testes de unidade
* Cobertura de código
* Testes de verificação funcional
* Resultados da varredura de app estático e dinâmico do IBM Application Security on Cloud. 

Este é um script de exemplo que executa testes e, em seguida, faz upload dos resultados para o {{site.data.keyword.DRA_short}}: 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

Para saber mais sobre o comando `idra`, veja [a página do pacote grunt-idra3 no npm](https://www.npmjs.com/package/grunt-idra3). 

### Publicando dados de teste de tarefas do Testador avançado

É possível incluir tarefas de teste com o tipo de Testador avançado em um pipeline. Depois que são executadas, elas fazem upload automaticamente de seus resultados no {{site.data.keyword.DRA_short}}. 

1. No estágio no qual você deseja incluir a tarefa que faz upload dos resultados, clique no ícone **Configuração de estágio** ![Ícone de configuração de estágio de pipeline](images/pipeline-stage-configuration-icon.png). Clique em **Configurar
estágio**.
2. Crie uma tarefa de teste e digite um nome para ela. 
3. Para o tipo de tarefa, selecione **Testador avançado**.
4. Preencha os campos **Comando de teste** e **Diretório ativo** como você faria para uma tarefa de teste de pipeline normal. 
5. Preencha os campos restantes para fazer upload dos resultados de teste para um tipo de teste específico. 

 1. Escolha o tipo de métrica que corresponde ao que você definiu na política do {{site.data.keyword.DRA_short}} que deseja usar.
 2. Digite um local do arquivo de resultado. Esse local é relativo ao diretório ativo. 

6. Se desejar fazer upload dos resultados para um segundo tipo de teste na mesma tarefa, preencha os campos prefixados com *Adicional*.
7. Clique em **Salvar** para retornar para o pipeline.

A Figura 1 mostra uma tarefa de teste que está configurada para executar testes de unidade, fazer upload dos resultados no formato Mocha e fazer upload dos resultados da cobertura de código no formato Istanbul.

![Tarefa de upload do DevOps Insights](images/insights_upload_job.png)
*Figura 1. Resultados de upload para o DevOps Insights*



## Definindo portas
{: #configure_pipeline_gates}

As portas do {{site.data.keyword.DRA_short}} verificam se os resultados do teste obedecem à política definida. Se a política não for atendida, a porta do {{site.data.keyword.DRA_short}} falhará, por padrão. Também é possível configurar portas para agir em uma função consultiva para permitir a progressão de pipeline mesmo após falha.

O painel Deployment Risk depende da presença de uma porta após uma tarefa de implementação temporária. Se desejar usar o painel, certifique-se de que tenha uma porta depois de implementar no ambiente temporário, mas antes de implementar em um ambiente de produção.

Geralmente, as portas são colocadas antes da promoção de construção em seu pipeline. Esses locais são ideais para verificar a qualidade da construção com relação a suas políticas, para assegurar que é seguro promover de um ambiente para outro. No entanto, é possível
colocar portas em qualquer lugar no pipeline nas quais você deseja que um critério específico seja verificado. As portas que forem colocadas antes da implementação em um ambiente temporário continuarão a utilizar políticas, mas não aparecerão no painel Deployment Risk.

1. Em um estágio, clique no ícone **Configuração de estágio** ![Ícone de configuração de estágio de pipeline](images/pipeline-stage-configuration-icon.png) e clique em **Configurar estágio**.
2. Clique em **Incluir Tarefa**. Para o tipo de tarefa, selecione **Teste**.
3. Para tipo de testador, selecione **Porta do {{site.data.keyword.DRA_short}}**.
4. Especifique o nome do ambiente. Certifique-se de que esse valor corresponda ao que foi definido em suas
[propriedades do ambiente](#toolchain_pipeline_props).
5. Insira o nome da política a ser verificado nessa porta.

 Esse nome deve corresponder exatamente a um dos nomes de política que você definiu. É possível especificar apenas políticas que são definidas na mesma
organização do {{site.data.keyword.Bluemix_notm}} que a sua cadeia de ferramentas.

6. Opcional: para fazer uma função de porta no modo consultivo, limpe a caixa de seleção **Parar a execução deste estágio se essa tarefa
falhar**. Em modo consultivo, o {{site.data.keyword.DRA_short}} conclui a mesma análise de política na porta e gera relatórios, mas, se uma falha
ocorrer, o pipeline não será parado.
7. Clique em **Salvar** para retornar para o pipeline.
8. Configure portas para todas as suas políticas do {{site.data.keyword.DRA_short}} repetindo estas etapas.

![Tarefa Mocha do Deployment Risk](images/insights_gate_job.png)
*Figura 2. Porta do DevOps Insights*

Após o seu pipeline estar configurado, comece a usar o {{site.data.keyword.DRA_short}}. 
