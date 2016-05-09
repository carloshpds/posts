
<h3> 
  <i>Intro</i>
</h3>

Olá, meu nome é <a href="https://github.com/carloshpds">Carlos Henrique</a>, tenho 22 anos e sou front-end engineer na equipe <a href="http://www.holmesdoc.com/">Holmes</a> da redspark.

Hoje o post será algo bem simples, extremamente rápido, porém algo que as pessoas me perguntam com muita frequência no mundo do AngularJS: 
"Como acessar a instância de uma factory ou service diretamente do console?".


<h3> 
  <i>What!? Why!?</i>
</h3>

Caso não tenha passado por tal necessidade, o motivo desta ação pode ficar meio obscuro. Então pense nas seguintes situações:

1 - Mantemos os dados do usuário em uma factory, pois como as mesmas são singleton, sempre iremos acessar o mesmos dados na aplicação inteira. Com isso, gostariamos de verificar o estado destes dados em um ponto específico da aplicação, mas apenas para uma consulta rápida.

2 - Temos uma factory qual serve como interação para um loader, possuí métodos para iniciar e parar o mesmo. Gostaríamos de iniciar tal interação de forma controlada, então nada melhor que chamar os métodos diretamente do console.

<h3> 
  <i>Abordagem por escopo</i>
</h3>

Ter uma ferramente para tal fim quando se trata de diretivas e/ou providers detentores de escopos ($scope) é algo bem comum, pois assim temos acesso ao estado do escope. 
Ferramentas como o <a href="https://chrome.google.com/webstore/detail/angularjs-batarang/ighdmehidhipcmcojjgiloacoafjmpfk">Batarang</a> fazem isto perfeitamente. 

O porém é que estas ferramentas se baseiam no DOM para construir a árvore de scopes. 
O AngularJS provê as classes <strong>ng-scope</strong> e <strong>ng-isolate-scope</strong> para que as ferramentas identifiquem os elementos detentores de escopo e com uma instrução simples podemos ter o estado dos mesmos:

[markdown]
```javascript
  var elements = angular.element('.ng-scope').toArray();
  elements.forEach((el) => { console.log( angular.element(el).scope() ) });
```
[/markdown]

Como nosso foco é acessar recurso que não se encontra no DOM, precisamos ter outra abordagem.


<h3> 
  <i>Solução - Injector</i>
</h3>

Aos que conhecem o AngularJS um pouco melhor, sabem que o responsável pela injeção de dependência de todos os recursos é o <strong>$injector</strong>.

Como sabemos que a instância de factories e/ou services são únicas, só precisamos acessa-las via injector. O que muitos não sabem é que há uma maneira bem simples de acessa-lo a partir do console.


[markdown]
```
  angular.element('body').injector()
```
[/markdown]

