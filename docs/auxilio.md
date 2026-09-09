# Comandos em Golang

## Sumário

- [1. Comandos](#1-comandos)
- [2. Sintax](#2-sintax)

## 1. Comandos

Esta seção tem como objetivo mostrar os principais comandos de terminal em go e seus usos

#### **Mod:**
Esse comando inicializa o módulo, assim controlando as dependências do projeto, identificando automanticamente essas partes.

```cmd
go mod init nome-do-projeto
```

#### **execução**
Os comando abaixo serve para executar o projeto

```cmd
go run main.go
```

O comando acima roda o pacote principal do projeto, comumente escrito como main

---

```cmd
go run .
```

O comando acima é para quando o projeto não possuir main.go, mas como é uma generalização também pode ser usado quando esse arquivo existir.

#### **Dependências:**
Os comandos abaixo são relacionados às bibliotecas e dependências que podem ser adicionados aos projeto

---

```cmd
go get github.com/XXX
```

O comando acima é usado para adicionar uma dependência ao go.mod

---

```cmd
go get -u
```

O comando acima atualiza as dependências usadas.

---

```cmd
go mod tidy
```

O comando acima é extremamente importante, permite adicionar dependências que estão sendo usadas, remove dependências não usadas, organiza o go.mod e atualiza o go.sum

#### **Testes:**
Nessa seção serão abordados os comandos para rodar os testes em go

```cmd
go test ./...
```

O comando acima executa todos os testes do módulo e seus subpacotes

---

```cmd
go test
```

O comando acima executa apenas os testes do pacote atual

---

```cmd
go test -v ./...
```

O comando acima executa todos os testes com detalhes, ou seja, o "-v" é de verbosidade

#### **Compilar:**
Essa seção aborda a compilação do código em go

```cmd
go build
```

O comando acima compila todo o projeto, mas também é possível especificar o arquivo colocando o nome do arquivo na frente

---

```cmd
go build -o app.exe .
```

O comando acima gera um executável com nome específico

#### **Formatação/Verificação:**
Esta seção aborda a formatação e verificação de código por meio de comandos já prontos de go.

```cmd
go fmt ./...
```

O comando acima formata automaticamente o código em go

---

```cmd
go vet ./...
```

O comando acima procura construções suspeitas ou possíveis problemas no código.


## 2. Sintax

#### **Estrutura do arquivo:**

```go
package nome-do-pacote
```

```go
import "biblioteca"

// ou

import ("varias", "bibliotecas")
```

#### **Variáveis:**

```go
var nome string
var idade int
// var + nome da variável + tipo
```

```go
var nome string = "Isaac"
// pode ser atribuido valor com o "="
```

```go
nome := "Isaac"
// também é possível criar sem tipar, assim o tipo é definido pelo valor
// usa-se ":="
```

#### **Constantes:**

```go
const idade = 20

// ou adicionando tipo

const idade int = 20
```

#### **If:**

```go
if idade >= 18 {
    fmt.print("maior de idade")
}
// não é necessário usar parênteses, vale ressaltas que os operadores são os padrões
```

```go
if idade >= 18 {
    fmt.Println("Maior")
} else {
    fmt.Println("Menor")
}
```

#### **For:**

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

// também pode funcionar como while

i := 0

for i < 10 {
    fmt.Println(i)
    i++
}

// também gera loop infinito

for {
    fmt.Println("Executando")
}

// também existe o comando break para quebrar o loop 
// e o comando continue para dar continuidade ao loop
```

#### **Switch case:**

```go
switch dia {
case "segunda":
    fmt.Println("Segunda-feira")
case "terça":
    fmt.Println("Terça-feira")
default:
    fmt.Println("Outro dia")
}
```

```go
switch {
case idade < 12:
    fmt.Println("Criança")
case idade < 18:
    fmt.Println("Adolescente")
default:
    fmt.Println("Adulto")
}
```

#### **Funções:**
 
```go
func soma(a int, b int) int {
    return a + b
}
// func + nome + (parâmetros com tipo) + tipo de retorno
```
 
---
 
```go
func soma(a, b int) int {
    return a + b
}
// quando os parâmetros são do mesmo tipo, o tipo pode ser escrito só no último
```
 
---
 
```go
func avisar(msg string) {
    fmt.Println(msg)
}
// funções sem retorno simplesmente omitem o tipo de retorno
```
 
---
 
```go
func aplicar(valores []int, f func(int) int) []int {
    resultado := []int{}
    for _, v := range valores {
        resultado = append(resultado, f(v))
    }
    return resultado
}
 
dobro := func(x int) int { return x * 2 }
// funções são valores em go: podem ser passadas como parâmetro,
// guardadas em variáveis e retornadas por outras funções
```
 
---
 
```go
func somarTudo(numeros ...int) int {
    total := 0
    for _, n := range numeros {
        total += n
    }
    return total
}
 
somarTudo(1, 2, 3, 4)
// o "..." cria uma função variádica, que aceita N argumentos
// dentro da função, "numeros" é um slice
```
 
#### **Múltiplos retornos:**
Go permite que uma função devolva mais de um valor, e esse é o mecanismo usado em praticamente toda a biblioteca padrão para retornar `valor, erro`.
 
```go
func dividir(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("divisão por zero")
    }
    return a / b, nil
}
 
resultado, err := dividir(10, 2)
// os dois valores precisam ser recebidos, senão o compilador reclama
```
 
---
 
```go
resultado, _ := dividir(10, 2)
// o "_" (blank identifier) descarta um valor que não será usado
```
 
---
 
```go
func dividir(a, b float64) (resultado float64, err error) {
    if b == 0 {
        err = errors.New("divisão por zero")
        return
    }
    resultado = a / b
    return
}
// retornos nomeados: as variáveis já nascem declaradas e zeradas,
// e o "return" sozinho (naked return) devolve os valores atuais delas
// é útil em funções curtas, mas em funções longas prejudica a leitura
```
 
## 3. Estruturas de dados
 
#### **Arrays:**
O array em go tem **tamanho fixo** e o tamanho faz parte do tipo, ou seja, `[3]int` e `[4]int` são tipos diferentes. Além disso, arrays são **tipos de valor**: ao atribuir ou passar para uma função, o array inteiro é copiado.
 
```go
var numeros [3]int
// array com 3 posições, todas iniciadas com o valor zero do tipo (0)
```
 
---
 
```go
numeros := [3]int{1, 2, 3}
 
numeros := [...]int{1, 2, 3}
// o "..." faz o compilador contar o tamanho automaticamente
```
 
---
 
```go
numeros[0] = 10
fmt.Println(numeros[0])
fmt.Println(len(numeros))
// acesso por índice começando em 0 e "len" para o tamanho
```
 
#### **Slices:**
O slice é a estrutura usada no dia a dia. Ele é uma "janela" sobre um array por baixo dos panos e carrega três informações: ponteiro para o array, `len` (quantos elementos tem) e `cap` (quanto cabe antes de precisar realocar).
 
```go
numeros := []int{1, 2, 3}
// sem número entre colchetes = slice
```
 
---
 
```go
numeros := make([]int, 0, 10)
// make(tipo, len, cap) — cria um slice com tamanho 0 e capacidade 10
// informar a capacidade evita realocações quando já se sabe o tamanho aproximado
```
 
---
 
```go
numeros = append(numeros, 4)
numeros = append(numeros, 5, 6)
numeros = append(numeros, outroSlice...)
// append retorna um novo slice, por isso é obrigatório reatribuir
// se a capacidade estourar, go cria um array maior e copia os dados
```
 
---
 
```go
parte := numeros[1:3]
// fatiamento: do índice 1 até o 2 (o final é exclusivo)
// atenção: "parte" compartilha o mesmo array de "numeros",
// alterar um pode alterar o outro
```
 
---
 
```go
copia := make([]int, len(numeros))
copy(copia, numeros)
// copy cria uma cópia real, sem compartilhar memória
```
 
---
 
```go
for i, v := range numeros {
    fmt.Println(i, v)
}
// range devolve índice e valor
// use "_" para ignorar o que não precisar: for _, v := range numeros
```
 
#### **Maps:**
O map é a tabela hash de go: guarda pares **chave → valor** com busca, inserção e remoção em tempo praticamente constante. Pontos importantes da teoria:
 
- A **chave precisa ser comparável** (string, números, bool, structs de campos comparáveis). Slices, maps e funções não podem ser chave.
- Um map é um **tipo de referência**: passar um map para uma função não copia os dados, então alterações dentro da função afetam o original.
- A **ordem de iteração é aleatória** por design. Nunca dependa dela; se precisar de ordem, colete as chaves em um slice e ordene.
- O **valor zero de um map é `nil`**. Ler de um map nil funciona (devolve o valor zero), mas **escrever gera panic**. Por isso sempre inicialize com `make` ou literal.
- Buscar uma chave inexistente **não dá erro**: devolve o valor zero do tipo, o que torna necessário o idioma "comma ok" para diferenciar "não existe" de "existe e vale zero".
```go
idades := make(map[string]int)
// make(map[tipoDaChave]tipoDoValor)
```
 
---
 
```go
idades := map[string]int{
    "Isaac": 20,
    "Ana":   25,
}
// criação com valores iniciais (a vírgula final é obrigatória)
```
 
---
 
```go
idades["Pedro"] = 30
fmt.Println(idades["Isaac"])
delete(idades, "Ana")
fmt.Println(len(idades))
// inserir/atualizar, ler, remover e contar
```
 
---
 
```go
valor, existe := idades["Joao"]
 
if existe {
    fmt.Println(valor)
} else {
    fmt.Println("chave não encontrada")
}
// idioma "comma ok": o segundo retorno é um bool dizendo se a chave existe
// sem ele, "valor" seria 0 e não daria para saber se a idade é 0 ou se não existe
```
 
---
 
```go
for chave, valor := range idades {
    fmt.Println(chave, valor)
}
// lembrando: a ordem muda a cada execução
```
 
---
 
```go
var vazio map[string]int
fmt.Println(vazio["a"]) // 0 — leitura funciona
vazio["a"] = 1          // panic: assignment to entry in nil map
```
 
---
 
```go
usuarios := map[string][]string{}
usuarios["admin"] = append(usuarios["admin"], "isaac")
// maps podem guardar qualquer tipo como valor: slices, structs, outros maps
```
 
## 4. Structs, métodos e ponteiros
 
#### **Structs:**
Go não tem classes. A struct é a forma de agrupar dados relacionados em um tipo próprio.
 
```go
type Pessoa struct {
    Nome  string
    Idade int
}
// campos com letra maiúscula são exportados (públicos fora do pacote),
// com letra minúscula ficam visíveis apenas dentro do pacote
```
 
---
 
```go
p := Pessoa{Nome: "Isaac", Idade: 20}
// criação nomeando os campos (recomendado)
 
p := Pessoa{"Isaac", 20}
// criação posicional — quebra se a ordem dos campos mudar
 
var p Pessoa
// struct zerada: Nome = "" e Idade = 0
```
 
---
 
```go
p.Idade = 21
fmt.Println(p.Nome)
// acesso aos campos com ponto
```
 
---
 
```go
p := &Pessoa{Nome: "Isaac"}
// "&" cria a struct e devolve um ponteiro para ela
// mesmo sendo ponteiro, o acesso continua sendo p.Nome (go faz o deref sozinho)
```
 
---
 
```go
type Endereco struct {
    Cidade string
}
 
type Pessoa struct {
    Nome string
    Endereco // campo embutido (embedding)
}
 
p := Pessoa{Nome: "Isaac", Endereco: Endereco{Cidade: "São Paulo"}}
fmt.Println(p.Cidade) // acesso direto, sem p.Endereco.Cidade
// é composição, não herança: a struct externa "promove" os campos da interna
```
 
#### **Métodos:**
Método é uma função com um **receptor**, o que a associa a um tipo. É o mais próximo que go chega de "método de classe".
 
```go
func (p Pessoa) Apresentar() string {
    return "Olá, eu sou " + p.Nome
}
 
p.Apresentar()
// receptor por valor: recebe uma CÓPIA da struct
// alterações feitas aqui dentro não afetam o original
```
 
---
 
```go
func (p *Pessoa) Aniversario() {
    p.Idade++
}
 
p.Aniversario()
// receptor por ponteiro: trabalha sobre a struct original
// use quando o método precisa MODIFICAR o estado ou quando a struct é grande
```
 
---
 
```go
func (p Pessoa) String() string {
    return fmt.Sprintf("%s (%d)", p.Nome, p.Idade)
}
// implementar o método String() faz o fmt usar essa saída automaticamente
```
 
#### **Ponteiros:**
Um ponteiro guarda o **endereço de memória** de um valor em vez do valor em si. Teoria essencial:
 
- `&variavel` devolve o endereço (referência) da variável.
- `*ponteiro` acessa o valor apontado (dereferência); em `*Tipo`, o `*` significa "ponteiro para Tipo".
- Go passa **tudo por valor**. Passar uma struct grande copia todos os campos; passar um ponteiro copia apenas o endereço.
- Sem ponteiro, uma função **não consegue alterar** a variável de quem a chamou.
- O valor zero de um ponteiro é `nil`; dereferenciar um ponteiro nil causa panic.
- **Não existe aritmética de ponteiros** em go, e o coletor de lixo cuida da memória — não há `free`.
- Slices, maps, channels e funções já se comportam como referência internamente, então normalmente **não** se usa ponteiro para eles.
```go
x := 10
p := &x
 
fmt.Println(p)  // endereço, algo como 0xc000018030
fmt.Println(*p) // 10
 
*p = 20
fmt.Println(x)  // 20 — alterar via ponteiro alterou a variável original
```
 
---
 
```go
func incrementar(n int) {
    n++
}
 
func incrementarPtr(n *int) {
    *n++
}
 
x := 10
incrementar(x)     // x continua 10 (recebeu uma cópia)
incrementarPtr(&x) // x vira 11
```
 
---
 
```go
type Conta struct {
    Saldo float64
}
 
func (c Conta) DepositarErrado(v float64) {
    c.Saldo += v // altera a cópia, o saldo real não muda
}
 
func (c *Conta) Depositar(v float64) {
    c.Saldo += v // altera a conta original
}
 
conta := Conta{}
conta.DepositarErrado(100)
fmt.Println(conta.Saldo) // 0
 
conta.Depositar(100)
fmt.Println(conta.Saldo) // 100
// esse é o motivo mais comum de bug em quem vem de linguagens com classes:
// métodos que mudam estado precisam de receptor por ponteiro
```
 
---
 
```go
p := &Pessoa{Nome: "Isaac"}
fmt.Println(p.Nome)
// go faz a dereferência automática: (*p).Nome e p.Nome são equivalentes
```
 
---
 
```go
var p *Pessoa
fmt.Println(p == nil) // true
fmt.Println(p.Nome)   // panic: nil pointer dereference
// sempre verifique se um ponteiro é nil antes de usar
```
 
**Regra prática:** escolha um estilo por tipo. Se algum método do tipo usa receptor por ponteiro, use ponteiro em **todos** os métodos dele, para manter consistência e evitar problemas ao satisfazer interfaces.
 
## 5. Concorrência e controle de fluxo
 
#### **Defer:**
O `defer` agenda uma chamada para ser executada **quando a função atual terminar**, seja por `return` normal ou por panic. Teoria:
 
- As chamadas adiadas são empilhadas e executadas em ordem **LIFO** (a última adiada roda primeiro).
- Os **argumentos são avaliados na hora do `defer`**, não na hora da execução.
- Roda mesmo se a função der panic, o que o torna ideal para liberar recursos: fechar arquivos, conexões, `mutex.Unlock()`, `wg.Done()`.
- Como só executa no fim **da função**, usar `defer` dentro de um loop longo acumula chamadas e segura recursos até o fim — nesses casos, extraia o corpo do loop para uma função.
- Com retornos nomeados, o `defer` consegue **alterar o valor retornado**.
```go
func main() {
    defer fmt.Println("fim")
    fmt.Println("início")
}
 
// saída:
// início
// fim
```
 
---
 
```go
func main() {
    defer fmt.Println("1")
    defer fmt.Println("2")
    defer fmt.Println("3")
}
 
// saída: 3, 2, 1 (pilha — LIFO)
```
 
---
 
```go
arquivo, err := os.Open("dados.txt")
if err != nil {
    return err
}
defer arquivo.Close()
// uso clássico: abrir o recurso e já garantir o fechamento na linha seguinte
```
 
---
 
```go
x := 10
defer fmt.Println("valor:", x)
x = 20
// imprime "valor: 10" — o argumento foi avaliado no momento do defer
```
 
---
 
```go
defer func() {
    fmt.Println("valor:", x)
}()
// dentro de uma closure, o valor é lido só na execução: imprime 20
```
 
---
 
```go
func processar() (err error) {
    defer func() {
        if r := recover(); r != nil {
            err = fmt.Errorf("recuperado de panic: %v", r)
        }
    }()
 
    panic("algo quebrou")
}
// defer + recover transforma um panic em erro comum
// recover só funciona dentro de uma função adiada
```
 
#### **Goroutines:**
Goroutine é uma função executando de forma concorrente, gerenciada pelo runtime de go. Teoria:
 
- É muito mais barata que uma thread do sistema (começa com alguns KB de stack, que cresce sob demanda), então criar milhares é normal.
- O **scheduler** de go multiplexa várias goroutines sobre poucas threads do SO (modelo M:N).
- Concorrência **não é** paralelismo: concorrência é lidar com várias tarefas ao mesmo tempo; paralelismo é executá-las literalmente ao mesmo tempo, o que depende dos núcleos disponíveis.
- Quando a função `main` termina, o programa encerra e **todas as goroutines morrem**, mesmo inacabadas. Por isso é preciso sincronizar com `WaitGroup` ou channels.
- Nunca use `time.Sleep` como sincronização real — serve só para exemplos.
- Acesso simultâneo à mesma variável causa **race condition**. Use `sync.Mutex` para proteger estado compartilhado, ou prefira o lema de go: *"não se comunique compartilhando memória; compartilhe memória comunicando"* (ou seja, use channels).
- Rode `go run -race .` para detectar corridas de dados.
```go
go minhaFuncao()
// a palavra-chave "go" dispara a função em uma nova goroutine
// a execução segue imediatamente para a próxima linha
```
 
---
 
```go
func main() {
    go fmt.Println("goroutine")
    fmt.Println("main")
}
// provavelmente só "main" é impresso: a main termina antes da goroutine rodar
```
 
---
 
```go
var wg sync.WaitGroup
 
for i := 1; i <= 3; i++ {
    wg.Add(1)
    go func(id int) {
        defer wg.Done()
        fmt.Println("trabalhador", id)
    }(i)
}
 
wg.Wait()
// Add informa quantas goroutines esperar, Done marca uma como concluída
// e Wait bloqueia até o contador chegar a zero
```
 
---
 
```go
var mu sync.Mutex
contador := 0
 
for i := 0; i < 1000; i++ {
    wg.Add(1)
    go func() {
        defer wg.Done()
        mu.Lock()
        contador++
        mu.Unlock()
    }()
}
// sem o mutex, "contador++" (que é ler, somar e escrever)
// se embaralha entre goroutines e o resultado final fica errado
```
 
#### **Channels:**
Channel é o "cano" tipado por onde goroutines trocam valores com segurança. Teoria:
 
- Criado com `make(chan Tipo)`. O envio é `ch <- valor` e o recebimento é `valor := <-ch`.
- **Sem buffer (unbuffered):** o envio bloqueia até alguém receber e o recebimento bloqueia até alguém enviar. Isso sincroniza as duas goroutines no mesmo ponto (rendezvous).
- **Com buffer:** `make(chan int, 3)` permite enviar até encher; só bloqueia quando o buffer está cheio (envio) ou vazio (recebimento).
- Se todas as goroutines ficarem bloqueadas esperando umas às outras, o runtime detecta e aborta com `fatal error: all goroutines are asleep - deadlock!`.
- **Quem fecha é quem envia**, nunca quem recebe. Enviar em channel fechado causa panic; receber devolve o valor zero imediatamente.
- Um channel `nil` bloqueia para sempre em envio e recebimento.
- `select` espera em vários channels ao mesmo tempo; se mais de um estiver pronto, escolhe aleatoriamente.
```go
ch := make(chan string)      // sem buffer
ch := make(chan string, 3)   // com buffer de 3
```
 
---
 
```go
func main() {
    ch := make(chan string)
 
    go func() {
        ch <- "olá"
    }()
 
    msg := <-ch
    fmt.Println(msg)
}
// o recebimento bloqueia a main até a goroutine enviar,
// funcionando também como sincronização
```
 
---
 
```go
valor, aberto := <-ch
 
if !aberto {
    fmt.Println("channel fechado")
}
// o segundo retorno indica se o channel ainda está aberto
```
 
---
 
```go
func produtor(ch chan<- int) {
    for i := 0; i < 5; i++ {
        ch <- i
    }
    close(ch)
}
 
func main() {
    ch := make(chan int)
    go produtor(ch)
 
    for v := range ch {
        fmt.Println(v)
    }
}
// "chan<- int" é um channel só de envio e "<-chan int" só de recebimento;
// isso deixa a intenção explícita e o compilador cobra
// o range sobre o channel encerra sozinho quando ele é fechado
```
 
---
 
```go
select {
case msg := <-ch1:
    fmt.Println("ch1:", msg)
case msg := <-ch2:
    fmt.Println("ch2:", msg)
case <-time.After(2 * time.Second):
    fmt.Println("timeout")
default:
    fmt.Println("nada pronto agora")
}
// select espera o primeiro channel que ficar pronto
// "time.After" implementa timeout e "default" evita bloqueio
```
 
---
 
```go
func main() {
    jobs := make(chan int, 100)
    resultados := make(chan int, 100)
 
    for w := 1; w <= 3; w++ {
        go func(id int) {
            for j := range jobs {
                resultados <- j * 2
            }
        }(w)
    }
 
    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)
 
    for i := 0; i < 5; i++ {
        fmt.Println(<-resultados)
    }
}
// padrão worker pool: várias goroutines consomem do mesmo channel de tarefas
```
 
## 6. Interfaces, erros e conversão
 
#### **Interfaces:**
Interface define um **conjunto de comportamentos** (assinaturas de métodos). Teoria:
 
- A implementação é **implícita**: não existe `implements`. Se o tipo tem os métodos, ele já satisfaz a interface. Isso é chamado de *duck typing* estático — verificado em tempo de compilação.
- Interfaces devem ser **pequenas**. O ditado da comunidade é *"the bigger the interface, the weaker the abstraction"*; boa parte da biblioteca padrão usa interfaces de um único método (`error`, `io.Reader`, `io.Writer`).
- Quem **consome** define a interface, não quem implementa. Declare a interface no pacote que precisa dela.
- Internamente uma interface guarda um par **(tipo, valor)**. Por isso uma interface contendo um ponteiro nil **não é igual a nil** — pegadinha clássica.
- Se um método usa receptor por ponteiro, só `*Tipo` satisfaz a interface, não `Tipo`.
- `interface{}` (ou `any`, a partir do Go 1.18) aceita qualquer valor, mas perde a informação de tipo — use com moderação.
```go
type Animal interface {
    Falar() string
}
 
