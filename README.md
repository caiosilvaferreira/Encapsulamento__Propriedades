# Encapsulamento, Propriedades e autopropriedades

Meu primeiro encapsulamento

```csharp
using System.Globalization;
namespace Course {
    class Produto1 {
        static void Main(string[] args) {
            Produto p = new Produto("TV", 500.0, 10);

            p.SetNome("T");

            p.GetPreco = 100.0; // como ele esta encapsulado, não é permitido alteração de valor

            Console.WriteLine(p.GetNome());
            Console.WriteLine(p.GetPreco());
        }
        }
    }
```

Classe

```csharp
using System.Globalization;
namespace Course {
    class Produto {
        private string _nome;   // o underline é colocado em todos os atributos que são privates
        private double _preco;  // as letras tambem fica em minusculo
        private int _quantidade;
        public Produto() {
        }
        public Produto(string nome, double preco, int quantidade) {
            _nome = nome;
            _preco = preco;
            _quantidade = quantidade;
        }

        public string GetNome() { // metodo get obtem valor, e set pode alterar o valor
            return _nome;
        }
        public void SetNome(string nome) {
            if (nome != null && nome.Length > 1)  { //so vai atribuir esse novo nome se nao for nulo e tiver mais um caractere
                _nome = nome;
            }
        }
        public double GetPreco() {
            return _preco;
        }
        public int GetQuantidade() {
            return _quantidade;
        }
        public double ValorTotalEmEstoque() {
            return _preco * _quantidade;
        }
        public void AdicionarProdutos(int quantidade) {
            _quantidade += quantidade;
        }
        public void RemoverProdutos(int quantidade) {
            _quantidade -= quantidade;
        }
        public override string ToString() {
            return _nome
            + ", $ "
            + _preco.ToString("F2", CultureInfo.InvariantCulture)
            + ", "
            + _quantidade
            + " unidades, Total: $ "
            + ValorTotalEmEstoque().ToString("F2", CultureInfo.InvariantCulture);
        }
    }
}
```

![Untitled](Encapsulamento,%20Propriedades%20e%20autopropriedades%20a4b3c513b3894b969a9bc28b34a0352c/Untitled.png)

exemplos de implementação de propriedade no codigo

```csharp
using System.Globalization;
namespace Course {
    class Produto1 {
        static void Main(string[] args) {
            Produto p = new Produto("TV", 500.0, 10);

            p.Nome = "T";

            Console.WriteLine(p.Nome); // agora ele aceita imprimir o nome do metodo normal sem o get e set igual no exemplo abaixo por conta da implementação da propriedade
            Console.WriteLine(p.Preco);
        }
        }
    }
```

Classe:

```csharp
using System.Globalization;
namespace Course {
    class Produto {
        private string _nome;   // o underline é colocado em todos os atributos que são privates
        private double _preco;  // as letras tambem fica em minusculo
        private int _quantidade;
        public Produto() {
        }
        public Produto(string nome, double preco, int quantidade) {
            _nome = nome;
            _preco = preco;
            _quantidade = quantidade;
        }
        public string Nome {    // isto é uma propriedade 
            get { return _nome; }
            set {
                if (value  != null && value.Length > 1) { //so vai atribuir esse novo nome se nao for nulo e tiver mais um caractere
                    _nome = value; // o value seria o atributo _nome
                }
            }
        }

        
        public double Preco {
            get { return _preco; }   // isso é uma propriedade
        }
        public double Quantidade {
            get { return _quantidade; } // isso é uma propriedade
        }

        public int GetQuantidade() {
            return _quantidade;
        }
        public double ValorTotalEmEstoque() {
            return _preco * _quantidade;
        }
        public void AdicionarProdutos(int quantidade) {
            _quantidade += quantidade;
        }
        public void RemoverProdutos(int quantidade) {
            _quantidade -= quantidade;
        }
        public override string ToString() {
            return _nome
            + ", $ "
            + _preco.ToString("F2", CultureInfo.InvariantCulture)
            + ", "
            + _quantidade
            + " unidades, Total: $ "
            + ValorTotalEmEstoque().ToString("F2", CultureInfo.InvariantCulture);
        }
    }
}
```

# Propriedades

as propriedades ajuda o codigo ficar menor e ter mais controle sobre os dados de saida e entrada

