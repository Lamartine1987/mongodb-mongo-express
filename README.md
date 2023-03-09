# mongodb-mongo-express

Esse é um teste baseado em containers Docker com o MongoDB junto ao mongo-express, uma interface de admnistração via web. 

Serão utilizadas as imagens mongo e mongo-express e os parâmentros serão definidos dentro do docker-compose.yaml

O serviço do mongoDB acessará a porta 27017, já o mongo-express acessará a porta 8081.

Dentro do docker-compose as variáveis de ambiente serão definidas para a geração dos dois containers. 

As variáveis MONGO_INITDB_ROOT_USERNAME e MONGO_INITDB_ROOT_PASSWORD do mongoDB foram definidas com o login:mongo3 password:mongo3 para 
acesso à instância mongoDB.

Para o mongo-express foram definadas as seguintes variáveis de ambiente:
ME_CONFIG_BASICAUTH_USERNAME e ME_CONFIG_BASICAUTH_PASSWORD - elas servem para acessar a aplicação web
ME_CONFIG_MONGODB_PORT, ME_CONFIG_MONGODB_ADMINUSERNAME e ME_CONFIG_MONGODB_ADMINPASSWORD - elas servem para que o mongo-express acesse a instância do mongoDB

ME_CONFIG_BASICAUTH_USERNAME: root 
ME_CONFIG_BASICAUTH_PASSWORD: root123
ME_CONFIG_MONGODB_ADMINUSERNAME: mongo3 
ME_CONFIG_MONGODB_ADMINPASSWORD: mongo3
ME_CONFIG_MONGODB_PORT: 27017
ME_CONFIG_MONGODB_SERVER: mongodb

Além disso, foi criado um volume para que armazene o estado do DB, caso o container seja apagado. Dessa forma, quando o próximo container mongoDB for 
criado ele passará a consumir as mesmas informações. 
volumes:
  mongo_volume:
  
 O armazenamento será feito no mongo_volume:/data/db
 
 Foi criada uma network para que os dois containers possa se comunicar.
 networks:
  mongo_net
  
Com essa network, a comunicação entre os containers pode ocorrer, assim definido dentro de cada um deles:
  networks:
    - mongo_net
    
Para fazer a criação dos containers, basta rodar no terminal na pasta em que foi criado o arquivo docker-compose.yaml a seguinte instrução:
  docker-compose up -d
  
Os containers serão criados e para conferir se estão rodando, basta digitar: docker container ls -a
O status dos containers precisam estar UP para você conseguir acessar o mesmo.
Depois basta ir ao seu navegador e digitar: http://localhost:8081

A aplicação web deve aparecer e você poderá colocar as suas credenciais para acessá-la. 
