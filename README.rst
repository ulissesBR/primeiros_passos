#######################################
 Curso Plone IFPR
#######################################

Este é o buildout utilizado durante o Hangout on Air `"Primeiros 
Passos com Plone, o CMS Pythonico" <http://bit.ly/155rNjr>`_ realizado em 12 
de Julho de 2013.

*********************
Instalando
*********************


Pré-Requisitos
================

Para ambientes de desenvolvimento sugerimos:

    * Sistema Operacional: Debian 7.0 / Ubuntu 12.10
    * Memória Mínima: 1GB


Preparação do ambiente
==========================

Acesso internet
----------------------

Tanto para o ambiente de desenvolvimento como o de produção é necessário
que o computador onde será realizada a instalação deve ter acesso à Internet.

Teste o acesso internet utilizando a ferramenta **wget** no terminal do Linux:
::

	wget -S --delete-after http://www.plone.org/


.. note :: O *-S* indica que o wget deverá retornar os cabeçalhos de
           conexão. 


Configurando proxy
~~~~~~~~~~~~~~~~~~~~

Caso, para acesso à internet, seja necessário configurar servidores de Proxy,
no terminal digite:
::

	export http_proxy=http://<endereco>:<porta>
	export https_proxy=http://<endereco>:<porta>
	export ftp_proxy=http://<endereco>:<porta>

.. note :: Para servidores que necessitam de autenticação,
           substitua *<endereco>:<porta>* por 
           *<nome_usuario>:<senha>@<endereco>:<porta>*.


Pacotes do sistema
----------------------

Primeiramente atualizar os pacotes existentes::

    aptitude update && aptitude upgrade


Depois instalar os pacotes base::

    sudo aptitude install build-essential libssl-dev libxml2-dev libxslt1-dev libbz2-dev zlib1g-dev python-setuptools python-dev python-virtualenv libjpeg62-dev libreadline-gplv2-dev python-imaging wv poppler-utils git -y

Clonando o buildout
---------------------

Inicialmente é feito o clone deste buildout:
::

    cd ~
    git clone git@github.com:simplesconsultoria/primeiros_passos.git


.. note :: Caso o comando acima apresente problemas -- provavelmente devido ao
           bloqueio da porta de ssh (22) na sua rede interna -- altere 
           **git@github.com:** por **https://github.com/**.



Criando VirtualEnv
---------------------

Para evitar conflitos com o Python utilizado pelo sistema operacional, cria-se
um virtualenv apartado do restante do sistema.
::

    cd primeiros_passos
    virtualenv py27
    source py27/bin/activate


Executando Buildout
---------------------

Usando o Python do Virtual Environment que criamos acima, executamos::

	python bootstrap.py


Isto criará o ambiente necessário para executarmos o buildout, o que é feito 
com o comando abaixo::

	./bin/buildout


Adicionando Complementos
--------------------------

Se quiser adicionar um complemento para o Plone, edite o arquivo buildout.cfg, 
procure na seção [buildout] a opção eggs (linha 22) e liste os novos 
complementos::

	eggs =
    	Pillow
    	Plone
    	Products.PrintingMailHost
    	collective.cover
    	Products.PloneFormGen
    	plone.app.workflowmanager

.. note:: No exemplo acima adicionamos os complementos 
          Products.PrintingMailHost, collective.cover, 
          Products.PloneFormGen e plone.app.workflowmanager.

Após alterar o arquivo buildout.cfg deve-se re-executar o script buildout para 
que os novos produtos sejam baixados e ativados.
