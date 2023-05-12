# Sobre o jogador

- Joga a letra com maior probabilidade de acerto,

- Remove possibilidades com base na letra **estar** ou **não** presente na palavra. Caso ela esteja, ganhamos informação e reduzimos a quantidade de palavras possíveis, sem perder vidas, caso não, reduzimos a quantidade de possibilidades pelo máximo possível naquele cenário.

- Eventualmente reduz o universo de probabilidades o bastante para sobrar apenas uma, ou

- Caso suas vidas acabem antes disso, chuta uma palavra aleátoria dentre aquelas que são prováveis.



# Similaridades com a Árvore de Huffman

Quando levamos em conta informações reduziveis a 'sim' ou 'não', como no nosso caso 'a letra **estar** ou **não** presente na palavra', podemos usar parte da lógica da Árvore de Huffman para demonstrar o funcionamento do sistema. 

Esta lógica, em termos simples, hierarquiza 'perguntas' e registra suas 'respostas' de forma binária, afim de minimizar o uso de bits para representar dados, comulmente caracteres.

Construimos esta árvore de baixo para cima, agrupando as letras com menor probabilidade de aparecer em grupos de dois, começando das duas menores.

Por exemplo, a árvore de huffman para a palavra 'abacate' ficaria como a seguir:

![alt text](abacate.jpg)
- Uma letra/conjunto seguida de interrogação simboliza a pergunta "é esta letra/conjunto?"
- "N" e "S" equivalem as respostas sim ou não a pergunta de cima, traduzidas em 0 ou 1 na hora de utilizar a árvore.

Observe que, apesar de normalmente construirmos essa árvore de baixo para cima, a navegamos no sentido contrário para fazermos perguntas, para garantir que estamos usando a menor quantidade possível de bits.

Esse método garante o menor uso de bits quanto possível por minimizar a quantidade necessária para obter uma letra com base na sua probabilidade de ocorrência.

# O algoritmo

No nosso caso, seguir a ordem estabelecida por uma árvore de huffman servirá para minimizarmos a perda de vidas, pois sempre estaremos tentando letras mais prováveis primeiro.

Quando aplicamos a lógica da arvore de huffman na implementação do nosso algoritmo, obtemos uma árvore similar a esta:

![alt text](forca.jpg)

- Nesse caso, assumimos que havia somente quatro palavras possíveis restantes: "arvore", "modera", "navega" e "filete".

Na imagem, descrevemos o seguinte comportamento de busca:

- verificamos que a letra mais frequente é 'e' e tentamos:
    - eliminamos uma alternativa sem 'e',
    - definimos alternativas restantes com base na posição dos 'e's encontrados.
- verificamos que a letra mais frequente é 'a' e tentamos:
    isso nos permite diferenciar entre 'modera' e 'navega', o que nos dá a resposta na próxima rodada.

Observe que a base do comportamento funciona como huffman.

Dentro do código, não precisamos nos preocupar com a aparencia ou informações da árvore depois do passo que estamos, pois é preciso apenas filtrar nossas possibilidades entre "contêm letra mais frequente" ou não a cada passo. 

Além disso, como eliminamos casos não importando se acertamos ou não devido a natureza do jogo, precisamos calcular a letra mais frequente no estado atual para cada interação.

Concluindo, utilizamos uma lógica similar a da arvore de hufman na implementação do nosso algoritmo, buscando maximizar a nosso ganho de informação enquanto conseguiamos alta prioridade para ocorrências comuns, o que ultimamente gerou a precisão registrada na demonstração.


## Caso haja dúvidas quanto a implementação aqui descrita, vide `demo.py`