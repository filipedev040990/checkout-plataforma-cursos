# Checkout plataforma de cursos

O intuito deste projeto é simular um ambiente de checkout, onde o cliente faz um cadastro e faz um "pagamento".<br>
Quando este pagamento for processado, o cliente receberá os dados de acesso ao portal email seu e-mail. <br>
Este repositório não contém o projeto, mas sim informações e link dos repositórios com os microserviços que o compoõem.<br>
Aqui também contém um docker-compose com a configuração de todos os containers necessários para a execução do projeto.

## 📉 Microserviço de Marketing

Este microserviço cadastra dados do lead e após o pagamento o converte para cliente. A confirmação do pagamento é monitorada consumindo uma fila do RabbitMq. Ele também monitora leads que iniciaram o cadastro mas não concluíram
o pagamento e envia notificações.<br>
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/marketing-microsservice)

## 💸 Microserviço Financeiro

Este microserviço cadastra dados do cliente e da cobrança. Em seguida publica este pagamento em uma fila para que seja processado posteriormente. Após confirmação do pagamento que é monitorada consumindo uma fila do RabbitMq, ele atualiza os dados financeiros e novamente publica os dados em outra fila que será consumida por outros microserviços.<br>
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/financial-microsservice)

## 💳 Microserviço de Pagamento

Este microserviço consome uma fila de pagamentos que estão aguardando processamento. Na sequência, publica o resultado em uma fila de pagamentos processados que será lida por outros microserviços.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/payment-microsservice)

## 📓 Microserviço Acadêmico

Este microserviço consome uma fila de pagamentos processados e caso tenha sido aprovado, irá criar um registro acadêmico do aluno e seus dados de acesso à plataforma. Na sequência, publica estes dados em uma fila de notificação que será lida por outro microserviço.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/academic-microsservice)


## 📧 Microserviço de Notificação

Este microserviço consome uma fila de notificações e dispara e-mails.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/notification-microsservice)
