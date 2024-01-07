<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CRUD de Produtos</title>
</head>
<body>

  <h1>CRUD de Produtos</h1>

  <form id="productForm">
    <label for="productName">Nome do Produto:</label>
    <input type="text" id="productName" required>

    <label for="productPrice">Preço:</label>
    <input type="number" id="productPrice" required>

    <button type="submit">Adicionar Produto</button>
  </form>

  <ul id="productList"></ul>

  <script>
    // Dados de produtos
    let products = [];

    // Referências aos elementos do DOM
    const productForm = document.getElementById('productForm');
    const productList = document.getElementById('productList');

    // Função para renderizar a lista de produtos
    function renderProducts() {
      productList.innerHTML = '';
      products.forEach(product => {
        const li = document.createElement('li');
        li.textContent = `${product.name} - $${product.price.toFixed(2)}`;
        
        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Excluir';
        deleteButton.addEventListener('click', () => deleteProduct(product.id));

        li.appendChild(deleteButton);
        productList.appendChild(li);
      });
    }

    // Função para adicionar um novo produto
    function addProduct(name, price) {
      const newProduct = {
        id: Date.now(),
        name,
        price
      };
      products.push(newProduct);
      renderProducts();
    }

    // Função para excluir um produto
    function deleteProduct(productId) {
      products = products.filter(product => product.id !== productId);
      renderProducts();
    }

    // Manipulador de envio do formulário
    productForm.addEventListener('submit', function(event) {
      event.preventDefault();

      const productName = document.getElementById('productName').value;
      const productPrice = parseFloat(document.getElementById('productPrice').value);

      if (productName && !isNaN(productPrice)) {
        addProduct(productName, productPrice);
        productForm.reset();
      } else {
        alert('Por favor, preencha todos os campos corretamente.');
      }
    });

    // Inicializar a renderização dos produtos
    renderProducts();
  </script>

</body>
</html>
