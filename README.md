Catálogo e Publicação de metadados de coleções
==============================================

Este documento demonstra como preparar as coleções de metadados em documentos JSON.


Como criar e enviar os metadados de uma nova coleção
----------------------------------------------------

Para criarmos uma nova coleção o primeiro passo é enviar um Pull Request para esse repositório.

Não sabe fazer isso? Fique tranquilo que aqui vai um passo a passo:

> **Tip:** Se preferir você pode ver [documentação oficial do GitHub sobre fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)


Acessando o GitHub
++++++++++++++++++

primeiro de tudo, tenha uma conta no GitHub. Você pode criar uma clicando no botão signup no canto superior direito da página ou logo aqui:
https://github.com/signup

Faça login na sua conta.

Criando um Fork
+++++++++++++++

Um fork é uma cópia de um repositório que fica na sua conta, separada do original.
Então você pode alterar os arquivos sem medo sem afetar os arquivos originais.

Para fazer um fork clique em `Fork` e na nova janela que abrir clique em `Create fork`.

Agora ao acessar os seus repositórios (clicar na sua foto de perfil no canto superior direito e em `Repositories`), você terá acesso ao seu Fork

Criando um Clone
++++++++++++++++

Enquanto o `fork` é uma cópia online de um repositório, o `clone` é uma cópia local, ou seja, baixada para o seu computador.

Vamos criar um `clone` do nosso `fork` no seu computador.
Para isso acesse o seu repositório `metadata` (o fork que vc criou no passo anterior), clique no botão verde `Code` e no simbolo de copiar. Isso irá copiar a url mostrada na tela.

agora em um terminal em sua máquina local, navegue até o diretório onde você quer salvar a cópia do seu repositório e execute o comando:

```git clone [cole aqui a url copiada]```

no meu caso ficou assim:

```git clone https://github.com/marujore/metadata.git```

Abaixo um exemplo usando o comando `mkdir` para criar um diretório, usando o comando `cd` para acessar o diretório e realizando o git clone.

Criando arquivo de metadado
+++++++++++++++++++++++++++

Agora você tem o diretório em sua máquina local!

Você pode criar um novo arquivo de metadados.

Recomendo que você copie o arquivo `sentinel/s2-l2a.json` e edite-o.

Renomeie seu arquivo, mantendo-o minisculo, e lembre-se sempre de descrever seu conjunto de dados, ele será lido por pessoas que talvez não sejam especialistas nele!

Cada campo do arquivo .json é descrito mais abaixo neste README. Veja a descrição de cada campo, faça sua edição no seu editor de texto preferido e uma vez encerrado faça um commit (descrito na próxima sessão).

Em caso de dúvidas entre em contato com os mantenedores do repositório, você pode fazer isso via email ou criar uma issue no repositório fazendo sua pergunta.

Fazendo um commit
+++++++++++++++++

Uma vez preparado o documento JSON, você pode fazer o *commit* (salvar a versão do seu projeto) no seu *fork* e em seguite abrir um *pull-request** (PR), ou seja fazer uma solicitação para que seus novos arquivos, ou suas edições sejam aceitas no repositorio oficial dos metadados.

Para fazer um commit, abra um terminal, navegue até o diretório do seu *fork* do repositório e digite o comando

```git status```

Em vermelho você verá os arquivos que foram alterados.

Para cada arquivo que você queira inserir no seu commit, faça o comando

```git add nome_do_arquivo```

Ao fazer um o comando `git status` novamente, você notará que agora esses arquivos aparecerão em verde.

Para inserir o (os) arquivo (os) no commit use o comando

```git commit -m "descrição das alterações"```

por exemplo

```git commit -m "Adição da nova coleção de dados do Satélite XYZ em reflectância de superfície"```

Agora você pode enviar suas alterações para o seu repositório, para isso use o comando

```git push origin main```

> **Tip:** Em alguns repositórios mais antigos o termo `master` era usado ao invés de `main`.

Se você acessar a página do seu repositório (seu fork do repositório), notará que ele esta 1 commit a frente.

Vamos submeter então as alterações para o repositório original

Abrindo um Pull-Request
+++++++++++++++++++++++

Ao acessar a página do seu repositório (seu fork), clique na aba `Pull requests`

Agora clique no botão verde `New pull request`

Metadados
---------