type Cachorro struct{}
 
func (c Cachorro) Falar() string {
    return "Au au"
}
 
var a Animal = Cachorro{}
fmt.Println(a.Falar())
// Cachorro satisfaz Animal automaticamente por ter o método Falar
```
 
---
 
```go
type Forma interface {
    Area() float64
    Perimetro() float64
}
 
func descrever(f Forma) {
    fmt.Println(f.Area(), f.Perimetro())
}
// qualquer tipo com esses dois métodos pode ser passado — polimorfismo
```
 
---
 
```go
var i interface{} = "texto"
 
s, ok := i.(string)
if ok {
    fmt.Println(s)
}
// type assertion: tenta extrair o tipo concreto de dentro da interface
// sem o "ok", se o tipo não bater, ocorre panic
```
 
---
 
```go
switch v := i.(type) {
case string:
    fmt.Println("string:", v)
case int:
    fmt.Println("int:", v)
default:
    fmt.Println("tipo desconhecido")
}
// type switch: descobre o tipo concreto guardado na interface
```
 
---
 
```go
var _ Animal = (*Cachorro)(nil)
// truque de compilação: garante que *Cachorro implementa Animal,
// gerando erro de build caso algum método falte
```
 
#### **Tratamento de erro:**
Go não tem exceções para fluxo normal. Erro é um **valor comum**, retornado e verificado explicitamente. `error` é apenas uma interface:
 
```go
type error interface {
    Error() string
}
```
 
---
 
```go
resultado, err := dividir(10, 0)
if err != nil {
    fmt.Println("erro:", err)
    return
}
// o padrão idiomático: checar o erro imediatamente após a chamada
```
 
---
 
```go
errors.New("mensagem de erro")
fmt.Errorf("falha ao processar %s", nome)
// duas formas de criar erros simples
```
 
---
 
```go
if err != nil {
    return fmt.Errorf("ao carregar config: %w", err)
}
// o verbo %w "embrulha" (wrap) o erro original, preservando a causa
// e adicionando contexto sobre onde ele ocorreu
```
 
---
 
```go
var ErrNaoEncontrado = errors.New("não encontrado")
 
