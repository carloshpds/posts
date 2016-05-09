
<h3> 
  <i>Intro</i>
</h3>

Olá, meu nome é <a href="https://github.com/carloshpds">Carlos Henrique</a>, tenho 22 anos e sou front-end engineer na equipe <a href="http://www.holmesdoc.com/">Holmes</a> da redspark.

Hoje o post será algo bem simples, extremamente rápido, porém algo que as pessoas me perguntam com muita frequência no mundo do AngularJS: 
"Como acessar a instância de uma factory ou service diretamente do console?".


<h3> 
  <i>Why!?</i>
</h3>

<h3> 
  <i>Contexto</i>
</h3>

Ter uma ferramente para tal fim quando se trata de diretivas e/ou providers detentores de escopos ($scope) é algo bem comum, pois assim temos acesso ao estado do escope. 
Ferramentas como o <a href="https://chrome.google.com/webstore/detail/angularjs-batarang/ighdmehidhipcmcojjgiloacoafjmpfk">Batarang</a> fazem isto perfeitamente. 

O porém é que estas ferramentas se baseiam no DOM para construir a árvore de scopes. 
O AngularJS provê as classes `ng-scope` e `ng-isolate-scope` para que as ferramentas identifiquem os elementos detentores de escopo e com uma instrução simples podemos ter o estado dos mesmos:

[markdown]
```
  var elements = angular.element('.ng-scope').toArray();
  elements.forEach((el) => { console.log( angular.element(el).scope() ) });
```
[/markdown]

Como nosso foco é acessar recurso que não se encontra no DOM, precisamos ter outra abordagem, precisamos acessar 

Alías, é sobre apenas uma linha:

[markdown]
```
  angular.element('body').injector()
```
[/markdown]

