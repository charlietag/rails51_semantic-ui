# semantic-ui installation

## Environment
* Nginx - Passenger
* Database - MariaDB 10.1
* Ruby 2.4.1
* Rails 5.1.4

## Start from scratch
* rails new -d mysql rails51_semantic-ui
* cd rails51_semantic-ui
  * rm .gitignore
  * wget https://raw.githubusercontent.com/charlietag/os_preparation/master/templates/F_09_create_rails/home/myrails/.gitignore
  * bundle exec rails g scaffold post title:string content:text
  * bundle exec db:create
  * bundle exec db:migrate
  * semantic.json

    ```bash
    cat > semantic.json <<!
    {
      "base": "semantic/",
      "paths": {
        "source": {
          "config": "src/theme.config",
          "definitions": "src/definitions/",
          "site": "src/site/",
          "themes": "src/themes/"
        },
        "output": {
          "packaged": "../node_modules/semantic-ui/dist/",
          "uncompressed": "../node_modules/semantic-ui/dist/components/",
          "compressed": "../node_modules/semantic-ui/dist/components/",
          "themes": "../node_modules/semantic-ui/dist/themes/"
        },
        "clean": "../node_modules/semantic-ui/dist/"
      },
      "permission": false,
      "autoInstall": true,
      "rtl": false
      "rtl": false,
      "version": "2.2.13" # will be added back after yarn add semantic-ui
    }
    !
    ```

  * yarn add semantic-ui
  * modify app/assets/{{javascripts,stylesheets}}/
  * modify app/views/index.html.erb
  * semantic-ui theming
    * cd semantic
      * Fix semantic setting to do "gulp build-css"
        * sed -i 's/compressedStream = stream$/compressedStream/g' tasks/build/css.js
      * v src/theme.config
      * /home/rails51_semantic-ui/node_modules/gulp/bin/gulp.js build

## Leverage this project
* git clone https://github.com/charlietag/rails51_semantic-ui.git
* cd rails51_semantic-ui
  * modify database setting
    * config/database.yml.sample ---> config/database.yml
    * bundle exec db:create
    * bundle exec db:migrate
  * bundle install
  * yarn install
