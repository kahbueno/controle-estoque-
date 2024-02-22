# controle-estoque-
Software que gerencia um estoque de produtos, 


using System;
using System.Collections.Generic;

class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public int Quantidade { get; set; }
    public decimal Valor { get; set; }
}

class Program
{
    private static List<Produto> produtos = new List<Produto>();
    private static int currentId = 1;

    static void Main()
    {
        ExibirMenu();
    }

    static void ExibirMenu()
    {
        while (true)
        {
            Console.Clear();
            Console.WriteLine("Controle de estoque - Produtos Eletrônicos");
            Console.WriteLine("[1] Novo");
            Console.WriteLine("[2] Listar Produtos");
            Console.WriteLine("[3] Remover Produtos");
            Console.WriteLine("[4] Entrada Estoque");
            Console.WriteLine("[5] Saída Estoque");
            Console.WriteLine("[0] Sair");
            Console.WriteLine("Selecione uma opção:");

            string opcao = Console.ReadLine()?? "false";

            switch (opcao)
            {
                case "1":
                    AdicionarProduto();
                    break;
                case "2":
                    ListarProdutos();
                    break;
                case "3":
                    RemoverProduto();
                    break;
                case "4":
                    EntradaEstoque();
                    break;
                case "5":
                    SaidaEstoque();
                    break;
                case "0":
                    Console.WriteLine("Obrigada por usar nosso sistema.");
                    return;
                default:
                    Console.WriteLine("Opção inválida.");
                    break;
            }
        }
    }

    static void AdicionarProduto()
    {
        Console.Clear();
        Console.WriteLine("Nome do produto:");
        string nome = Console.ReadLine()?? "false";

        Console.WriteLine("Valor do produto:");
        if (!decimal.TryParse(Console.ReadLine(), out decimal valor))
        {
            Console.WriteLine("Valor inválido.");
            Console.ReadLine();
            return;
        }

        Produto p = new Produto
        {
            Id = currentId++,
            Nome = nome,
            Valor = valor,
            Quantidade = 0
        };

        produtos.Add(p);
        Console.WriteLine("Produto adicionado com sucesso!");
        Console.ReadLine();
    }

    static void ListarProdutos()
    {
        Console.Clear();
        foreach (var produto in produtos)
        {
            Console.WriteLine($"ID: {produto.Id} - Nome: {produto.Nome} - Valor: {produto.Valor:C2} - Quantidade: {produto.Quantidade}");
        }
        Console.ReadLine();
    }

    static void RemoverProduto()
    {
        Console.Clear();
        Console.WriteLine("Digite o ID do produto que deseja remover:");
        if (int.TryParse(Console.ReadLine(), out int id))
        {
            var produto = produtos.Find(p => p.Id == id);
            if (produto != null)
            {
                produtos.Remove(produto);
                Console.WriteLine("Produto removido com sucesso!");
            }
            else
            {
                Console.WriteLine("Produto não encontrado.");
            }
        }
        else
        {
            Console.WriteLine("ID inválido.");
        }
        Console.ReadLine();
    }

    static void EntradaEstoque()
    {
        Console.Clear();
        Console.WriteLine("Digite o ID do produto que deseja adicionar ao estoque:");
        if (int.TryParse(Console.ReadLine(), out int id))
        {
            var produto = produtos.Find(p => p.Id == id);
            if (produto != null)
            {
                Console.WriteLine("Quantidade a ser adicionada:");
                if (int.TryParse(Console.ReadLine(), out int quantidade))
                {
                    produto.Quantidade += quantidade;
                    Console.WriteLine("Quantidade adicionada com sucesso!");
                }
                else
                {
                    Console.WriteLine("Quantidade inválida.");
                }
            }
            else
            {
                Console.WriteLine("Produto não encontrado.");
            }
        }
        else
        {
            Console.WriteLine("ID inválido.");
        }
        Console.ReadLine();
    }

    static void SaidaEstoque()
    {
        Console.Clear();
        Console.WriteLine("Digite o ID do produto que deseja retirar do estoque:");
        if (int.TryParse(Console.ReadLine(), out int id))
        {
            var produto = produtos.Find(p => p.Id == id);
            if (produto != null)
            {
                Console.WriteLine("Quantidade a ser retirada:");
                if (int.TryParse(Console.ReadLine(), out int quantidade) && quantidade <= produto.Quantidade)
                {
                    produto.Quantidade -= quantidade;
                    Console.WriteLine("Quantidade retirada com sucesso!");
                }
                else
                {
                    Console.WriteLine("Quantidade inválida ou superior ao estoque atual.");
                }
            }
            else
            {
                Console.WriteLine("Produto não encontrado.");
            }
        }
        else
        {
            Console.WriteLine("ID inválido.");
        }
        Console.ReadLine();
    }
}
