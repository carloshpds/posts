
<h3> 
  <i>Intro</i>
</h3>

Olá, meu nome é <a href="https://github.com/carloshpds" target="_blank">Carlos Henrique</a>, tenho 22 anos e sou front-end engineer na equipe <a href="http://www.holmesdoc.com/" target="_blank">Holmes</a> da redspark.

Hoje o post será algo bem simples, extremamente rápido, porém algo que as pessoas me perguntam com muita frequência no mundo do AngularJS: 
"Como acessar a instância de uma factory ou service diretamente do console?".

PS: Os exemplos estarão em ES2015, então talvez seja necessário verificar a compatibilidade do browser. Apenas troque <i>let</i> por <i>var</i> e <i>=></i> por <i>function</i> que terá a compatibilidade para todos os browsers. :)

<h3> 
  <i>What!? Why!?</i>
</h3>

Caso não tenha passado por tal necessidade, o motivo desta ação pode ficar meio obscuro. Então pense nas seguintes situações:

1 - Mantemos os dados do usuário em uma factory, pois como as mesmas são singleton, sempre iremos acessar o mesmos dados na aplicação inteira. Com isso, gostariamos de verificar o estado destes dados em um ponto específico da aplicação, mas apenas para uma consulta rápida.

2 - Temos uma factory qual serve como interação para um loader, possuí métodos para iniciar e parar o mesmo. Gostaríamos de iniciar tal interação de forma controlada, então nada melhor que chamar os métodos diretamente do console.

Iremos seguir com a segunda situação.

<h3> 
  <i>Abordagem por escopo</i>
</h3>

Ter uma ferramente para tal fim quando se trata de diretivas e/ou providers detentores de escopos ($scope) é algo bem comum, pois assim temos acesso ao estado do escope. 
Ferramentas como o <a href="https://chrome.google.com/webstore/detail/angularjs-batarang/ighdmehidhipcmcojjgiloacoafjmpfk">Batarang</a> fazem isto perfeitamente. 

O porém é que estas ferramentas se baseiam no DOM para construir a árvore de scopes. 
O AngularJS provê as classes <strong>ng-scope</strong> e <strong>ng-isolate-scope</strong> para que as ferramentas identifiquem os elementos detentores de escopo e com uma instrução simples podemos ter o estado dos mesmos:

[markdown]
```javascript
  let elements = angular.element('.ng-scope').toArray();
  elements.forEach((el) => { console.log( angular.element(el).scope() ) });
```
[/markdown]

Como nosso foco é acessar recurso que não se encontra no DOM, precisamos ter outra abordagem.


<h3> 
  <i>Solução - Injector</i>
</h3>

Aos que conhecem o AngularJS um pouco melhor, sabem que o responsável pela injeção de dependência de todos os recursos é o <strong>$injector</strong>.

Como sabemos que a instância de factories e/ou services são únicas, só precisamos acessa-las via injector. O que muitos não sabem é que há uma maneira bem simples de acessa-lo a partir do console.

Primeiramente devemos conhecer o elemento raiz da aplicação, aquele qual vai o <i>ng-app</i> ou recebe o <i>bootstrap</i> do AngularJs. Sabendo isto, podemos considerar este e todos os elementos filhos possuem acesso ao injector:  

[markdown]
```javascript
  let injector = angular.element(document).injector();
```
[/markdown]

Executando a linha acima temos acesso a todas as funcionalidades do injector. Utilizaremos o método <i>get</i> para acessar nosso loader que chamaremos de <strong>redLoader</strong>.

[markdown]
```javascript
  let injector = angular.element(document).injector();
  let loader   = injector.get('redLoader');
  loader.start();
```
[/markdown]

A interação com o loader acontece normalmente via console. Assim podemos executar testes rapidamente, sem mexer no código e sem ter que recarregar a aplicação pra ver a alteração.

Uma outra situação interessante é verificar se um provider existe utilizando o método <i>has</i>, pois assim podemos entender melhor carregamento dinâmico ou <i>breaking changes</i> de terceiros.

[markdown]
```javascript
  let injector = angular.element(document).injector();
  injector.has('redLoader');
  -> true
```
[/markdown]

<h3> 
  <i>That's all folks</i>
</h3>

É isso aí galera! Qualquer dúvida podem me mandar no <a href="https://twitter.com/carloshpds2" target="_blank">twitter</a> ou no <a href="https://github.com/carloshpds" target="_blank">github</a>, até o próximo post! :)