O repositório ``metadata`` consiste em uma base de dados revisados pelos responsáveis de modo a publicar os dados no catálogo oficial da BIG/BDC. Basicamente, esses metadados são documentos em JSON que seguem algumas diretrizes de campos de modo a serem integrados com o modelo de dados do [bdc-catalog](https://github.com/brazil-data-cube/bdc-catalog).

Para incluir uma nova coleção neste repositório, recomenda-se criar um [fork](https://github.com/brazil-data-cube/metadata/fork) para sua conta no GitHub. Em seguida, clone o repositorio::

    git clone https://github.com/<UserName>/metadata




A estrutura deste documento deve seguir os seguintes campos:

- ``id``: Identificador Unico da coleção (Deve-se manter como ``null``). Este valor deve ser alterado posteriormente uma vez que tenha um identificador referente no banco de dados do catálogo.
- ``name``: (*OBRIGATORIO*) Nome curto para representar a coleção. Uma boa prática é manter os nomes com os caracteres em minúsculo. ``landsat``, ``mod13q1``, etc. Caso opte por usar algum separador de preferência ao uso de hífen (``-``). Esse campo não permite o uso de espaços.
- ``version``: (*OBRIGATORIO*) Versão desta coleção e será considerado como chave unica com o campo ``collection-version``.. Aceita-se numeros, letras etc. ``landsat-2`` (Coleção Landsat Versão 2), ``mod13q1-6.1`` (Coleção MOD13Q1 Versão 6.1), etc.
- ``title``: (*OBRIGATORIO*) Título representativo da coleção. Utilize um titulo descritivo e curto pois será destacado no catálogo STAC. ``Landsat Collection 2 - Level-2`` etc. Caso opte por usar algum separador de preferência ao uso de hífen (``-``).
- ``description``: (*OBRIGATORIO*) Descrição do dado.
- ``grid_ref_sys``: (*OPCIONAL*) Grade de referência da coleção, caso não exista manter como ``null``.
- ``collection_type``: (*OBRIGATORIO*) Enumeração do tipo do documento. Os valores disponíveis são: ``collection`` - coleções de dados; ``cube`` - cudos de dados; ``mosaic`` - mosaico de imagens; ``classification`` - mapa temático do produto classificado.
- ``metadata``: (*OBRIGATORIO*) Metadados gerais a serem agregados na coleção. Nos objetos STAC Collection, incorpora novos campos dentro de ``properties``.

    - ``providers``: (*OBRIGATORIO*) Lista de entidades provedores dos dados. Cada entidade provedor segue a especificação [STAC Provider Object](https://github.com/radiantearth/stac-spec/blob/v1.0.0/collection-spec/collection-spec.md#provider-object) e deve possuir os seguintes campos:

        - ``name``: Nome real da entidade provedora dos dados.
        - ``roles``: Enumeração que represente o papel do provedor de dados. Os valores disponíveis são: `licensor`, `producer`, `processor` e `host`.
        - ``url``: Pagina inicial que o provedor utiliza para descrever o seu papel e a definição dos dados para contato.
        - ``description`` (*OPCIONAL*): Detalhes adicionais para descrever a entidade provedora.

- ``keywords``: Palavras chaves associadas para descrever a coleção. Uma boa prática é manter os nomes com os caracteres em minúsculo. Algumas palavras chaves a serem adotadas podem referir-se à àrea do dado (`brazil`, `biome`, `amazon`, `cerrado`, `paraiba state`), nome do programa espacial (`cbers`, `landsat`), nome do satélite que carrega o instrumento (`cbers-4`, `landsat-8`,` `cbers-4a`,` `sentinel-2`), sensor (`oli`, `msi`, `wfi`), tipo do dado (`mosaic`), formato do dado (`cog`, `cloud optimized geotiff`) dentre outros (`visible imagery`, `earth observation`, `visible wavelengths`, `ultraviolet wavelengths`, `yanomami`, `indigenous`).
- ``is_public``: Campo booleano que define se a coleção está disponível publicamente no STAC. Por padrão ``true``. Quando configurado como ``false``, só poderá acessa-la através de role definida no INPE IAM.
- ``is_available``: Campo booleano que define se a coleção se encontra disponível. Este campo é usado quando uma coleção deixa de existir (devido a existência de uma nova) ou mesmo quando planeja-se alguma parada momentânea. Quando configurado como ``false``, nem mesmo usuários com permissão de acesso (com exceção de administradores) podem acessa-lá caso tenham o privilégio configurado no INPE IAM. Por padrão, é configurado como ``false``.
- ``category``: (*OBRIGATORIO*) Campo interno do ``bdc-catalog`` para identificação da categoria de dados que se enquadra a coleção: ``eo``, ``sar``, ``lidar``, ``unknown``.
- ``quicklook``: Propriedade que representa as bandas utilizadas na geração do *asset* ``thumbnail``.
- ``version_predecessor``: (*OPCIONAL*) Identificador *INTEIRO* da coleção que representa a versão anterior.
- ``version_successor``: (*OPCIONAL*) Identificador *INTEIRO* da coleção que representa a versão seguinte.
- ``bands``: (*OBRIGATORIO*) Lista de bandas da coleção. Cada *banda* deve seguir a seguinte assinatura:

    - ``name``: (*OBRIGATORIO*) Nome real da banda disponível no sensor. Não pode conter espaços.
    - ``common_name``: (*OBRIGATORIO*) Alias da banda (nome usual).
    - ``description``: (*OPCIONAL*) Descrição curta para banda.
    - ``min_value``: (*OBRIGATORIO*) Valor minimo considerado como válido.
    - ``max_value``: (*OBRIGATORIO*) Valor máximo considerado como válido.
    - ``nodata``: (*OPCIONAL*) Valor de nodata. Obs: NaN é uma representação de valor, nodata deve ser um valor específico como 0, -9999 ou outro valor determinado.
    - ``scale``: (*OBRIGATORIO*) Escala multiplicadora do dado. Ex: muitos dados de reflectância de superfície são armazenados como inteiros variando entre 0 e 10000. Assim o scale desses dados é 0.0001 para transforma-los em escala 0 a 1.
    - ``scale_add``: (*OPCIONAL*) Fator aditivo a ser considerado na banda. Em produtos Landsat-2 Collection 2 por exemplo, existe um fator aditivo de -0.2 a ser considerado após o scale multiplicativo. Por padrão, valor ``null``.
    - ``data_type``: (*OBRIGATORIO*) Representação do tipo de dado em computação para armazenamento dos dados. Os valores disponíveis seguem o *bdc-catalog*: ``uint8``, ``int8``, ``uint16``, ``int16``, ``uint32``, ``int32``, ``float32``, ``float64``.
    - ``mime_type``: (*OBRIGATORIO*) Media type vinculado a banda gerada em disco. Os valores suportados atualmente são: ``image/png``, ``image/tiff``, ``image/tiff; application=geotiff``, ``image/tiff; application=geotiff; profile=cloud-optimized``, ``text/plain``, ``text/html``, ``application/json``, ``application/xml``, ``application/x-tar``, ``application/zip``, ``application/gzip``, ``image/jp2; profile=cloud-optimized``, ``image/jp2``, ``application/x-netcdf``, ``application/netcdf``.
    - ``resolution_x``: (*OPCIONAL*) Resolução espacial dos pixels em `x`.
    - ``resolution_y``: (*OPCIONAL*) Resolução espacial dos pixels em `y`.
    - ``resolution_unit``: (*OPCIONAL*) Unidade da Resolução espacial. Ex: ``Meter``, ``Kilometer``. Atente-se a letras maiúsculas e minúsculas.
    - ``center_wavelength``: (*OPCIONAL*) Comprimento central da onda, em micrometros (*μm*), quando houver.
    - ``full_width_half_max``: (*OPCIONAL*) Largura à meia altura, parâmetro que descreve a largura de uma banda espectral em termos de resolução espectral.

- ``summaries``: (*OPCIONAL*) Sumário dos valores dos campos que podem ser vinculados a nivel item na coleção:

    - ``instruments``: (*OBRIGATORIO*) Lista de sensores presentes na coleção. Por exemplo no sentinel-2 ``["msi"]``.
    - ``platform``: (*OBRIGATORIO*) Lista de plataformas vinculadas na coleção. Por exemplo no sentinel-2 ``["sentinel-2a", "sentinel-2b"]``.
    - ``constellation``: (*OPCIONAL*) Constelações vinculadas a coleção. Por exemplo no sentinel-2 ``["sentinel-2"]``.
    - ``gsd``: (*OPCIONAL*) Ground Sampling Distance, parâmetro que define a resolução espacial de uma imagem capturada por um sensor.
    - ``view:off_nadir`` (*OPCIONAL*) Visada do sensor a Nadir.

- ``item_assets``: (*OBRIGATORIO*) Mapa de assets presentes na coleção, de modo a oferecer uma visão alto nivel para que o usuário possa determinar quais assets esta interessado. O mapa deve representar ``Map[str, Asset]`` onde a chave é uma *string* representando o nome do *asset* (sem espaços) e o ``Asset`` a seguinte assinatura:

    - ``title``: (*OBRIGATORIO*) Titulo descritivo do *asset*.
    - ``type``: (*OBRIGATORIO*) Media type do *asset*.
    - ``roles``: (*OBRIGATORIO*) Caracteristica do *asset*: ``thumbnail``, ``overview``, ``data``, ``metadata``.
    - ``description`` (*OPCIONAL*) Descrição detalhada do *asset* e/ou como foi processado.

- ``properties``: (*OPCIONAL*) Campos opcionais sem validação que podem ser incorporados no corpo do STAC.


Os campos a seguir referem-se ao *collection_type* ``cube`` ou ``mosaic``:

- ``temporal_composition_schema``: (*OPCIONAL*) composição temporal da coleção. Esse campo pode ser opcional se for uma coleção ``Identidade`` por exemplo.
- ``composition_function``: (*OPCIONAL*) função de composição do cubo de dados. Os valores disponíveis atualmente são: ``Identity``, ``Least CC First``, ``Median``.

> :warning: **Warning:**
Revise os documentos antes de fazer o *commit* e abrir o *pull-request*. Garanta que o documento é um JSON válido, caso contrário não será aceito.
