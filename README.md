using System;
using System.Collections.Generic;

class AparelhoEletronico
{
    public string Nome { get; set; }
    public double Preco { get; set; }

    public AparelhoEletronico(string nome, double preco)
    {
        Nome = nome;
        Preco = preco;
    }

    public override string ToString()
    {
        return $"{Nome} - R$ {Preco:F2}";
    }
}

class CarrinhoDeCompras
{
    public List<(AparelhoEletronico, int)> Itens { get; private set; }

    public CarrinhoDeCompras()
    {
        Itens = new List<(AparelhoEletronico, int)>();
    }

    public void AdicionarItem(AparelhoEletronico aparelho, int quantidade)
    {
        Itens.Add((aparelho, quantidade));
    }

    public double CalcularTotal()
    {
        double total = 0;
        foreach (var (aparelho, quantidade) in Itens)
        {
            total += aparelho.Preco * quantidade;
        }
        return total;
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Criar uma lista de aparelhos eletrônicos disponíveis
        List<AparelhoEletronico> aparelhos = new List<AparelhoEletronico>
        {
            new AparelhoEletronico("Smartphone Samsung A54 5g 256gb   ",1790.00),
            new AparelhoEletronico("Tablet S6 lite 4g 64gb            ",1499.99),
            new AparelhoEletronico("Notebook  asus i7                 ",2499.50),
            new AparelhoEletronico("Smart TV Lg 4k Samsung            ",3299.98),
            new AparelhoEletronico("Playstation 5 Digital             ",3199.00),
            new AparelhoEletronico("Caixa de som JBL                  ",129.99),
            new AparelhoEletronico("Fone bluetooth REDMI              ",69.79),
            new AparelhoEletronico("pen drive 32GB SanDisk            ",39.49),
            // Adicione mais aparelhos conforme necessário
        };

        CarrinhoDeCompras carrinho = new CarrinhoDeCompras();

        Console.WriteLine("Bem-vindo à loja STARS eletrônicos!");
        Console.WriteLine("Selecione um item desejado:\n");

        // Mostrar os aparelhos disponíveis
        for (int i = 0; i < aparelhos.Count; i++)
        {
            Console.WriteLine($"{i + 1}. {aparelhos[i]}");
        }

        int escolha;
        do
        {
            // Pedir ao usuário para selecionar um aparelho
            Console.Write("\nDigite o número do item desejado ou 0 para finalizar: ");
            while (!int.TryParse(Console.ReadLine(), out escolha) || escolha < 0 || escolha > aparelhos.Count)
            {
                Console.Write("Escolha inválida. Digite novamente seu BURRO: ");
            }

            if (escolha != 0)
            {
                // Obter o aparelho selecionado
                AparelhoEletronico aparelhoEscolhido = aparelhos[escolha - 1];

                // Pedir a quantidade desejada
                Console.Write($"Digite a quantidade desejada para '{aparelhoEscolhido.Nome}': ");
                int quantidade;
                while (!int.TryParse(Console.ReadLine(), out quantidade) || quantidade <= 0)
                {
                    Console.Write("Quantidade inválida. Digite novamente: ");
                }

                // Adicionar o item ao carrinho de compras
                carrinho.AdicionarItem(aparelhoEscolhido, quantidade);
            }
        } while (escolha != 0);

        // Mostrar resumo da compra
        Console.WriteLine("\nResumo da Compra:");
        foreach (var (aparelho, quantidade) in carrinho.Itens)
        {
            Console.WriteLine($"{aparelho.Nome} - Quantidade: {quantidade} - Preço unitário: R$ {aparelho.Preco:F2}");
        }


        Console.WriteLine($"Total: R$ {carrinho.CalcularTotal():F2}");

        Console.WriteLine("\nA STARS Eletronicos Agradece pela sua preferencia,VOLTE SEMPRE!!");
        Console.WriteLine("\nContate nossos vendedores pelo ZAP:");
        Console.WriteLine("\n*Jaqueline (31) 9123456789");
        Console.WriteLine("\n*Paulo     (31) 9789456123");
        Console.WriteLine("\n*Israel    (31) 9012378945"); 
    }
}
