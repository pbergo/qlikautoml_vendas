# Desafio Qlik AutoML

## Resumo

- [License](#license-summary)
- [Termo Responsabilidade](#disclaimer)
- [Introdução](#introdução)
- [Cenário](#cenário)
- [O Desafio](#introduction)
- [O que se espera](#o-que-se-espera)
- [Base de Dados](#base-de-dados)
    - [Docker Desktop](#docker-desktop)
    - [Base de Dadas Vendas](#base-de-dados-vendas---mysql)

## License

Esse projeto foi feito baseado no licenciamento MIT. Veja detalhes em [LICENSE](LICENSE).

## Termo de Responsabilidade

1. Este **não** é um projeto suportado pela Qlik.
2. Contribuições como Issues, Pull Requests e códigos adicionais são bem vindos.
3. **Qlik Inc.** ou **Qlik Support** não tem nenhum relacionamento com esse projeto.
4. Todos os dados aqui apresentados são fictícios e qualquer relação com a realidade é mera coincidência.
4. A versão inicial foi desenvolvida por [Pedro Bergo](https://www.linkedin.com/in/pedrobergo/), atualmente Qlik Data Integration Senior Implementation Consultant na empresa Qlik, Inc, no time Data Professional Services.

## Introdução

Esse documento foi criado como desafio para uso do [Qlik AutoML](https://www.qlik.com/us/products/qlik-automl), possibilitando aos interessados entender e aplicar alguns dos recursos da plataforma Qlik Cloud (https://www.qlik.com).

Todos os dados aqui apresentados são fictícios e qualquer relação com a realidade é mera coincidência.

## Cenário

A COM.ROUPAS é mundialmente conhecida pelo design inovador, qualidade de seus produtos e garantia de entrega. Seus produtos e sua marca alcançam diretamente 9 países e sua presença é conhecida em 83 importantes cidades no Brasil e mundo. 

O seu modelo de negócio é baseado em dois pilares: Preços Fixos e Prazo de Entrega de 7 dias.

Essa estratégia permitiu forte expansão a partir de 2019, usando um inovador modelo de venda, entrega e forte atendimento aos clientes e público consumidor, mantendo-se à frente da concorrência e sendo caso de sucesso internacional.

Mesmo com toda a vantagem adquirida, a COM.ROUPAS enfrenta enormes desafios no seu mercado, como enorme pressão da concorrência, aumento dos custos de fornecedores e grandes dificuldades na logística de entregas. 

Em 2025, suas vendas continuam em crescimento, mas a empresa viu recentemente uma redução nas margens de lucro, causadas pelo aumento de custos diretos e também por dificuldades na operação de distribuição. O cenário conflituoso mundial apresenta um desafio adicional, e a diretoria decidiu investigar a fundo os motivos que causam os frequentes problemas nas entregas.

O primeiro ponto a ser investigado se refere aos motivos que causam cancelamento nos Pedidos de Venda e você e sua equipe serão os responsáveis por entender e apresentar uma solução para reduzir ou eliminar esse problema.


### O Desafio

A empresa deseja identificar em tempo real se cada pedido de venda pode ser cancelado ou não. Ela espera que essa abordagem permite reverter possíveis cancelamentos ou redirecionar os esforços de programação de entregas de pedidos que tenham grande risco cancelados, permitindo manter as margens de lucro.

A equipe da COM.ROUPAS disponibilizou a base de dados de vendas para suas análises e elaboração de um modelo de IA/ML que permita predizer se um determinado pedido de venda será ou não cancelado, além de identificar quais os atributos mais interferem no cancelamento.

### O que se espera

- Saber quais dados impactam no cancelamento de pedidos.
- Prover um método (API ou outro) que possiblite a previsão de cancelamento em tempo real para cada novo pedido.

### Base de dados

O modelo do banco de dados está apresentado a seguir.

![Docker Terminal](https://github.com/pbergo/qlikautoml_vendas/blob/fe5464e70272bb6dad13aded6d5bea9fe3e05f87/images/derbase.png)

##### Docker Desktop

Recomenda-se utilizar plataforma Docker Desktop para rodar a base MySQL.
O Docker Desktop pode ser encontrado em https://www.docker.com/products/docker-desktop/

Para rodar o Docker Desktop é necessário ter Sistema operacional Windows 10/11, 4Gb de memória e WSL-Windows Subsystem for Linux 2.

Nesse link você encontra instruções de [instalação do Docker Desktop em Windows](https://docs.docker.com/desktop/setup/install/windows-install/), além de detalhamento dos requisitos necessários para instalação.

Depois de instalado, você ainda precisará se cadastrar no cloud da Docker a fim de usar o ambiente.

##### Base de dados Vendas - MySQL

O banco de dados está disponível no repositório docker e pode ser acessado através dos comandos a seguir para colocar o banco no ar e popular a base de dados.

1. Abra o Docker Desktop
- Faça login no Docker Desktop
- Acesse o Terminal do Docker

![Docker Terminal](https://github.com/pbergo/qlikautoml_vendas/blob/fe5464e70272bb6dad13aded6d5bea9fe3e05f87/images/dockerterminal.png)


2. Baixar e executar a base MySQL

``` bash
# Open bash (bash or powerbash)
docker run --name vendasodsdb -e MYSQL_ROOT_PASSWORD="mysql1234!" -e MYSQL_DATABASE=vendasods -e MYSQL_ROOT_HOST=% -e PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin -v /var/lib/mysql -p 3306:3306 -p 33060:33060 -d pedrobergo/vendasodsdb:latest
```

3. Popular a base de dados VENDASODS
``` bash
# Senha é mysql1234!
docker container exec -it -e MYSQL_ROOT_PASSWORD="mysql1234!" vendasodsdb sh -c "mysql -u root -p vendasods < /tmp/vendasods.sql"
```

A base VENDASODS no MySQL está disponível através das seguintes credenciais:
- Conexão: localhost
- Porta: 3306
- Usuário: root
- Senha: mysql1234!
- Database: vendasods
- SSL: Preferred ou Enabled