ex:

```csharp
using System.Globalization;
namespace Course {
    class Produto1 {
        static void Main(string[] args) {
            Produto p = new Produto("TV", 500.0, 10);

            p.Nome = "T";

            Console.WriteLine(p.Nome); // agora ele aceita imprimir o nome do metodo normal sem o get e set igual no exemplo abaixo por conta da implementação da propriedade
            Console.WriteLine(p.Preco);
        }
        }
    }
```

usando auto propriedades o codigo antigo esta na parte de cima.

```csharp
using System.Globalization;
namespace Course {
    class Produto {
        private string _nome;   // como ele tem uma logica especifica não tem como colocar get e set
        public double Preco { get; private set; }
        public int Quantidade { get; private set; }
        
        public Produto(string nome, double preco, int quantidade) {
            _nome = nome;
            Preco = preco;
            Quantidade = quantidade;
        }
        public string Nome {    // isto é uma propriedade 
            get { return _nome; }
            set {
                if (value  != null && value.Length > 1) { //so vai atribuir esse novo nome se nao for nulo e tiver mais um caractere
                    _nome = value; // o value seria o atributo _nome
                }
            }
        }
        public double ValorTotalEmEstoque() {
            return Preco * Quantidade;
        }
        public void AdicionarProdutos(int quantidade) {
            Quantidade += quantidade;
        }
        public void RemoverProdutos(int quantidade) {
            Quantidade -= quantidade;
        }
        public override string ToString() {
            return _nome
            + ", $ "
            + Preco.ToString("F2", CultureInfo.InvariantCulture)
            + ", "
            + Quantidade
            + " unidades, Total: $ "
            + ValorTotalEmEstoque().ToString("F2", CultureInfo.InvariantCulture);
        }
    }
}
```

![Untitled](Encapsulamento,%20Propriedades%20e%20autopropriedades%20a4b3c513b3894b969a9bc28b34a0352c/Untitled%201.png)

exercicio que aprendir com encapsulamento:

```csharp
using System.Globalization;
namespace Course {
    class Produto1 {
        static void Main(string[] args) {

            ContaBancaria conta;

            Console.Write("Entre com numero da conta: ");
            int id = int.Parse(Console.ReadLine());
            Console.Write("Informe o titular da conta: ");
            string nome = Console.ReadLine();
            Console.Write("Haverá depósito inicial (s/n)? ");
            string decisao =Console.ReadLine().ToLower();
            if (decisao=="s") {
                Console.Write("Entre com valor de depósito inicial: ");
                decimal depositoInicial = decimal.Parse(Console.ReadLine());
                conta = new ContaBancaria(id, nome, depositoInicial);
                Console.WriteLine(conta);
                Console.WriteLine();
            } else {

                conta = new ContaBancaria( nome, id);
                Console.WriteLine();
            }

            Console.Write("Entre com valor para depósito: ");
            decimal deposito = decimal.Parse(Console.ReadLine());
            conta.Deposito(deposito);
            Console.WriteLine("Dados da conta atualizado: ");
            Console.WriteLine(conta);
            Console.WriteLine();

            Console.Write("Entre com valor para saque: ");
            decimal saque = decimal.Parse(Console.ReadLine());
            conta.Saque(saque);
            Console.WriteLine("Dados da conta atualizado: ");
            Console.WriteLine(conta);
            Console.WriteLine();

        }
    }
}
```

Classe:

```csharp
using System.Globalization;
using System.Reflection.Metadata;
using System.Runtime.CompilerServices;

namespace Course {
    class ContaBancaria {

        public string Nome { get; set; }
        public decimal Saldo { get; private set; }
        public int Id { get; private set; }

        public ContaBancaria( int conta, string nome, decimal saldo) : this(nome, conta) {
            Saldo = saldo;
        }

        public ContaBancaria(string nome, int id) {
            Nome = nome;
            Id = id;
        }

        public void Saque(decimal saque) {

            Saldo -= saque+5.0m;
        }

        public void Deposito(decimal deposito) {
            Saldo += deposito;
        }

        public override string ToString() {
            return "Conta: "
                        +Id
                        +", Titular: "
                        +Nome
                        +", Saldo: $ "
                        +Saldo.ToString("F2", CultureInfo.InvariantCulture);
        }
    }
}
```
