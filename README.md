# ADO 4

## O que desenvolver

Seus usuários são treinadores de pokémons que desejam encontrar pokémons para capturar.

Para facilitar o trabalho deles, crie um pequeno sistema que os ajude a encontrar seus pokémons.

Para isso, eles devem usar o seu pequeno sistema onde informam um CEP brasileiro e obtém como resposta os dados que informam qual CEP é esse
e qual é o pokémon mais comum no logradouro correspondente.

## Organização dos grupos.

O trabalho deve ser feito em grupos de 1 a 4 pessoas.
Preferencialmente, os mesmos grupos com os mesmos membros dos trabalhos anteriores.

## O que usar para desenvolver

O sistema deve ser desenvolvido com uma (e apenas uma) dessas opções:

* Em PHP 8.1 ou superior usando [curl](https://www.php.net/manual/en/curl.examples-basic.php). O uso ou não do Laravel é opcional.

* Em Java 8 ou superior utilizando [HttpURLConnection](https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/net/HttpURLConnection.html).

* Em Java 11 ou superior utilizando [HttpClient](https://docs.oracle.com/en/java/javase/20/docs/api/java.net.http/java/net/http/HttpClient.html).

* Em Python utilizando [Flask](https://flask.palletsprojects.com/en/2.3.x/) e [Requests](https://requests.readthedocs.io/en/latest/).

## Procedimentos da implementação

1. Consulte os dados do CEP no site [https://viacep.com.br/ws/XXXXX-XXX/json](https://viacep.com.br/ws/01001-000/json), onde XXXXX-XXX é o CEP a ser pesquisado.

2. Se o CEP existir, usando o terceiro, quarto e quinto dígitos do CEP, pesquise o pokémon correspondente
no site [https://pokeapi.co/api/v2/pokemon/NNN](https://pokeapi.co), onde NNN é o número do pokémon (obtido do CEP). Retire os zeros à esquerda de NNN se houver.

3. Retorne um JSON para o usuário contendo os seguintes dados:

```javascript
{
    "ok": true,

    // Este é o CEP informado.
    "cep": "XXXXX-XXX",

    // Este é o nome da rua trazido pelo viacep.
    "logradouro": "Rua X",

    // Este é o "bairro" trazido pelo viacep.
    "bairro": "Vila XYZ",

    // Este é o campo "localidade" trazido pelo viacep.
    // Perceba que o viacep chama de "localidade" ao invés de "cidade".
    "cidade": "Nome da cidade",

    // Este é o "uf" trazido pelo viacep.
    "uf": "SIGLA",

    // Nome do pokémon encontrado ou "N/A" se a pokéapi não encontrar nenhum.
    "pokemon": "nome",

    // O número do pokémon ou 0 se nenhum for encontrado.
    "numero-pokemon": 123,

    // Link da foto do pokémon ou uma string em branco se a pokéapi não encontrar o pokémon.
    // Pegue essa foto no JSON da pokeapi ao atravessar os campos sprites->other->official_artwork->front_default.
    // Ou, apenas substitua o número no final se o pokémon existir.
    "foto-pokemon": "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png"
}
```

4. Se o CEP não existir, retorne isso:

```javascript
{
    "ok": false
}

5. Certifique-se que a página em HTML anexa disponibilizada pelo professor contendo um Javascript fazendo AJAX consegue ler e exibir os dados informados.
