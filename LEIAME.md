# PT-BR

A diferença é que no caso de se utilizar  `==`  haverá uma coerção do valor para que ambos os lados da expressão tenham o mesmo tipo.

No caso do  `===`  não haverá coerção e por isso o código abaixo dará falso:

```
if(1 === '1')
    console.log('igual');
else
   console.log('diferente');//Esta será a resposta
```

Já se utilizarmos somente  `==`  haverá uma coerção para que ambos sejam o mesmo tipo e dará igual.

```
if(1 == '1')
    console.log('igual');//Esta será a resposta
else
   console.log('diferente');
```

Outro exemplo:

```
if(0 == '')
    console.log('igual');//Esta será a resposta
else
   console.log('diferente');
```

No caso  `''`  é considerado um valor  `falsey`, que pode ser considerado falso mesmo não tendo o valor  `false`.

Já no caso abaixo é dada a mensagem correta, que são diferentes:

```
if(0 === '')
    console.log('igual');
else
   console.log('diferente');//Esta será a resposta
```

Seguem alguns outros valores que podem resultar em casos estranhos na comparação lógica em  `javascript`:

Dão falso:

```
0
''
' '
null
undefined
NaN
```
