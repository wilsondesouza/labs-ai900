# Introdução às Configurações Iniciais no Azure para Implementação de Aprendizado de Máquina

## Estabelecimento do Ambiente Azure Machine Learning

Ao ingressar na plataforma Azure, o primeiro passo é criar um ambiente propício ao desenvolvimento de modelos de Aprendizado de Máquina (ML). No Menu Lateral, a primeira ação consiste em selecionar "Criar um Recurso" > "IA + Machine Learning" > "Azure Machine Learning".

Ao optar por criar, será apresentado um menu abrangente de configuração.

As informações essenciais a serem preenchidas compreendem:

Assinatura (associada à conta)
Grupo de Recursos (cada recurso deve pertencer a um grupo)
Nome
Região
A inclusão de detalhes como conta de armazenamento, cofre de chaves e Application Insights pode ser automática ou requer intervenção. No caso de ausência de dados preenchidos, a opção "criar" deve ser selecionada imediatamente abaixo.
Uma vez preenchidas as informações básicas, é possível avançar clicando em "examinar + criar", desde que todas as entradas estejam corretas e validadas pela Azure, conforme ilustrado na imagem abaixo. Em seguida, clique em "criar".

Após a confirmação da criação, o recurso iniciará seu processo, podendo levar alguns minutos. Uma vez iniciado, a tela subsequente será exibida. Aguarde até o início do processo.

Ao término da criação, a tela de confirmação será exibida, permitindo o acesso ao recurso.

Ao entrar, é recomendável acessar o Azure Studio para configurar a aplicação, clicando em "Iniciar o Studio".


## Azure Studio

Ao iniciar o Azure Studio, uma variedade de opções de Aprendizado de Máquina estará disponível. Para o propósito inicial de aprendizado, a opção "ML Automatizado" deve ser selecionada no menu lateral.

Essa escolha implica que, após as configurações iniciais, o Azure irá treinar modelos conforme as configurações estabelecidas. Dentro da aba ML Automatizado, selecione a opção "Novo trabalho de ML Automatizado".

No decorrer das configurações, é necessário estabelecer parâmetros conforme as diretrizes da [documentação oficial da Microsoft](https://microsoftlearning.github.io/AI-900-AIFundamentals.pt-BR/Instructions/02-module-02.html), a saber:

Seleção do tipo de tarefa: regressão
Criação de um novo conjunto de dados com as seguintes configurações:
Nome: bike-rentals
Descrição: dados históricos de aluguel de bicicletas
Tipo: tabular
Especificação da fonte de dados como "De arquivos da Web"
URL da Web: [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals)
Formato de arquivo: delimitado
Delimitador: vírgula
Codificação: UTF-8
Cabeçalhos de coluna: apenas o primeiro arquivo contém cabeçalhos
Esquema: inclusão de todas as colunas, excluindo o caminho
Definição de parâmetros adicionais, como métrica primária, modelos permitidos, limites, validação e teste, e especificações de computação.
Após o seguimento passo-a-passo da documentação referente ao tipo de tarefa e dados, a tela de confirmação será apresentada, permitindo a criação (o que levará alguns segundos).

Uma vez concluído, a visualização dos dados do conjunto criado ("bike-rentals") estará disponível. Em seguida, as configurações de tarefa devem ser ajustadas conforme especificado.

Após todas as configurações, uma aba de verificação final será exibida. Verifique se as configurações estão conforme desejado e clique em "Envie o trabalho de treinamento".

O processo de envio inicialmente indicará que o trabalho foi enviado, mas ainda não foi inicializado. Após alguns minutos, o trabalho será iniciado automaticamente, mudando para o status "Em execução". O tempo de execução médio é de aproximadamente 15 minutos a partir da alteração do status.

Ao finalizar o treinamento, o status será atualizado para "concluído" e as informações estarão disponíveis no modelo. Na aba "Melhor resumo de modelo", é possível acessar informações sobre o melhor modelo configurado e suas métricas.


## Implantação do Modelo

Na página do modelo, clique em "Modelo de registro". Será aberta uma aba para preenchimento do nome e descrição, seguido pelo registro do modelo.

Na aba lateral, dentro da guia "Ativos", selecione "Modelos" e clique no modelo registrado.

Clique no nome abaixo do item "Criado por trabalho". Isso permitirá o acesso às informações do modelo, como métricas e logs de treinamento.

O nome exibido na parte superior será diferente, pois corresponde ao melhor modelo dentro dos parâmetros definidos para a Azure, com nomes gerados automaticamente para diferenciação.

## Teste do Modelo
Para testar a saída do modelo e verificar sua conformidade com os dados compartilhados, é necessário realizar testes. No menu lateral do Azure, selecione "Pontos de extremidade" dentro da aba "Ativos". Se necessário, crie um ponto de extremidade e avance para implantar o modelo. O processo de implantação pode levar alguns minutos. Após a conclusão, acesse a aba de teste e insira o comando abaixo:
```
 {
   "input_data": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```

Nesta interface, é possível visualizar um arquivo JSON de entrada para teste. Os parâmetros utilizados para teste são fornecidos. Cada modelo de aprendizado de máquina apresentará um valor específico.