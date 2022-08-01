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

### 5) Configure os arquivos:

```bash
/seuprojeto/docroot/sites/default/settings.php
/seuprojeto/docroot/sites/default/services.yml
```

### 6) Se existe destrói, recomplila o projeto, instala os pacotes, instala os pacotes Drush e Drupal Console

```bash
lando destroy -y 
lando rebuild -y 
lando composer install
lando composer require drush/drush:10.x drupal/drush drupal/console
lando ssh --service appserver --user root --command "chmod +x /app/vendor/drush/drush/drush"
lando ssh --service appserver --user root --command "chmod +x /app/vendor/drupal/console/bin/drupal"
lando rebuild -y
lando drush
lando drupal
```

### 7) Restaure o dump MySql do site 

```bash
lando db-import backup/site.sql
```

### 8) Desinstale os módulos Senha única USP e Google Analytics

```bash
lando drush pm:uninstall senhaunicausp google_analytics
```

### 9) Instale os módulos dev

```bash
lando drush pm:enable devel kint
```

### 10) Cache rebuild com Drush

```bash
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

#### Neste ponto o site está totalmente configurado para o ambiente dev

### 13) Compilando o tema eca

```bash
cd docroot/themes/custom/eca
lando npm uninstall -g gulp-cli
rm -rf node_modules
lando npm install -g gulp-cli --save-dev
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
