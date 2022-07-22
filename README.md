# FirstAngularApp

## Angular local Execution
Prereqisties:
1) Install Node.js

2) Install npm : 
   upgrade npm : $ npm install -g npm

3) Install angular/cli
     $ npm install -g @angular/cli

Application
     Application package Install : $ npm install 
     Application Build           : $ npm build

     Application Run             : $ ng serve
                                   $ npm start
     Application Access          : http://localhost:4200


### Docker Build Local Steps
1. /Users/srinivas/devops/git/angular-todo
2. docker build -t sbathuru/angular-todo:latest .
3. docker push sbathuru/angular-todo:latest 
4. docker run -p 4200:80 --name angular-todo sbathuru/angular-todo


# This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 11.0.4.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.
