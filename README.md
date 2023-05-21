# myslq-replication
MySQL replication with Docker

Executar
Para executar esses exemplos, você precisará iniciar os contêineres com "docker-compose" e após iniciar a replicação de configuração. Veja os comandos dentro de ./build.sh.

Crie 2 contêineres MySQL com replicação baseada em linha mestre-escravo
./build.sh

Faça alterações no mestre
docker exec mysql_master sh -c "export MYSQL_PWD=111; mysql -u root mydb -e 'create table code(code int); insert into code values (100), (200)'"

Ler alterações do escravo
docker exec mysql_slave sh -c "export MYSQL_PWD=111; mysql -u root mydb -e 'select * from code \G'"

Solução de problemas
Verificar registros
docker-compose logs

Iniciar contêineres no modo "normal"
Acesse "build.sh" e execute o comando passo a passo.

Verifique os contêineres em execução
docker-compose ps

Limpar diretório de dados
rm -rf ./mestre/dados/*
rm -rf ./slave/data/*

Execute o comando dentro de "mysql_master"
docker exec mysql_master sh -c 'mysql -u root -p111 -e "SHOW MASTER STATUS \G"'

Execute o comando dentro de "mysql_slave"
docker exec mysql_slave sh -c 'mysql -u root -p111 -e "SHOW SLAVE STATUS \G"'

Entre em "mysql_master"
docker exec -it mysql_master bash
Entre em "mysql_slave"
docker exec -it mysql_slave bash
