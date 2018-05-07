---

copyright:
  years: 2016, 2018
lastupdated: "2018-3-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Criando políticas e regras
{: #policies_and_rules}

As políticas são conjuntos de regras que controlam as portas em seu pipeline de entrega. Se o seu código não atender nem exceder uma política executada em uma porta específica, a implementação será interrompida para evitar que as mudanças de risco sejam liberadas.

As políticas são definidas no {{site.data.keyword.DRA_short}}. As políticas são criadas na organização (org.) do {{site.data.keyword.Bluemix_notm}} que contém o {{site.data.keyword.DRA_short}}. Qualquer aplicativo que estiver na mesma organização poderá usar a política. 

## Criando políticas
{: #create_policies}

Para criar uma política:

1. No menu de navegação {{site.data.keyword.DRA_short}}, clique em **Configurações**.

2. Clique em **Políticas**.

3. Clique em **Criar política** e, em seguida, digite um nome e uma descrição para a nova política.

4. Clique em **Avançar**.

4. Inclua pelo menos uma regra na política:
  1. Clique em **Incluir regra na política**.
  2. Selecione o tipo de regra.
  3. Insira detalhes e condições para a regra.
  4. Clique em **Salvar**.

5. Ao concluir a inclusão de regras na política, clique em **Concluído**.

## Criando regras
{: #creating_rules}

As regras definem os critérios que suas políticas usam para julgar o sucesso ou a falha. Você pode criar uma política de "Teste de unidade e cobertura de teste" que contenha uma regra de teste de unidade que requeira 80 por cento de sucesso de teste de unidade e uma regra de cobertura de teste que requeira 100 por cento de cobertura de código. Se você incluir uma porta que se refira a essa regra em um pipeline, a porta evitará que quaisquer construções que não satisfaçam a ambas as regras continuem. 

É possível requerer o sucesso sem importar o quê marcando os testes como críticos. Para criar uma regra, selecione uma política e, em seguida, clique em **Incluir regra na política**. 

### Criando regras de teste de verificação funcional
{: #criteria_fvt}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico. Para determinar nomes de casos de teste, veja [Formatos e ferramentas de resultado de teste](#criteria_formats).

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


### Criando regras de teste de unidade
{: #criteria_ut}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico. Para determinar nomes de casos de teste, veja [Formatos e ferramentas de resultado de teste](#criteria_formats).

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


### Criando regras de cobertura de código
{: #criteria_codecoverage}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de cobertura de código que é necessária para ser declarada bem-sucedida.

3. Para monitorar para regressões de cobertura de código, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

4. Clique em **Salvar**.

### Criando regras de varredura de segurança estática
{: #criteria_static}

É possível integrar o {{site.data.keyword.DRA_short}} ao IBM Application Security on Cloud para executar varreduras de código estático e de app dinâmico. Para obter mais informações sobre o Application Security on Cloud, veja [a documentação oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

### Criando regras de varredura de segurança dinâmica
{: #criteria_dynamic}

É possível integrar o {{site.data.keyword.DRA_short}} ao {{site.data.keyword.appseccloudfull}} para executar varreduras de apps dinâmicos. Para obter mais informações sobre o Application Security on Cloud, veja [a documentação oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

## Formatos e ferramentas de resultado de teste
{: #criteria_formats}

Para resultados de teste, o {{site.data.keyword.DRA_short}} suporta estes tipos de métricas e formatos:

* Teste de verificação funcional (Mocha, xUnit)
* Teste de unidade (Mocha, xUnit, Karma/Mocha)
* Cobertura de código (Cobertura, lcov, Istanbul como formato do relatório de resumo json, Blanket.js)

O {{site.data.keyword.DRA_short}} também suporta testes do Selenium e Jasmine. Esses testes devem ser incluídos dentro das ferramentas oficialmente suportadas, como xUnit e Mocha. Para saber mais sobre como usar o {{site.data.keyword.deliverypipeline}}, o {{site.data.keyword.DRA_short}} e o Selenium juntos, veja [Executando testes do Selenium por meio da linha de comandos em um pipeline de entrega](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Para itens que têm casos de teste, é possível especificar casos de teste críticos, que são testes que devem passar independentemente da porcentagem
aceitável. Os nomes de casos de teste críticos devem corresponder ao atributo `full title` do caso de teste.    
* Para testes Karma/Mocha, as sequências de descrição `describe()` e `it()` são vinculadas aos espaços.
* Para testes xUnit, o nome do pacote, o nome de classe e o nome da função são vinculados aos espaços. Isso é ilustrado no seguinte exemplo:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Esse exemplo produz estes nomes de casos de teste:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

É possível usar o Sauce Labs com o {{site.data.keyword.DRA_short}} incluindo a integração de ferramenta do Sauce Labs em seu pipeline. Em seguida, incorpore as
variáveis de ambiente `SAUCE_USERNAME` e `SAUCE_ACCESS_KEY` em testes do Selenium como credenciais.

É possível ver os títulos completos de todos os testes nos logs após uma execução.  

**Observações:**
* O {{site.data.keyword.DRA_short}} não suporta testes críticos que contenham um hífen no título integral.    
* Se você mudar o seu nome da organização, deverá recriar as políticas que estavam associadas com o nome anterior. Você perderá o acesso a quaisquer relatórios de decisão que foram gerados antes da mudança de nome.
