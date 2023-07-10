# Checkout plataforma de cursos (Em desenvolvimento)

O intuito deste projeto é simular um ambiente de checkout, onde o cliente faz um cadastro e faz um "pagamento".<br>
Quando este pagamento for processado, o cliente receberá os dados de acesso ao portal em seu e-mail. <br>
Este repositório não contém o projeto, mas sim informações e link dos repositórios com os microserviços que o compõem.<br>
Aqui também contém um docker-compose com a configuração de todos os containers necessários para a execução do projeto.

## Fluxo do Projeto
![Fluxo-Portal-Cursos](https://github.com/filipedev040990/checkout-plataforma-cursos/assets/106783314/c2aa4b82-81b2-4364-bd83-35c8b3b9030a)



## 📉 Microserviço de Marketing

Este microserviço cadastra dados do lead e após o pagamento o converte para cliente. A confirmação do pagamento é monitorada consumindo uma fila do RabbitMq. Ele também monitora leads que iniciaram o cadastro mas não concluíram
o pagamento e envia notificações.<br>
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/marketing-microsservice)

## 💸 Microserviço Financeiro

Este microserviço cadastra dados do cliente e da cobrança. Em seguida publica este pagamento em uma fila para que seja processado posteriormente. Após confirmação do pagamento que é monitorada consumindo uma fila do RabbitMq, ele atualiza os dados financeiros e novamente publica os dados em outra fila que será consumida por outros microserviços.<br> Em caso de falha na cobrança, será publicado uma mensagem em uma fila para o microserviço de notificação enviar um e-mail para o pagador.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/financial-microsservice)

## 💳 Microserviço de Pagamento

Este microserviço consome uma fila de pagamentos que estão aguardando processamento. Na sequência, publica o resultado em uma fila de pagamentos processados que será lida por outros microserviços.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/payment-microsservice)

## 💳 Microserviço Card Encryptor

Este microserviço recebe dados de cartão de crédito e o salva criptografado no banco de dados para posteriormente fornecê-lo ao microserviço de pagamento. Após o microserviço de pagamento utilizá-lo para a cobrança, estes dados são eliminados.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/card-encryptor-microsservice)

## 📓 Microserviço Acadêmico

Este microserviço consome uma fila de pagamentos processados e caso tenha sido aprovado, irá criar um registro acadêmico do aluno e seus dados de acesso à plataforma. Na sequência, publica estes dados em uma fila de notificação que será lida por outro microserviço.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/academic-microsservice)


## 📧 Microserviço de Notificação

Este microserviço consome uma fila de notificações e dispara e-mails.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/notification-microsservice)

## 🐰 RabbitMq

Nossos microserviços se comunicarão através de mensageria. Para isso usaremos o rabbitmq. Ele já está configurado para criar as Exchanges e filas e fazer os binds ao subir o container.
Você pode clonar este projeto através deste [link](https://github.com/filipedev040990/rabbitmq)
