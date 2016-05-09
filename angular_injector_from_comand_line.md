
<h3> 
  <i>Intro</i>
</h3>

Olá, meu nome é <a href="https://github.com/carloshpds">Carlos Henrique</a>, tenho 22 anos e sou front-end engineer na equipe <a href="http://www.holmesdoc.com/">Holmes</a> da redspark.

Hoje o post será algo bem simples, extremamente rápido, porém algo que as pessoas me perguntam com muita frequência no mundo do AngularJS: 
"Como acessar a instância de uma factory ou service diretamente do console?".


<h3> 
  <i>Contexto</i>
</h3>

Se ter uma ferramente para tal fim quando se trata de diretivas e/ou providers detentores de escopos ($scope) é algo bem comum, pois assim temos acesso ao estado do escope. 
Ferramentas como o <a href="https://chrome.google.com/webstore/detail/angularjs-batarang/ighdmehidhipcmcojjgiloacoafjmpfk">Batarang</a> fazem isto perfeitamente. 

Mas como estas ferramentas se baseiam no DOM para construir a árvore de scopes, não temos o conteúdo "abstrato". 
O AngularJS provê as classes `ng-scope` e `ng-isolate-scope` para que estas ferramentas identifiquem o elemento detentor do escopo.

Alías, é sobre apenas uma linha:

[markdown]
```
  angular.element('body').injector()
```
[/markdown]

