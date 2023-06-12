<h1 style='text-align: center;'>Configurar e subir o ambiente localmente</h1>

## Introdução

Este guia tem como objetivo auxiliar novos desenvolvedores a subirem pela primeira vez a aplicação completa localmente, bem como auxiliar os demais desenvolvedores a subirem e derrubarem a aplicação de forma mais simples.

> É preferível um ambiente Linux para acessar o ambiente, Windows pode dar problemas em algumas máquinas.

## Baixando os fontes do projeto

Em uma pasta de sua escolha (preferencialmente alguma que não exija privilégios de administrador), crie uma pasta para acomodar os fontes do projeto e entre nela:

### Linux

```bash
mkdir siged && cd siged
```

### Windows

```bash
mkdir siged | cd siged
```

Execute o seguinte comando para baixar todos os arquivos do projeto provenientes do _GitHub_:

### Linux

```bash
git clone https://github.com/DITGO/2021-2-SiGeD-Frontend && git clone https://github.com/DITGO/2021-2-SiGeD-Clients && git clone https://github.com/DITGO/2021-2-SiGeD-Users && git clone https://github.com/DITGO/2021-2-SiGeD-Demands && git clone https://github.com/DITGO/2021-2-SiGeD-Sectors && git clone https://github.com/DITGO/2021-2-SiGeD-Cargos && git clone https://github.com/DITGO/2021-2-SiGeD-Patrimonio
```

### Windows

```bash
git clone https://github.com/DITGO/2021-2-SiGeD-Frontend | git clone https://github.com/DITGO/2021-2-SiGeD-Clients | git clone https://github.com/DITGO/2021-2-SiGeD-Users | git clone https://github.com/DITGO/2021-2-SiGeD-Demands | git clone https://github.com/DITGO/2021-2-SiGeD-Sectors | git clone https://github.com/DITGO/2021-2-SiGeD-Cargos | git clone https://github.com/DITGO/2021-2-SiGeD-Patrimonio
```

## Dependências

Como o ambiente será executado dentro de um container [`docker`](https://www.docker.com/), é necessário que ele esteja instalado e rodando em sua máquina.

## Subindo a aplicação

Dentro da pasta `siged` onde estão as pastas da aplicação, crie um script para facilitar a inicialização:

### Linux

crie um arquivo chamado `initialize_containers.sh` (Linux) ou `initialize_containers.bat` (Windows) e cole o seguinte código nele:

```sh
docker network create siged_backend
for dir in 2021-2-SiGeD-Cargos 2021-2-SiGeD-Demands 2021-2-SiGeD-Sectors 2021-2-SiGeD-Clients 2021-2-SiGeD-Frontend 2021-2-SiGeD-Users 2021-2-SiGeD-Patrimonio
do
  docker-compose --f ./${dir}/docker-compose.yml up --detach
done
```

### Windows

```batch
@echo off

docker network create siged_backend

for %%i in (
    "2021-2-SiGeD-Cargos"
    "2021-2-SiGeD-Demands"
    "2021-2-SiGeD-Sectors"
    "2021-2-SiGeD-Clients"
    "2021-2-SiGeD-Frontend"
    "2021-2-SiGeD-Users"
    "2021-2-SiGeD-Patrimonio"
) do (
    cd %%i
    docker-compose --file docker-compose.yml up --detach
    cd ..
)
```


Execute os scripts diretamente no console, certificando-se de estar na pasta "siged", que contém todos os repositórios clonados:

### Linux

```bash
bash initialize_containers.sh
```

### Windows

```batch
initialize_containers.bat
```

## Derrubando a aplicação

Assim como para subir a aplicação, crie um script chamado `stop_containers.sh` (Linux) ou `stop_containers.bat` (Windows) e cole o seguinte código nele:

### Linux

```sh
for dir in 2021-2-SiGeD-Cargos 2021-2-SiGeD-Demands 2021-2-SiGeD-Sectors 2021-2-SiGeD-Clients 2021-2-SiGeD-Frontend 2021-2-SiGeD-Users 2021-2-SiGeD-Patrimonio
do
  docker-compose --f ./${dir}/docker-compose.yml down
done
docker network rm siged_backend
```

### Windows

```batch
@echo off

for %%i in (
    "2021-2-SiGeD-Cargos"
    "2021-2-SiGeD-Demands"
    "2021-2-SiGeD-Sectors"
    "2021-2-SiGeD-Clients"
    "2021-2-SiGeD-Frontend"
    "2021-2-SiGeD-Users"
    "2021-2-SiGeD-Patrimonio"
) do (
    docker-compose --file ./"%%~i"/docker-compose.yml down
)

docker network rm siged_backend

```

Novamente, execute os scripts diretamente no console, certificando-se de estar na pasta "siged", que contém todos os repositórios clonados:

### Linux

```bash
bash stop_containers.sh
```

### Windows

```batch
stop_containers.bat
```
