
# Blockchain - Projeto MoviUFF

## Desenvolvimento de uma lógica de blockchain

**Proposta:** Criar um código simples em qualquer linguagem de programação. O código deve receber dados criptografados, calcular o hash da mensagem original e, em seguida, inserir um novo conjunto de dados, retornando o hash da mensagem combinado com uma parte do hash anterior.

Essencialmente, o processo consiste em:

1.  Receber dados criptografados
2. Calcular o hash da mensagem original
3. Inserir o próximo conjunto de dados.
4. Retornar o hash da mensagem atual junto com parte do hash anterior.





## Tecnologias utilizadas

**Linguaguem:** Python

**Ambiente de Execução:** Google Colab





## Criptografando os Dados de entrada

Na especificação determina que os dados de entrada deveriam estar criptografados. Dessa forma foi incluido no código uma etapa anterior onde é passado uma frase e no fim tem-se a frase em forma criptografica.

Os seguintes dados criptografados foram utilizados na etapa de criação do hash e cadeia da blockchain

```
dados1
Dados originais: Desenvolvimento de uma lógica de blockchain
Dados criptografados: 2a97e3dc07fe246323f751aac2b503ad4ddb3c9f0ae0eece74d107dc3499a6c876bcf78ae80909d1044f729c
Tag de autenticação: 25dda6d0f5ab8f98ba3c919c0c8eb883

dados2
Dados originais: minha senha do banco é 1234
Dados criptografados: f13e3d47dd25b7723e35efa04ed2291ae5af35b86d666a8aa6423ba0
Tag de autenticação: b10e9549c35b88eafcef873047f5d3fa
```

## Etapa de Geração da Hash e criação da Blockchain

### Importação de Bibliotecas

Foi preciso importar uma biblioteca python ```hashlib```
que fornece funções de hash, como SHA-256, que será usada para calcular o hash da mensagem.([Fonte](https://docs.python.org/3/library/hashlib.html))

>Já os SHA, (Secure Hash Algorithms) são conjuntos de funções criptográficas de hash definidas pela linguagem a serem usadas para vários aplicativos, como segurança de senha, etc. Algumas variantes são suportadas pelo Python na biblioteca “ hashlib.A função que será usada será SHA256 que uma função hash pertence à classe hash SHA-2, o tamanho do bloco interno é de 32 bits.”. ([Fonte](https://acervolima.com/sha-em-python/#google_vignette))

### Definição de Classe e Métodos:

#### Classe Blockchain

```python
class Blockchain:
    def __init__(self):
        self.cadeia = []
        self.hash_anterior = None
```

Foi definida a Classe Blockchain, cujo método init, tem como paremetros:

- **cadeia** que é uma lista que armazenará os hashes dos blocos = self.cadeia
- **variável hash_anterior** que manterá o hash do bloco anterior inicializada com o valor nulo. 

#### Métodos 
- Calcula o _Hash_ e Insere na Classe Blockchain
```python
    def calcular_inserir_hash(self, dados_criptografados):
        if self.hash_anterior is not None:
            dados_criptografados += self.hash_anterior
        print('Dados criptografados: ',dados_criptografados)
        hash_mensagem_original = hashlib.sha256(dados_criptografados.encode()).hexdigest()
        self.cadeia.append(hash_mensagem_original) 
        self.hash_anterior = hash_mensagem_original
 ```

**Denifição do Método:**
Recebe 2 parametros:
1. as informacoes da blockchain (cadeia com os hash dos blocos e o hash do ultimo bloco) 
2. dados criptografados. \\

**Funcionamento:**
1. Verifica a variável do último hash da blockchain ```self.hash_anterior```: Se tiver vazia esse é o primeiro dado da cadeia então ele será criptografado sem concatenar com ninguém.Caso houver um bloco anterior, ele concatena o hash anterior com os novos dados.
2. Os dados criptografados são transformados em sequência de bytes com o método ```encode``` e convertido em hexadecimal utilizando ```hexdigest()```. E só então é calculado o hash dos dados usando SHA-256.
3. Atualiza a cadeia e o hash_anterior da classe Blockchain

- Retorna o Hash Atual

```python
    def retornar_hash_atual_com_parte_do_anterior(self):
        return self.hash_anterior
```

A variável ```self.hash_anterior``` após inclusão dos dados, armazena a concatenção dos hash anterior com os dados criptografados. 

- Impressão da cadeia

```python
    def imprimir_cadeia(self):
        for bloco in self.cadeia:
            print(bloco)
```
Impressão importante afim de mostrar o que foi armazenado na cadeia. 


