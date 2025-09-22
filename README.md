## **Código Python: Sistema de Controle de Estoque**

```python
import json
import os

ARQUIVO = "estoque.json"

# Função para carregar produtos do arquivo
def carregar_estoque():
    if not os.path.exists(ARQUIVO):
        return []
    with open(ARQUIVO, "r", encoding="utf-8") as file:
        return json.load(file)

# Função para salvar produtos no arquivo
def salvar_estoque(estoque):
    with open(ARQUIVO, "w", encoding="utf-8") as file:
        json.dump(estoque, file, indent=4, ensure_ascii=False)

# Função para adicionar produto
def adicionar_produto(estoque):
    nome = input("Nome do produto: ")
    quantidade = int(input("Quantidade: "))
    preco = float(input("Preço unitário: "))

    produto = {
        "nome": nome,
        "quantidade": quantidade,
        "preco": preco
    }

    estoque.append(produto)
    salvar_estoque(estoque)
    print("✅ Produto adicionado com sucesso!")

# Função para listar produtos
def listar_estoque(estoque):
    if not estoque:
        print("Nenhum produto no estoque.")
        return
    print("\n=== Estoque Atual ===")
    for i, produto in enumerate(estoque):
        print(f"{i+1}. {produto['nome']} | Quantidade: {produto['quantidade']} | Preço: R$ {produto['preco']:.2f}")
    print("====================\n")

# Função para atualizar quantidade de produto
def atualizar_produto(estoque):
    listar_estoque(estoque)
    if not estoque:
        return
    escolha = int(input("Digite o número do produto que deseja atualizar: "))
    if 1 <= escolha <= len(estoque):
        novo_valor = int(input("Nova quantidade: "))
        estoque[escolha - 1]["quantidade"] = novo_valor
        salvar_estoque(estoque)
        print("✅ Estoque atualizado com sucesso!")
    else:
        print("Opção inválida.")

# Função para remover produto
def remover_produto(estoque):
    listar_estoque(estoque)
    if not estoque:
        return
    escolha = int(input("Digite o número do produto que deseja remover: "))
    if 1 <= escolha <= len(estoque):
        produto_removido = estoque.pop(escolha - 1)
        salvar_estoque(estoque)
        print(f"❌ Produto '{produto_removido['nome']}' removido do estoque.")
    else:
        print("Opção inválida.")

# Função principal
def main():
    estoque = carregar_estoque()

    while True:
        print("=== Sistema de Controle de Estoque ===")
        print("1 - Adicionar produto")
        print("2 - Listar estoque")
        print("3 - Atualizar quantidade")
        print("4 - Remover produto")
        print("5 - Sair")
        escolha = input("Escolha uma opção: ")

        if escolha == "1":
            adicionar_produto(estoque)
        elif escolha == "2":
            listar_estoque(estoque)
        elif escolha == "3":
            atualizar_produto(estoque)
        elif escolha == "4":
            remover_produto(estoque)
        elif escolha == "5":
            print("Saindo do sistema...")
            break
        else:
            print("Opção inválida, tente novamente!")

if __name__ == "__main__":
    main()
```

---

## **Funcionalidades**

* Adicionar produtos ao estoque com **nome, quantidade e preço**
* Listar produtos cadastrados
* Atualizar quantidade de um produto
* Remover produtos do estoque
* Persistência de dados em **arquivo JSON**
* Menu interativo no terminal

---

## **Requisitos**

* Python 3.x

---

## **Como Executar**

1. Salve o arquivo como `controle_estoque.py`
2. Execute no terminal:

```bash
python controle_estoque.py
```

3. Use o menu para gerenciar o estoque.

---

## **Exemplo de Uso**

```text
=== Sistema de Controle de Estoque ===
1 - Adicionar produto
2 - Listar estoque
3 - Atualizar quantidade
4 - Remover produto
5 - Sair
Escolha uma opção: 1

Nome do produto: Caneta
Quantidade: 50
Preço unitário: 1.50
✅ Produto adicionado com sucesso!

=== Sistema de Controle de Estoque ===
Escolha uma opção: 2

=== Estoque Atual ===
1. Caneta | Quantidade: 50 | Preço: R$ 1.50
====================
```

---

## **README.md para GitHub**

````markdown
# 📦 Sistema de Controle de Estoque

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)

## Descrição
Este projeto implementa um **sistema simples de controle de estoque** utilizando Python.  
Os produtos são armazenados em um arquivo **JSON**, garantindo persistência dos dados.

---

## Funcionalidades
- Adicionar produtos com nome, quantidade e preço  
- Listar todos os produtos do estoque  
- Atualizar a quantidade de produtos  
- Remover produtos do estoque  
- Sistema interativo no terminal  

---

## Requisitos
- Python 3.x  

---

## Como Executar
1. Salve o arquivo `controle_estoque.py`  
2. Execute no terminal:

```bash
python controle_estoque.py
````

3. Utilize o menu para gerenciar o estoque.

---

## Melhorias Futuras

* Adicionar categorias de produtos
* Relatórios de estoque baixo
* Interface gráfica (Tkinter ou PyQt)
* Versão web com Flask ou Django

---

## Licença

Uso pessoal.
