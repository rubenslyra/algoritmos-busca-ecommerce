# 1. **Implementação dos Algoritmos de Busca**

#### Busca Linear

```csharp
static int BuscaLinear(int[] arr, int numeroProcurado)
{
    for (var i = 0; i < arr.Length; i++)
    {
        if (arr[i] == numeroProcurado)
        {
            return i;
        }
    }
    return -1;
}
```

#### Busca Binária

```csharp
static int BuscaBinaria(int[] arr, int numeroProcurado)
{
    int indiceInicial = 0;
    int indiceFinal = arr.Length - 1;

    while (indiceInicial <= indiceFinal)
    {
        int indiceMedio = (indiceInicial + indiceFinal) / 2;

        if (arr[indiceMedio] == numeroProcurado)
            return indiceMedio;

        if (numeroProcurado < arr[indiceMedio])
            indiceFinal = indiceMedio - 1;
        else
            indiceInicial = indiceMedio + 1;
    }

    return -1;
}
```

#### Busca por Interpolação

```csharp
static int BuscaInterpolacao(int[] arr, int numeroProcurado)
{
    int indiceInicial = 0;
    int indiceFinal = arr.Length - 1;

    while (indiceInicial <= indiceFinal && numeroProcurado >= arr[indiceInicial] && numeroProcurado <= arr[indiceFinal])
    {
        if (indiceInicial == indiceFinal)
        {
            if (arr[indiceInicial] == numeroProcurado) return indiceInicial;
            return -1;
        }

        int posicao = indiceInicial + ((numeroProcurado - arr[indiceInicial]) * (indiceFinal - indiceInicial)) / (arr[indiceFinal] - arr[indiceInicial]);

        if (arr[posicao] == numeroProcurado)
            return posicao;

        if (arr[posicao] < numeroProcurado)
            indiceInicial = posicao + 1;
        else
            indiceFinal = posicao - 1;
    }

    return -1;
}
```

#### Busca Exponencial

```csharp
static int BuscaExponencial(int[] arr, int numeroProcurado)
{
    if (arr[0] == numeroProcurado)
        return 0;

    int i = 1;
    while (i < arr.Length && arr[i] <= numeroProcurado)
        i = i * 2;

    return BuscaBinaria(arr, numeroProcurado); // Busca Binária após encontrar o intervalo adequado
}
```

### 2. **Implementação do Programa Principal**

Agora, vamos implementar o programa principal que chama os algoritmos de busca e exibe os resultados para os produtos em um formato de console.

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        // Base de dados de produtos (preços ou IDs)
        int[] produtos = { 1, 3, 4, 14, 41, 49, 54, 57, 88, 91, 93, 96 };
        int produtoProcurado = 54;

        // Chamada dos algoritmos de busca
        Console.WriteLine("Executando buscas para o produto ID: " + produtoProcurado);

        // Busca Linear
        int posicaoBuscaLinear = BuscaLinear(produtos, produtoProcurado);
        ExibirResultadoBusca("Busca Linear", posicaoBuscaLinear);

        // Busca Binária
        int posicaoBuscaBinaria = BuscaBinaria(produtos, produtoProcurado);
        ExibirResultadoBusca("Busca Binária", posicaoBuscaBinaria);

        // Busca por Interpolação
        int posicaoBuscaInterpolacao = BuscaInterpolacao(produtos, produtoProcurado);
        ExibirResultadoBusca("Busca por Interpolação", posicaoBuscaInterpolacao);

        // Busca Exponencial
        int posicaoBuscaExponencial = BuscaExponencial(produtos, produtoProcurado);
        ExibirResultadoBusca("Busca Exponencial", posicaoBuscaExponencial);
    }

    static void ExibirResultadoBusca(string metodo, int posicao)
    {
        if (posicao == -1)
            Console.WriteLine($"{metodo}: Produto não encontrado.");
        else
            Console.WriteLine($"{metodo}: Produto localizado na posição {posicao}.");
    }

    // Funções de Busca (já implementadas)
    static int BuscaLinear(int[] arr, int numeroProcurado)
    {
        for (var i = 0; i < arr.Length; i++)
        {
            if (arr[i] == numeroProcurado)
            {
                return i;
            }
        }
        return -1;
    }

    static int BuscaBinaria(int[] arr, int numeroProcurado)
    {
        int indiceInicial = 0;
        int indiceFinal = arr.Length - 1;

        while (indiceInicial <= indiceFinal)
        {
            int indiceMedio = (indiceInicial + indiceFinal) / 2;

            if (arr[indiceMedio] == numeroProcurado)
                return indiceMedio;

            if (numeroProcurado < arr[indiceMedio])
                indiceFinal = indiceMedio - 1;
            else
                indiceInicial = indiceMedio + 1;
        }

        return -1;
    }

    static int BuscaInterpolacao(int[] arr, int numeroProcurado)
    {
        int indiceInicial = 0;
        int indiceFinal = arr.Length - 1;

        while (indiceInicial <= indiceFinal && numeroProcurado >= arr[indiceInicial] && numeroProcurado <= arr[indiceFinal])
        {
            if (indiceInicial == indiceFinal)
            {
                if (arr[indiceInicial] == numeroProcurado) return indiceInicial;
                return -1;
            }

            int posicao = indiceInicial + ((numeroProcurado - arr[indiceInicial]) * (indiceFinal - indiceInicial)) / (arr[indiceFinal] - arr[indiceInicial]);

            if (arr[posicao] == numeroProcurado)
                return posicao;

            if (arr[posicao] < numeroProcurado)
                indiceInicial = posicao + 1;
            else
                indiceFinal = posicao - 1;
        }

        return -1;
    }

    static int BuscaExponencial(int[] arr, int numeroProcurado)
    {
        if (arr[0] == numeroProcurado)
            return 0;

        int i = 1;
        while (i < arr.Length && arr[i] <= numeroProcurado)
            i = i * 2;

        return BuscaBinaria(arr, numeroProcurado); // Busca Binária após encontrar o intervalo adequado
    }
}
```

### 3. **Execução e Saída Esperada**

Ao rodar o programa, você verá algo semelhante a:

```bash
Executando buscas para o produto ID: 54
Busca Linear: Produto localizado na posição 6.
Busca Binária: Produto localizado na posição 6.
Busca por Interpolação: Produto localizado na posição 6.
Busca Exponencial: Produto localizado na posição 6.
```

### 4. **Possíveis Expansões**

Você pode expandir o projeto para incluir:

- **Testes unitários** para cada algoritmo de busca.
- **Entrada dinâmica** onde o usuário insere os produtos e os IDs a serem buscados.
- **Análise de desempenho** para comparar os tempos de execução dos diferentes algoritmos.

Este código fornece uma base sólida para demonstrar a eficiência dos diferentes algoritmos de busca e aplicar isso em um cenário de e-commerce.
