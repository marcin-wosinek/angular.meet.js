### AngularJs
## meet.js 27 lutego 2013

### Kim jestem?
* Marcin Wosinak
* 5 lat doświadczenia w IT
  * WebDev: Javascript
  * C# dev: UnitTests
* Aktualnie kontraktor w Roche

### Wy?

* Kto już pracował z angularem?
* Kto lubi unit testy?
* Kto używa yeomana?

### Czym jest angular?

* framework aplikacji
* 29KB zminimalizowany i spakowany
 * backbone: 19KB (z underscore & backbone)
 * backbone: 32KB (z lodash & jQuery)
 * ember: 49KB
* brak zależności:
 * może używać jQuery, o ile jest dostępne przy uruchomieniu

### AngularJs
* MVVM [G+] [1]
* Proste objekty js
* Wstrzykiwanie zależności
* TESTOWALNOŚĆ!
* Directives
* Programowanie deklaratywne

### Architektura MVVM
* proste objekty js
* sprawdzanie wszystkich zmian po kolecji - ale object.observer nadchodzi

```js
function TodoCtrl($scope, $log) {
  // use console log
  $log.log('Test');

  $scope.addTodo = function() {
    $scope.todos.push({text:$scope.todoText, done:false});
    $scope.todoText = '';
  };
 
  $scope.remaining = function() {
    var count = 0;
    angular.forEach($scope.todos, function(todo) {
      count += todo.done ? 0 : 1;
    });
    return count;
  };
 
  $scope.archive = function() {
    var oldTodos = $scope.todos;
    $scope.todos = [];
    angular.forEach(oldTodos, function(todo) {
      if (!todo.done) $scope.todos.push(todo);
    });
  };
}
```

### Wstrzykiwanie zależności
* usprawnia testowanie
* ładnie posumowywuje powiązania między częściami aplikacji

```js
$scope; // view model
$log; // console: ie friendly
$window; // testable window counter part
$http; // http requests
// and all our services
```

### Directives
* narzędzie do uczenia html nowych sztuczek
 * dowiązuje kontrolery

```html
<div ng-controller="ProductCtrl">
```

 * pętle

```html
<ul>
  <li ng-repeat="friend in friends">
    [{{$index + 1}}] {{friend.name}} who is {{friend.age}} yrs old.
 </li>
</ul>
```

 * dowiązanie modelu

```html
<input type="checkbox" ng-model="confirmed" ng-change="change()"
```

* wskrzeszanie dawnych featureów

```html
<blink>Click me</blink>
```

* Brak manipulacji DOMem w kontrolerze

### Programowanie deklaratywne
* Czyli to co mamy w html, css a teraz też w js
* html: chcesz paragraf?

```html
<p>Text</p>
```

* css: chcesz go na czarwono?

```css
p { color: red}
```

* js: dowiązujemy zawartość do module - co piszemy w zwykłym html

```html
<p>{{modelData}}</p>
```

### TESTOWALNOŚĆ!
* Wstrzykiwanie zależności
* Directives
* proste objekty js jako modele

```js
//Code:
function PasswordCtrl($scope) {
  $scope.password = '';
  $scope.grade = function() {
    var size = $scope.password.length;
    if (size > 8) {
      $scope.strength = 'strong';
    }
    else if (size > 3) {
      $scope.strength = 'medium';
    }
    else {
      $scope.strength = 'weak';
    }
  };
}

// test:
var scope = {};

var pc = new PasswordCtrl(scope);
pc.password('abc');
pc.grade();
expect(scope.strength).toEqual('weak');
```

### Wątpliwości
* dla niektórych nawet deal breaker

### Walidatorom się to nie spodoba
* niestandardowe tagi

```html
<tabs>
   <pane title="Localization">
```

* niestandardowe atrybuty

```html
<li ng-repeat="todo in todos">
<input type="text" ng-model="todoText" />
```

* a część z nich była specjanie usunięta z html

```html
<blink>CLICK ME!</blink>
```

### Powrót do lat 90?
* angular używa własnych tagów, pozwala nam tworzyć kolejne, i oczekuje że będziemy pisać takie rzeczy:

```html
<form ng-submit="addTodo()">
<button ng-click="fireAlert()">
```

### Błedne tagi
* wszystkie directives
* dla atrybutów jest wersja z data-\* or x-\* 
* dodatkowe tagi potrzebują shimów dla ie8

### Nie - to nasza przyszłość
* web components
* shadow dom 

Będą podobne api w przeglądarkach. Już teraz możemy korzystać z części możliwości - dzięki angularowi.
A wszystko jest bezpiecznie wydzielone w scopy.

### Shadow DOM
* Uzywane wewnętrzenie przez przeglądarki do tworzenia kontrolek
* Wystawi te same funkcjonalności do web developerów
* Szkic roboczy http://www.w3.org/TR/shadow-dom/
* Przyjemny opis http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/ 


### Yeoman
* CLI
* super narzędzie do tworzenia kodu
* wypycha zmainy z serwera do przeglądarki - bez odświerzania

### Testacular
* Test runner
* Odpala testy w prawdziwych przeglądarkack
* Pracuje na linuxie, nie potrzebuje graficznego środowiska
* Build by angular team, all angular tests are on testacular
* Zbudowany przez team angulara, wszystkie testy angulara są oparte o testacular
* Pracuje z jasmine, sinon

### Chcecie sprawdzić?
* Przygotowałem maszyne ze środowiskiem developerskim
* Pełna maszyna https://docs.google.com/folder/d/0Bzhquk4DfXAtYUhKNlJhb01jaEk/edit?usp=sharing - oparta o ubuntu server
 * user: developer
 * hasło: developer
* Skrypt instalujący https://github.com/marcin-wosinek/angular-dev

### Jak zacząc z angularem?
* Is possible to use in legacy projects
* Da się używać z legacy code
* Goes well allong with jquery
* Dogaduje się z jquery
* Istnieje projekt przepisania bootstrapowego js do angulara [angular-ui-bootstrap] [2]
* They say it is possible to use it along with require.js [angular-require-js] [3]
* Mówią że da się korzystać z require.js [angular-require-js] [3]

### Pytania?
* Jeśli twój css nie działa dobrze z ng-show i ng-hide spróbuj ui-if z angular-ui

### Gdzie można mnie złapać
* marcin.wosinek@gmail.com
* \#marcin.wosinek
* podsumowanie i linki:
* http://marcin-wosinek.github.com/angular.meet.js

[1]: https://plus.google.com/+AngularJS/posts/aZNVhj355G2   "G+"
[2]: http://angular-ui.github.com/bootstrap/   "angular-ui-bootstrap"
[3]: https://github.com/elsom25/angular-requirejs-html5boilerplate-seed   "angular-require-js"
