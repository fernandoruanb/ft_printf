<h1 style="text-align: center;">FT_PRINTF</h1>
<img src="https://cdn.pixabay.com/photo/2016/10/27/06/38/tea-time-1773531_1280.png"\>

## 📜 Sobre o Projeto

O **ft_printf** surge no **segundo milestone** da grande jornada na **École 42**.

Uma maneira simples de entender esse projeto é imaginar o **ft_printf como um garçom**.

Durante o processo de formação na 42, começamos implementando diversas funções básicas de saída.  
Entre as primeiras estão:

- `ft_putchar` → imprime um único caractere
- `ft_putnbr` → imprime um número
- `ft_putstr` → imprime uma string completa

Cada função possui uma responsabilidade específica.  
Porém, surge um problema natural:

> E se quisermos uma única função capaz de organizar e imprimir diferentes tipos de dados?

Em vez de chamar várias funções diferentes manualmente, seria muito mais interessante possuir **um sistema centralizado**, capaz de interpretar o que desejamos imprimir e então chamar internamente o serviço correto.

É exatamente aqui que entra o **ft_printf**.

Assim como um garçom em um restaurante:

1. O garçom recebe o pedido.
2. Ele interpreta o que foi solicitado.
3. Ele encaminha o pedido correto para o setor responsável.

Da mesma forma, **ft_printf recebe uma string de formatação**, interpreta seu conteúdo e chama a função interna apropriada para imprimir os dados desejados.

---

## ⚙️ Funções Variádicas

Um dos aspectos mais interessantes do **ft_printf** é o início do uso de **funções variádicas**.

Diferente das funções tradicionais, que recebem uma quantidade fixa de argumentos, as funções variádicas permitem trabalhar com **um número indefinido de parâmetros**.

Para isso utilizamos os seguintes recursos da linguagem C:

- `va_list`
- `va_start`
- `va_arg`
- `va_end`

Esses mecanismos permitem percorrer uma lista de argumentos dinamicamente, possibilitando que o programa interprete e utilize diferentes tipos de dados conforme necessário.

---

## 🎯 Objetivo do Projeto

Inspirado no **printf original da linguagem C**, o objetivo do **ft_printf** é reproduzir parte de seu comportamento, tornando seus mecanismos internos compreensíveis.

Ao implementar esse projeto do zero, aprendemos conceitos fundamentais como:

- funcionamento da saída formatada
- interpretação de strings de formatação
- uso de **argumentos variádicos**
- organização de funções de impressão de forma modular

Em outras palavras, o **ft_printf transforma o funcionamento abstrato do `printf` em algo palpável e implementável**, permitindo compreender como essa ferramenta tão poderosa realmente funciona internamente.

Aqui está seu texto **organizado em Markdown**, mantendo sua explicação técnica mas estruturando de forma clara para um **README de projeto**.

## ⚙️ Como o ft_printf Funciona

O funcionamento do **ft_printf** segue uma lógica simples, porém poderosa.

Assim como o `printf` original da linguagem C, a função **sempre retorna a quantidade total de caracteres que foram impressos**.

### 1. Inicialização dos argumentos variádicos

Primeiramente, inicializamos uma lista de argumentos utilizando `va_list`.  
Isso permite acessar todos os parâmetros adicionais que o usuário passou para a função.

```c
va_list args;
va_start(args, format);
````

A partir desse momento, temos acesso a todos os argumentos fornecidos.

---

### 2. Parsing da string de formatação

A string de formatação é então enviada para uma função responsável por analisá-la, chamada aqui de **parse_format**.

Essa função percorre a string **caractere por caractere**, interpretando o que deve ser feito.

Existem dois cenários possíveis:

* **Caractere normal**
  Se o caractere não possui nenhum significado especial, ele é simplesmente impresso e o contador de caracteres é incrementado.

* **Caractere especial `%`**
  Quando encontramos `%`, significa que um **especificador de formatação** está chegando.

---

### 3. Identificação do especificador

Após encontrar `%`, verificamos qual especificador vem logo em seguida.

Por exemplo:

| Especificador | Significado       |
| ------------- | ----------------- |
| `%c`          | caractere         |
| `%s`          | string            |
| `%d` / `%i`   | número inteiro    |
| `%u`          | inteiro sem sinal |
| `%x` / `%X`   | hexadecimal       |
| `%p`          | ponteiro          |
| `%%`          | imprime `%`       |

Cada especificador possui uma **função específica responsável por tratá-lo**.

---

### 4. Chamada da função responsável

Se o especificador for, por exemplo, `%s`, a função responsável por strings é chamada.

Nesse momento utilizamos:

```c
va_arg(args, tipo)
```

Isso nos permite **obter o próximo valor da lista de argumentos**, que foi passado pelo usuário.

Após a leitura, a lista de argumentos **avança automaticamente para o próximo valor**, ficando pronta para a próxima consulta.

---

### 5. Impressão e contagem

A função responsável então:

1. Trata o dado recebido
2. Imprime o valor no output
3. Incrementa o contador de caracteres impressos

Esse contador é essencial para **simular o comportamento real do `printf`**.

---

### 6. Retorno final

Após toda a string de formatação ser analisada e todos os dados serem impressos, o **ft_printf retorna o total de caracteres impressos**.

```c
return total_characters_printed;
```

---

## 🍽️ A dinâmica do "garçom"

A metáfora do **garçom** ajuda a visualizar o funcionamento do ft_printf:

1. O cliente faz o pedido (argumentos da função).
2. O garçom lê o pedido (parse da string).
3. Ele identifica o tipo de pedido (`%s`, `%d`, `%x`, etc).
4. Ele chama o setor correto da cozinha (função específica).
5. O prato é entregue ao cliente (impressão no output).
6. Ao final, o garçom conta quantos pratos foram servidos (total de caracteres).

Assim, o **ft_printf atua como um sistema central que recebe pedidos, interpreta instruções e encaminha cada tarefa para a função responsável**, reproduzindo o comportamento do `printf` original de forma modular.

## How to use

Da mesma forma como no projeto **Libft**, precisamos apenas compilar o projeto usando o comando:

```bash
make
```
Com o projeto compilado, o programa **ft_printf** ficará disponível para ser carregado junto com a compilação de outro programa

```shell
cc ft_printf.c convert_*.c ft_strlen.c handle*.c yourProgram.c parse*.c print*.c -I . -o myPrintf
```

Dessa forma, com esse comando, podes compilar o meu ft_printf inteiro com seu programa, aquele que detém a função **main**, ao qual exemplifiquei aqui com **yourProgram.c**, podes colocar o nome que colocaste em seu programa. 

Assim, poderão chamar o **ft_printf** da mesma forma como fariam com o printf como:

```c
ft_printf("Hello World, %s\n", "Fernando");
```
Printará o "Hello World", seguido de "Fernando" e uma newline.

## Team

O projeto **ft_printf** não é realizado em equipes dentro da 42. Trata-se de um projeto individual, começando a ser um pouco mais complexo que os demais.
