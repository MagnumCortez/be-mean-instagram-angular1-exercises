# AngularJS 1.5.x - Aula 03 - Exercício  
**user:** [ednilsonamaral](https://github.com/ednilsonamaral)  
**autor:** Ednilson Amaral  
**data:** 1468631267387


## Criar uma função que para ordenar uma tabela a partir de uma coluna, clicando na sua tr > th, ordenando pelo campo da coluna.

## Criar mais 1 Controller para Teachers com seu form para adição, listagem (defina um Array inicial) com a ordenação do exercício anterior, filtro filter e também o use o seu filtro criado na segunda aula.


```html
<!DOCTYPE html>
<html lang="pt-br" data-ng-app="aula05">
<head>
    <meta charset="utf-8">
    <title>Be MEAN - AngularJS - Aula 05 - Exercícios</title>

    <style>
        body{
            background-color: rgba(249, 269, 168, .5);
            font-size: 20px;
            color: #696969;
        }
    </style>
</head>

<body data-ng-controller="TeachersController">
    <!-- CONTROLLER DE TEACHERS -->
    <h1>{{ titulo }}</h1>

    <label>
        Busca por professor:
        <input data-ng-model="searchTeacher">
    </label>

    <table>
        <thead>
            <tr>
                <th data-ng-repeat="(key, value) in teachers[0]">
                    <a href="" data-ng-click="orderne(key)">
                        {{ key }}
                    </a>
                </th>
            </tr>
        </thead>

        <tbody>
            <tr data-ng-repeat="teacher in teachers | orderBy:predicate:reverse | filter:searchTeacher">
                <td data-ng-repeat="(key, value) in teacher">{{ value }}</td>
            </tr>
        </tbody>
    </table>

    <!-- CONTROLLER DE OLD TEACHERS -->
    <span data-ng-init="teacherOrder = 'disciplina'; teacherReverse = false;"></span>

    <div data-ng-controller="MasterController">
        <h1>{{ titulo }}</h1>

        <label>
            Busca por professor:
            <input data-ng-model="searchTeacher">
        </label>

        <p>
            <label>
                Nome:
                <input type="text" data-ng-model="form.User.name">
            </label>

            <br>

            <label>
                Idade:
                <input type="num" data-ng-model="form.User.age">
            </label>

            <br>

            <label>
                Sexo:
                <input type="text" data-ng-model="form.User.sex">
            </label>

            <br>

            <label>
                Disciplina:
                <input type="text" data-ng-model="form.User.disciplina">
            </label>
        </p>

        <button data-ng-click="add(form.User)">ADD</button>

        <table>
            <thead>
                <tr>
                    <th data-ng-repeat="(key, value) in oldt[0]">{{ key }}</th>
                </tr>
            </thead>

            <tbody>
                <tr data-ng-repeat="teacher in oldt | orderBy:teacherOrder:teacherReverse | filter:searchTeacher">
                    <td data-ng-repeat="(key, value) in teacher">{{ value }}</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.5/angular.min.js"></script>

    <script>
        var app = angular.module('aula05', []);

        // Controllers
        app.controller('TeachersController', TeachersController);
        app.controller('MasterController', MasterController);

        // Filter
        app.filter('checkAge', function() {
            return function(num){
                if(num<18) return "Menor de idade!";
                else return "Maior de idade, tá fudido!";
            }
        });

        // Objects
        function TeachersController($scope){
            $scope.titulo = "Be MEAN - Lista de Professores";
            $scope.teachers = [
                {name: 'Suissa', age: '30', sex:'m', linguagem: 'javascript'},
                {name: 'Giovana', age: '29', sex:'f', linguagem: 'angular'},
                {name: 'Bruna', age: '55', sex:'f', linguagem: 'html'},
                {name: 'José Santos', age: '17', sex:'m', linguagem: 'css'}
            ];

            $scope.add = add;
            function add(){
                $scope.cursos.push({
                    name: 'Ednilson',
                    age: '24',
                    sex: 'm',
                    linguagem: 'front-end'
                });
            }

            $scope.predicate = '';
            $scope.reverse = false;

            $scope.orderne = function(key){
                //console.log("VSF, CONSEGUI ESSA PORRETINHA!");

                if (key == $scope.predicate){
                    $scope.reverse = !$scope.reverse;
                } else {
                    $scope.predicate = key;
                    $scope.reverse = false
                }
            }
        }

        function MasterController($scope){
            $scope.titulo = "Be MEAN - Lista de Professores Antigos (OS MAIS FODAS PIKAS DAS GALÁXIAS)";
            $scope.oldt = [
                {name: 'Einsten', age: '30', sex:'m', disciplina: 'fisica teórica'},
                {name: 'Tesla', age: '29', sex:'m', disciplina: 'engenharia mecânica'},
                {name: 'Frank Miller', age: '55', sex:'m', disciplina: 'física - implosão'},
                {name: 'Robert Oppenheimer', age: '37', sex:'m', disciplina: 'física - energia nuclear'}
            ];

            $scope.add = add;
            function add(user){
                $scope.oldt.push(user);
            }
        }

        MasterController.$inject = ['$scope'];
    </script>
</body>
</html>
```