if errors.Is(err, ErrNaoEncontrado) {
    // compara com um erro sentinela, mesmo que ele esteja embrulhado
}
```
 
---
 
```go
type ErroValidacao struct {
    Campo string
}
 
func (e *ErroValidacao) Error() string {
    return "campo inválido: " + e.Campo
}
 
var validacao *ErroValidacao
if errors.As(err, &validacao) {
    fmt.Println(validacao.Campo)
}
// erro customizado é qualquer tipo com o método Error()
// errors.As extrai o tipo concreto de dentro da cadeia de erros
```
 
---
 
```go
panic("estado impossível")
// panic deve ser reservado para erros irrecuperáveis de programação,
// não para erros esperados como arquivo ausente ou input inválido
```
 
#### **Conversão de tipo:**
Go é fortemente tipado e **não faz conversão implícita**. Somar um `int` com um `float64` sem converter é erro de compilação.
 
```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
// sintaxe: Tipo(valor)
// atenção: converter float para int trunca a parte decimal (não arredonda)
```
 
---
 
```go
s := strconv.Itoa(42)        // int  -> string ("42")
n, err := strconv.Atoi("42") // string -> int
// converter número para string com string(42) NÃO funciona como esperado:
// isso gera o caractere Unicode do código 42, não o texto "42"
```
 
---
 
```go
f, err := strconv.ParseFloat("3.14", 64)
b, err := strconv.ParseBool("true")
i, err := strconv.ParseInt("42", 10, 64)
// ParseInt recebe a base (10) e o tamanho em bits (64)
```
 
---
 
```go
s := "go"
bytes := []byte(s)
runes := []rune(s)
texto := string(bytes)
// string em go é uma sequência imutável de bytes em UTF-8
// []byte trata byte a byte; []rune trata caractere a caractere
// para textos com acentos ou emoji, use []rune para não quebrar o caractere
```
 
---
 
```go
fmt.Sprintf("%d anos", 20)
// Sprintf formata qualquer valor em string
// verbos úteis: %d inteiro, %s string, %f float, %v valor padrão,
// %+v struct com nomes dos campos, %T tipo do valor
```
 
---
 
```go
var i interface{} = 42
 
n := i.(int)     // type assertion (interface -> tipo concreto)
f := float64(n)  // type conversion (tipo -> outro tipo)
// são coisas diferentes: assertion consulta o que está dentro da interface,
// conversion transforma um valor de um tipo em outro
```