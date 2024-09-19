## README do Projeto

# Algoritmos de Busca em Produtos e Preços - Aplicação Console

Este repositório contém a implementação de algoritmos de busca (linear, binária, interpolação e exponencial) aplicados a um cenário de e-commerce, focado em localizar produtos, melhores preços e identificar os mais vendidos em um intervalo de tempo. Este projeto foi desenvolvido em C# como uma aplicação console.

## Índice

- [Requisitos](#requisitos)
- [Ferramentas Necessárias](#ferramentas-necessárias)
- [Instalação](#instalação)
- [Como Rodar o Projeto](#como-rodar-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Contribuição](#contribuição)
- [Licença](#licença)

---

## Requisitos

Para desenvolver e rodar este projeto, você precisará dos seguintes requisitos:

- **.NET SDK 8.0**: Certifique-se de que a versão correta do .NET SDK está instalada.
- **Visual Studio Code** (VSCode): Editor de código recomendado.
- **Extensões do VSCode**:
  - [C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) - Para suporte ao desenvolvimento com C#.
  - [NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=jmrog.vscode-nuget-package-manager) - Para gerenciamento de pacotes NuGet.

---

## Ferramentas Necessárias

1. **Visual Studio Code (VSCode)**  
   - Download: [VSCode](https://code.visualstudio.com/Download)

2. **.NET SDK 8.0**  
   - Download: [.NET SDK 8.0](https://dotnet.microsoft.com/download/dotnet/8.0)

3. **Git**  
   - Ferramenta de controle de versão para clonar o repositório.
   - Download: [Git](https://git-scm.com/downloads)

---

## Instalação

1. **Clonar o Repositório**  
   Clone este repositório no seu ambiente local utilizando o comando abaixo:

   ```bash
   git clone https://github.com/rubenslyra/algoritmos-busca-console.git
   ```

2. **Instalar o .NET SDK 8.0**  
   Certifique-se de que o .NET SDK 8.0 está instalado executando o comando abaixo:

   ```bash
   dotnet --version
   ```

   O retorno esperado é algo como `8.0.x`.

3. **Abrir o Projeto no VSCode**  
   Navegue até o diretório do projeto e abra-o no VSCode:

   ```bash
   code .
   ```

4. **Restaurar Pacotes NuGet**  
   Dentro do terminal do VSCode, execute o comando a seguir para restaurar os pacotes NuGet:

   ```bash
   dotnet restore
   ```

---

## Como Rodar o Projeto

1. **Build do Projeto**  
   Para compilar o projeto, execute o comando:

   ```bash
   dotnet build
   ```

2. **Executar o Projeto**  
   Para rodar o projeto console e executar os algoritmos de busca, utilize:

   ```bash
   dotnet run
   ```

3. **Testes**  
   Caso o projeto tenha testes unitários, você pode rodá-los utilizando o comando:

   ```bash
   dotnet test
   ```

---

## Funcionalidades

- **Busca Linear**: Percorre a lista de produtos um por um até encontrar o item desejado.
- **Busca Binária**: Ideal para listas ordenadas, divide o array ao meio repetidamente até encontrar o item.
- **Busca por Interpolação**: Busca em listas distribuídas uniformemente (como uma lista de preços), oferecendo uma otimização baseada no valor.
- **Busca Exponencial**: Começa verificando um intervalo crescente e, em seguida, realiza uma busca binária nos itens relevantes. Útil para grandes quantidades de dados.

---

## Estrutura do Projeto

```
algoritmos-busca-console/
│
├── /src                # Código-fonte do projeto
│   ├── Program.cs       # Ponto de entrada da aplicação
│   └── Algorithms.cs    # Implementação dos algoritmos de busca
│
├── /tests              # Testes unitários (se aplicável)
│   └── AlgorithmsTests.cs
│
├── /assets             # Arquivos de imagens e outros recursos (se necessário)
├── README.md           # Este arquivo README
└── .gitignore          # Arquivo para ignorar certos arquivos no controle de versão
```

![graphviz](https://github.com/user-attachments/assets/ab58e966-581e-49bb-8c95-a6a848589664)


---

## Contribuição

Para contribuir com o projeto:

1. Faça um fork do repositório.
2. Crie um branch para a sua funcionalidade (`git checkout -b nova-funcionalidade`).
3. Faça commit das suas alterações (`git commit -m 'Adicionar nova funcionalidade'`).
4. Faça push para o branch (`git push origin nova-funcionalidade`).
5. Abra um Pull Request.

---

## Licença

Este projeto é licenciado sob os termos da licença MIT. Para mais detalhes, consulte o arquivo `LICENSE`.

---

**Autor**: Rubens Lyra (@rubenslyra)
