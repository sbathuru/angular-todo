## Angular local Execution
Prereqisties:
1) Install Node.js
2) Install npm : 
   upgrade npm : $ npm install -g npm
3) Install angular/cli
     $ npm install -g @angular/cli

Application
     Application package Install : $ npm install <br>
     Application Build           : $ npm build.  <br>
     Application Run             : $ ng serve    <br> 
                                   $ npm start.  <br>
     Application Access          : http://localhost:4200


### Docker Build Local Steps
1. /Users/srinivas/devops/git/angular-todo
2. docker build -t sbathuru/angular-todo:latest .
3. docker push sbathuru/angular-todo:latest 
4. docker run -p 4200:80 --name angular-todo sbathuru/angular-todo
