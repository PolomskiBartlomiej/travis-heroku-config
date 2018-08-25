[![Build Status](https://travis-ci.com/mtumilowicz/travis-heroku-config.svg?branch=master)](https://travis-ci.com/mtumilowicz/travis-heroku-config)

# travis-heroku-config
Configuration of CI / CD (travis, heroku).

# manual
* connect travis to github:
    1. Go to Travis-ci.com and Sign up with GitHub.
    1. Accept the Authorization of Travis CI. You’ll be redirected to GitHub.
    1. Click the green Activate button, and select the repositories you want to use with Travis CI.
    1. Add a `.travis.yml` file to your repository to tell Travis CI what to do.

* `.travis.yml` with deploy to heroku
    * gradle wrapper
        ```
        language: java
        jdk: oraclejdk8
        
        before_install:
          - chmod +x gradlew
        
        branches:
          only:
          - master
        
        deploy:
          provider: heroku
          api_key:
            secure: $HEROKU_KEY_API
          app: mtumilowicz-hello
        ```
            
    * maven wrapper
        ```
        language: java
        jdk: oraclejdk8
        
        before_install:
          - chmod +x mvnw
        
        branches:
          only:
          - master
        
        deploy:
          provider: heroku
          api_key:
            secure: $HEROKU_KEY_API
          app: mtumilowicz-hello
        ```        
        
* HEROKU_KEY_API
    1. download and install `heroku-cli`: https://devcenter.heroku.com/articles/heroku-cli
    1. log in:
        ```
        $ heroku login
        
        Enter your Heroku credentials.
        
        Email: ...
        Password: ...
        ```
    1. generate $HEROKU_KEY_API
        ```
        heroku auth:token
        ```
    1. set HEROKU_KEY_API in Environment Variables of a project on travis

# project description
* CI using travis
* CD using travis & heroku
* prints hello on default URL:
    https://mtumilowicz-hello.herokuapp.com/
* use of spring boot actuator:
    https://mtumilowicz-hello.herokuapp.com/actuator/health