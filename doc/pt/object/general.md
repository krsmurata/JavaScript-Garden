## Uso de Objetos e Propriedades

Tudo em Javascript se comporta como um objeto, com duas exceções que são
[`null`](#core.undefined) e [`undefined`](#core.undefined).

    false.toString() // 'false'
    [1, 2, 3].toString(); // '1,2,3'
    
    function Foo(){}
    Foo.bar = 1;
    Foo.bar; // 1

Uma ideia errada muito comum é que [literais numéricos][2] não podem ser usados
como objetos. Isso ocorre porque uma falha no *parser* do JavaScript tenta
interpretar a *notação de ponto* junto com o número como um ponto flutuante literal.

    2.toString(); // retorna SyntaxError

Existem algumas soluções para fazer literais numéricos se comportarem
como objetos.

    2..toString(); // o segundo ponto é interpretado de forma correta
    2 .toString(); // note o espaço do lado esquerdo do ponto
    (2).toString(); // 2 é analisado primeiro

### Objetos como Tipos de Dados

Objetos em JavaScript também podem ser usados como um [*Hashmap*][1], que
basicamente é uma lista de nomes de propriedades e valores.

Usando um objeto literal - notação `{}` - é possível criar um objeto simples.
Esse novo objeto [herda](#object.prototype) de `Object.prototype` e 
não possui [propriedades próprias](#object.hasownproperty) definidas nele.

    var foo = {}; // um novo objeto vazio

    // um novo objeto com a propriedade chamada 'test' e valor 12
		var bar = {test: 12}; 

### Acessando Propriedades

As propriedades de um objeto podem ser acessadas de duas formas: usando tanto
a *notação de ponto* ou a *notação de conchetes*.
    
    var foo = {name: 'kitten'}
    foo.name; // kitten
    foo['name']; // kitten
    
    var get = 'name';
    foo[get]; // kitten
    
    foo.1234; // SyntaxError
    foo['1234']; // works

Ambas notações são identicas em como elas se comportam, com a única diferença sendo
a notação com colchetes que possibilita a configuração dinâmica das propriedades, bem como
o uso de nomes de propriedades que do contrário gerariam  *syntax error*.

### Removendo Propriedades

O único jeito de remover uma propriedade de um objeto é usando o operador
`delete`. Note que atribuindo `undefined` ou `null` para a propriedade somente remove
o *valor* associado à propriedade, mas não a *key*.

    var obj = {
        bar: 1,
        foo: 2,
        baz: 3
    };
    obj.bar = undefined;
    obj.foo = null;
    delete obj.baz;

    for(var i in obj) {
        if (obj.hasOwnProperty(i)) {
            console.log(i, '' + obj[i]);
        }
    }

O código acima imprimi ambos `bar undefined` e `foo null`, somente `baz`
foi removido e por isso não está na saída.

### Notação das Keys

    var test = {
        'case': 'Sou uma keyword e preciso ser escrito explicitamente como string',
        delete: 'Sou uma keyword também' // retorna SyntaxError
    };

Propriedades de objetos podem ser escritas como simples palavras ou como *strings*
(com aspas duplas ou simples). Por causa de outro erro no design do *parser*
do JavaScript o código acima irá disparar `SyntaxError` antes da versão ECMAScript 5.

Esse erro acontece porque `delete` é uma *keyword*, portanto precisa ser escrita
como uma *string literal* para garantir que irá ser corretamente interpretada por
versões mais antigas da *engine* JavaScript.

[1]: http://en.wikipedia.org/wiki/Hashmap
[2]: https://developer.mozilla.org/index.php?title=pt/JavaScript/Guia/Valores%2C_Vari%C3%A1veis_e_Literais#Literais
