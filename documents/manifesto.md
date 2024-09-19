# Documento de Especificações Técnicas por Engenharia Reversa: Algoritmos de Busca Aplicados a Produtos, Preços e Vendas

### 1. Introdução

Este documento apresenta uma análise técnica detalhada de algoritmos de busca aplicados ao contexto de sistemas de e-commerce, com foco na busca de produtos, melhores preços e produtos mais vendidos em determinado período. A partir da implementação de algoritmos de busca linear e binária, serão adicionados e explicados dois algoritmos adicionais: **busca por interpolação** e **busca exponencial**. Além disso, será discutido como cada algoritmo pode ser aplicado ao cenário de dados comerciais.

### 2. Contexto de Aplicação

No contexto de um sistema de e-commerce, as buscas realizadas podem estar relacionadas a:
- **Localização de um produto** dentro de um catálogo (array de produtos).
- **Busca de melhores preços** em intervalos de tempo, especialmente quando há variações.
- **Identificação dos produtos mais vendidos** em uma faixa de datas específica.

Para esses cenários, a eficiência dos algoritmos de busca é crucial para proporcionar uma experiência otimizada ao usuário final e garantir tempos de resposta rápidos, especialmente em grandes bases de dados.

### 3. Algoritmos de Busca

#### 3.1. Busca Linear

A **busca linear** percorre toda a lista de produtos ou preços sequencialmente. No caso de um catálogo de produtos, este algoritmo pode ser usado quando:
- O catálogo é pequeno ou não ordenado.
- Os dados ainda não foram indexados por critérios como preço ou data de venda.

**Aplicação Típica:**
- Buscar produtos em um pequeno catálogo.
- Identificar o menor preço em uma lista não ordenada de preços históricos.

**Pseudocódigo Adaptado para Preços:**
```csharp
for i in range(0, arr.Length)
    if arr[i].Price <= valorMaximo
        return arr[i]  // Retorna o produto com o menor preço encontrado.
return -1
```

**Complexidade:**
- Pior caso: O(n) - quando o produto ou preço desejado está no final da lista ou não está presente.
- Melhor caso: O(1) - quando o produto é o primeiro da lista.

