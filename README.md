# Deployment do Quake III em OpenShift

## 1. Deployment:
* O Deployment "quake" especifica que uma réplica do servidor Quake será implantada.
* Define dois containers: um para o servidor Quake e outro para o servidor de conteúdo, onde ambos utilizam a mesma imagem.
* O readiness probe é configurado para verificar a disponibildiade do servidor Quake a cada 5 segundos após um atraso inicial de 15 segundos.
* E por fim, os volumes "quake3-server-config" e "quake3-content" são montados para acessar suas respectivas configurações e dados de conteúdo.

## 2. Serviço:
* Ele expõe o servidor Quake por meio de um NodePort para permitir acesso externo.
* O Serviço "quake" encaminha o tráfego para três portas diferentes nos pods: 8080 para o cliente, 27960 para o servidor e 9090 para o servidor de conteúdo.

## 3. ConfigMap: 
* O ConfigMap "quake3-server-config" contém a configuração do servidor Quake, como as configurações do jogo, nome do servidor, senha e mapas.

## 4. Rota:
* A rota "quake" é direcionada para o Serviço com o nome "quake", segmentando a porta "client", tornando possível acessar a aplicação por meio de um URL.
