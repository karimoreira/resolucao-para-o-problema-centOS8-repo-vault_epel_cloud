# Solução para Problemas de Download dos Metadados do Repositório Baseos no CentOS 8

Decidi colocar em produção a solução prática para resolver o problema de download dos metadados do repositório Baseos no CentOS 8, que foi descontinuado. A solução envolve a configuração do repositório alternativo "vault.epel.cloud".

Com a descontinuação do CentOS 8, muitos usuários enfrentaram dificuldades ao tentar atualizar ou instalar pacotes usando os repositórios padrão, incluindo eu e no momento não quero mudar de distro. Esse problema é causado pelo fim do suporte aos repositórios oficiais, o que impede o download dos metadados necessários para gerenciar pacotes, porém temos opções alternativas e que bom que somos uma comunidade.



## Como resolver o problema de download dos metadados para o repositório Baseos no CentOS 8 Linux, que foi descontinuado?

## Configurando o repositório “vault.epel.cloud” no CentOS 8. Para isso temos que:

Instalar o pacote epel-release, que adiciona o repositório EPEL (extra packages for enterprise linux) à lista de repositórios, permitindo a instalação de pacotes adicionais não disponíveis nos repositórios padrão:

-  sudo yum install epel-release

Comentar as linhas contendo mirrorlist nos arquivos de configuração dos repositórios do CentOS:
- sudo sed -i ‘s/mirrorlist/#mirrorlist/g’ /etc/yum.repos.d/CentOS-*

Descomentar as linhas que definem baseurl e definir o URL do repositório para vault.centos.org:
- sudo sed -i ‘s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

Substituir o URL baseurl antigo pelo novo URL vault.centos.org:
- sudo sed -i ‘s|baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

Comentar as linhas contendo mirrorlist nos arquivos de configuração dos repositórios CentOS-Linux e descomentar as linhas que definem baseurl e definir o URL do repositório para vault.epel.cloud:
- sudo sed -i ‘s/mirrorlist/#mirrorlist/g’ /etc/yum.repos.d/*.repo
- sudo sed -i ‘s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/*.repo

Substituir o URL baseurl antigo pelo novo URL vault.epel.cloud:
- sudo sed -i ‘s|baseurl=http://mirror.centos.org|baseurl=http://vault.epel.cloud|g' /etc/yum.repos.d/*.repo

Atualizar todos os pacotes instalados no sistema:
- sudo yum update -y

Listar os arquivos de configuração dos repositórios no diretório /etc/yum.repos.d/:
- ls /etc/yum.repos.d/

Substituir todas as ocorrências de mirror.centos.org por vault.epel.cloud em todos os arquivos .repo:
- sudo sed -i ‘s|mirror.centos.org|vault.epel.cloud|g’ /etc/yum.repos.d/*.repo

Atualizar todos os pacotes e permitir a remoção de pacotes conflitantes, se necessário:
- sudo yum update -y — allowerasing*-