![graf_produto_01](https://github.com/user-attachments/assets/6267b139-3b92-4536-8f43-34b025431eab)


#### 3.2. Busca Binária

A **busca binária** é aplicável quando a lista de produtos ou preços está ordenada. Em um e-commerce, ela pode ser utilizada para:
- **Localizar produtos** com base em IDs ou preços, assumindo que a lista de produtos esteja previamente ordenada por esses critérios.
- **Identificar variações de preços** em um determinado intervalo de tempo, desde que os preços sejam registrados em ordem cronológica.

**Pseudocódigo Adaptado para Busca de Produto por Preço:**
```csharp
indiceInicial = 0
indiceFinal = arr.Length - 1

while indiceInicial <= indiceFinal
    indiceMedio = (indiceInicial + indiceFinal) / 2
    if arr[indiceMedio].Price == valorProcurado
        return arr[indiceMedio]
    else if valorProcurado < arr[indiceMedio].Price
        indiceFinal = indiceMedio - 1
    else
        indiceInicial = indiceMedio + 1
return -1
```

**Complexidade:**
- O(log n) - em todos os casos devido à divisão sucessiva do array em metades.

![graf_produto_02](https://github.com/user-attachments/assets/744f80ac-c953-474b-8c81-5bdc3cf25fa5)


### 4. Algoritmos Adicionais

#### 4.1. Busca por Interpolação

A **busca por interpolação** assume que os dados estão distribuídos uniformemente e é ideal quando se trabalha com dados de preços ou produtos ordenados de forma regular. Esse algoritmo ajusta dinamicamente o ponto de busca com base na diferença entre o valor procurado e os valores presentes, tornando-o mais eficiente que a busca binária para dados que seguem um padrão linear.

**Aplicação Típica:**
- **Localizar o menor preço** entre produtos dentro de uma faixa de preços. Útil quando os preços são distribuídos uniformemente em grandes listas de produtos.

**Pseudocódigo Adaptado para Preços:**
```csharp
indiceInicial = 0
indiceFinal = arr.Length - 1

while (indiceInicial <= indiceFinal) && (valorProcurado >= arr[indiceInicial].Price) && (valorProcurado <= arr[indiceFinal].Price)
    pos = indiceInicial + ((valorProcurado - arr[indiceInicial].Price) * (indiceFinal - indiceInicial)) / (arr[indiceFinal].Price - arr[indiceInicial].Price)

    if arr[pos].Price == valorProcurado
        return arr[pos]
    if arr[pos].Price < valorProcurado
        indiceInicial = pos + 1
    else
        indiceFinal = pos - 1
return -1
```

**Complexidade:**
- Melhor caso: O(log log n) quando os preços estão distribuídos uniformemente.
- Pior caso: O(n) quando a distribuição não é uniforme.

![graf_produto_03](https://github.com/user-attachments/assets/98700c68-7cf0-45f2-bbe4-cd24814e279b)


#### 4.2. Busca Exponencial

A **busca exponencial** é particularmente útil em grandes sistemas de e-commerce, onde o volume de dados é enorme. Este algoritmo identifica rapidamente a faixa de valores relevantes para então aplicar uma busca binária dentro dessa faixa.

**Aplicação Típica:**
- **Buscar os produtos mais vendidos** em um período específico. A busca exponencial permite localizar a faixa de tempo apropriada em uma lista de vendas ordenadas cronologicamente e, em seguida, aplicar uma busca binária para localizar os produtos mais vendidos.

**Pseudocódigo Adaptado para Produtos Mais Vendidos:**
```csharp
if arr[0].Vendas == valorProcurado
    return arr[0]

i = 1
while i < arr.Length && arr[i].Vendas <= valorProcurado
    i = i * 2

return BuscaBinaria(arr, valorProcurado, i/2, min(i, arr.Length-1))
```

**Complexidade:**
- O(log n) para a busca binária após localizar a faixa com crescimento exponencial.
- Pior caso: O(log n).

![graf_produto_04](https://github.com/user-attachments/assets/a4336af2-244d-4a08-af56-af42ba6f53df)


### 5. Aplicação ao Contexto Comercial

Cada um dos algoritmos discutidos tem sua relevância específica no contexto de um sistema de e-commerce, conforme descrito abaixo:

| **Algoritmo**           | **Cenário de Aplicação**                                       | **Vantagens**                                                                 | **Desvantagens**                                                   |
|-------------------------|---------------------------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Busca Linear**         | Pequenos catálogos de produtos ou quando os dados não são ordenados | Simples de implementar, ideal para pequenos conjuntos de dados                | Ineficiente em grandes volumes de dados                      |
| **Busca Binária**        | Catálogos grandes ordenados por preço, ID ou data de venda     | Extremamente eficiente em dados ordenados                                     | Requer dados previamente ordenados                                |
| **Busca por Interpolação** | Busca de produtos com preços em uma distribuição quase uniforme | Melhor desempenho que a busca binária para distribuições lineares de dados    | Pode ser ineficaz com dados desigualmente distribuídos         |
| **Busca Exponencial**    | Busca de produtos mais vendidos em grandes intervalos de tempo | Ideal para grandes volumes de dados; encontra a faixa adequada rapidamente    | Mais complexo que a busca binária e linear                        |

### 6. Conclusão

Este documento detalhou a implementação e análise de algoritmos de busca aplicados a sistemas de e-commerce, com foco na busca de produtos, melhores preços e vendas dentro de determinados períodos. A busca linear e binária foram explicadas junto com dois algoritmos adicionais (busca por interpolação e busca exponencial) que proporcionam diferentes níveis de eficiência, dependendo da natureza e volume dos dados.

Ao adaptar os algoritmos a contextos comerciais específicos, foi possível

 identificar cenários práticos onde cada técnica se destaca, garantindo que sistemas de busca possam ser otimizados tanto em precisão quanto em performance.
