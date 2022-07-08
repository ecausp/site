# site

Arquivos de configuração para desenvolvimento do site institucional com Docker + Lando 

O objetivo é ter um ambiente de desenvolvimento (Drupal8) para desenvolvimento do site institucional utilizando Docker + Lando. Com isso não será mais necessário ter Apache, MySql e PHP instalados no desktop de desenvolvimento.

## Uso

### 1) Certifique-se de ter instalados o lando e o docker:

Para isso acesse a documentação: 

Docker: https://docs.docker.com/engine/install/ubuntu/ 

Lando: https://docs.lando.dev/basics/installation.html#linux

### 2) Reinicie seu PC

### 3) Baixe o site institucional para a pasta do seu projeto

### 4) Baixe o arquivo (.lando.yml) deste repositório para a raiz do seu projeto

Note que o .gitignore vai substituir o do projeto. Isso é para que os arquivos do Lando não sejam versionados em seu projeto. Você pode optar em incluir no .gitignore do seu projeto ou se preferir pode deixar que os arquivos sejam versionados.

Note que no arquivo .lando.yml você pode optar por exemplo pela versão do PHP, versão do Composer ou pelo servidor de Web utilizado, Apache ou Ngix

### 5) Configure os arquivos:

```bash
/seuprojeto/docroot/.htaccess
/seuprojeto/docroot/sites/default/settings.php
/seuprojeto/docroot/sites/default/services.yml
```

### 6) Inicialize o projeto

```bash
lando rebuild -y
```

### 7) Restaure o dump MySql do site 

```bash
lando db-import backup/site.sql
```

### 8) Desinstale os módulos Senha única USP e Google Analytics

```bash
lando drupal mou senhaunicausp google_analytics
```

### 9) Instale os módulos dev

```bash
lando drupal moi devel kint
```

### 10) Adicione o projeto drush

```bash
lando composer require drush/drush:10.x
# Teste o comando (cache rebuild) com
lando drush cr
```

### 11) Acesse

```bash
https://ecadev.lndo.site
```

### 12) Logue com seu usuário Drupal

```bash
https://ecadev.lndo.site/user
```

### 13) Compilando o tema eca

```bash
cd seuprojeto
lando npm install --global gulp-cli
cd docroot/themes/custom/eca
lando gulp compile
lando gulp watch
```

### 14) Comandos

#### Recompila o projeto
```bash
lando rebuild -y
```

#### Composer install no projeto
```bash
lando composer install
```

#### Só para testar o override de configurações php no arquivo php.ini
```bash
lando php -i | grep upload_max_filesize
```

#### Para iniciar o projeto
```bash
lando start
```

#### Informações do projeto
```bash
lando info
```

#### Se tem mais projetos iniciando com o mesmo exemplo de .lando.yml, certifique-se de os outros porjetos estão parados. Para isso vá na pasta do projeto que não vai utilizar no momento e execute
```bash
lando stop
```

## Sobre o Lando

O Lando também possui outros comandos de acordo com o recipiente utilizado, Ex. Drupal8, https://docs.lando.dev/config/lamp.html#tooling

O Lando possui recipientes para outros Frameworks (Symfony) e CMS's (Drupal e Wordpress), https://docs.lando.dev/config/recipes.html#supported-recipes
