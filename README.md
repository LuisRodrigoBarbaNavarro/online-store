# Práctica 4 I Tienda en Línea con Carrito de Compras 🐈

### Información Básica

**Nombre:** Barba Navarro Luis Rodrigo

**Fecha (Creación):** 12/10/23

**Descripción:** Este repositorio contiene el código fuente de una tienda en línea interactiva y personalizable, construida con Bootstrap y Javascript. La tienda permite a los usuarios agregar productos de manera dinámica a su carrito de compras y generar un ticket de compra detallado al finalizar la compra.

### Explicación (script-index) 🐈

Este archivo de código es parte del funcionamiento principal de la tienda en línea que permite a los usuarios agregar productos al carrito de compras y mostrar información relevante, incluyendo subtotales. A continuación se pretende mostrar el código completo y el explicación de cada uno de los métodos utilizados:

```javascript
/* Rodrigo Barba - Shinia */
// Arreglo de productos en el cart
const cart = [];

document.addEventListener("DOMContentLoaded", function () {
  // Productos en el catálogo.
  const productList = [
    {
      id: 1,
      image: "https://th.bing.com/th/id/R.3e86b77bdff2526ffdb6170146d728bf?rik=5SHrQ97a2L3Hzw&pid=ImgRaw&r=0",
      name: "Rosa Dorada (Gold Rose)",
      description: "La Rosa Dorada es una flor exquisita con pétalos dorados y un delicado aroma a vainilla. Es una elección perfecta para ocasiones especiales. Siempre te permite obtener ganancias",
      price: 19.99,
    },
    {
      id: 2,
      image: "https://th.bing.com/th/id/R.22fba4aff6f35c75b3f683792896cac1?rik=ASuMXgP4AFuvfw&riu=http%3a%2f%2f2.bp.blogspot.com%2f_enAvQ-J1tLQ%2fR1JMYMRVH7I%2fAAAAAAAAAFs%2fuOiaGAHDStE%2fs1600-R%2fOrchid%2b5.JPG&ehk=Sa2M8mF4wZaT7W9Y2Imm%2bCLPJYGL93IC%2bSxCor6niqk%3d&risl=&pid=ImgRaw&r=0",
      name: "Orquídea Celestial (Heavenly Orchid)",
      description: "La Orquídea Celestial es una flor rara y elegante con pétalos de color lavanda y un aroma suave y agradable. Es símbolo de belleza y elegancia.",
      price: 29.99,
    },
    {
      id: 3,
      image: "https://th.bing.com/th/id/OIP.5eRfiVuzyoj4VownPMV-nAHaEo?pid=ImgDet&rs=1",
      name: "Lirio de Plata (Silver Lily)",
      description: "El Lirio de Plata es una flor única con pétalos plateados y un aroma fresco y limpio. Representa la pureza y la claridad. Grandes y espectaculares para la ocasión",
      price: 24.99,
    },
    {
      id: 4,
      image: "https://th.bing.com/th/id/R.b42f616caf98f787d5ab6636671030b8?rik=gIt6ZBiOAlqq8g&riu=http%3a%2f%2f4.bp.blogspot.com%2f-_JVM0D_1cPY%2fULo-qXily7I%2fAAAAAAAAOTE%2fMYg26LsL5Ys%2fs1600%2fPurple%2bTulips%2bFlowers%2bWallpapers%2b11.jpg&ehk=WsTRIhAcap9FOGHz8WsM1X1VG8zR4BdDMdcy0ysSd7k%3d&risl=&pid=ImgRaw&r=0",
      name: "Tulipán de Medianoche (Midnight Tulip)",
      description: "El Tulipán de Medianoche es un tulipán de color negro profundo y misterioso. Es una opción sorprendente y elegante.",
      price: 14.99,
    },
    {
      id: 5,
      image: "https://th.bing.com/th/id/OIP.ULKem-anJ2oDv0DcvAUVdwHaFO?pid=ImgDet&rs=1",
      name: "Girasol Brillante (Bright Sunflower)",
      description: "El Girasol Brillante es una flor que irradia alegría con sus pétalos amarillos vibrantes y su centro marrón cálido. Es perfecto para transmitir felicidad.",
      price: 59.99,
    },
    {
      id: 6,
      image: "https://th.bing.com/th/id/OIP.wVCXksh8Wc6UVYi9pUSzNwHaE2?pid=ImgDet&rs=1",
      name: "Margarita de Luna (Moon Daisy)",
      description: "La Margarita de Luna es una flor blanca con un delicado brillo plateado en sus pétalos. Evoca la magia de una noche estrellada. Simplemente especiales para la ocasión",
      price: 12.99,
    },
  ];

  // Obtiene el contenedor donde se mostrará el catálogo y el resumen de compra.
  const productListContainer = document.getElementById("productList");
  const checkoutCartContainer = document.getElementById("checkoutCart");
  const totalCheckout = document.getElementById("totalCheckout");

  // Genera las tarjetas de productos en el catálogo y las agrega al contenedor.
  productList.forEach((product) => {
    const card = document.createElement("div");
    card.classList.add("col-md-4", "mb-4");
    card.innerHTML = `
            <div class="card card-custom neo-md rounded-md">
                <img src="${product.image}" class="card-img-top card-img-custom" alt="Producto ${product.id}">
                <div class="card-body">
                    <h5 class="card-title">Producto ${product.id}</h5>
                    <h5 class="card-title">${product.name}</h5>
                    <p class="card-text">Descripción: ${product.description}</p>
                    <p class="card-text">Precio: $${product.price}</p>
                    <div class="input-group">
                        <span class="input-group-btn">
                            <button type="button" class="btn btn-danger btn-number" data-type="minus" data-field="inputQuantity${product.id}">-</button>
                        </span>
                        <input type="text" id="inputQuantity${product.id}" class="form-control input-number" value="1" min="1" max="10">
                        <span class="input-group-btn">
                            <button type="button" class="btn btn-success btn-number" data-type="plus" data-field="inputQuantity${product.id}">+</button>
                        </span>
                    </div>
                    <button class="btn btn-primary add-to-cart" data-product-id="${product.id}" style="margin-top: 20px">Agregar al cart</button>
                </div>
            </div>
        `;
    productListContainer.appendChild(card);

    // Obtiene la cantidad de productos a agregar al cart y manda llamar la función para agregar el producto al cart.
    const btnAdd = card.querySelector(".add-to-cart");
    btnAdd.addEventListener("click", function () {
      const quantity = parseInt(
        document.getElementById(`inputQuantity${product.id}`).value
      );

      if (quantity > 0) {
        addProduct(product, quantity);
      }
    });
  });

  // Almacena en el arreglo los productos agregados al cart y actualiza la cantidad de productos en el carrito en caso de que se agregue más de uno del mismo producto.
  function addProduct(product, quantity) {
    const cartProduct = cart.find((item) => item.product.id === product.id);

    if (cartProduct) {
      cartProduct.quantity += quantity;
    } else {
      cart.push({ product, quantity });
    }

    updateCheckoutCart();
  }

  // Eventos para incrementar y decrementar la cantidad de productos en el cart.
  const btnNumberButtons = document.querySelectorAll(".btn-number");
  btnNumberButtons.forEach(function (button) {
    button.addEventListener("click", function (e) {
      e.preventDefault();

      const fieldName = this.getAttribute("data-field");
      const type = this.getAttribute("data-type");
      const input = document.getElementById(fieldName);
      const currentVal = parseInt(input.value);

      if (!isNaN(currentVal)) {
        if (type === "minus") {
          if (currentVal > input.min) {
            input.value = currentVal - 1;
          }
        } else if (type === "plus") {
          if (currentVal < input.max) {
            input.value = currentVal + 1;
          }
        }
      }
    });
  });

  // Elimina un producto del carrito cuando se presiona el botón de eliminar.
  const checkoutCart = document.getElementById("checkoutCart");
  checkoutCart.addEventListener("click", function (e) {
    if (e.target.classList.contains("btnDelete")) {
      const id = e.target.parentElement.parentElement.firstElementChild
        .textContent;
      const index = cart.findIndex((item) => item.product.id === id);

      cart.splice(index, 1);
      updateCheckoutCart();
    }
  });

  // Actualiza el resumen de compra en el carrito cuando se agrega un producto o se cambia la cantidad de productos.
  function updateCheckoutCart() {
    checkoutCart.innerHTML = "";
    let subtotal = 0;

    cart.forEach((item) => {
      const row = document.createElement("tr");
      row.innerHTML = `
                <td>Producto ${item.product.id}</td>
                <td>${item.product.name}</td>
                <td>${item.quantity}</td>
                <td>$${item.product.price}</td>
                <td>$${item.product.price * item.quantity}</td>
                <td><button type="button" class="btn btn-danger btnDelete">Eliminar</button></td>
            `;
      checkoutCart.appendChild(row);

      subtotal += item.product.price * item.quantity;
    });

    totalCheckout.textContent = `$${subtotal.toFixed(2)}`;
  }
});

// Botón para comprar productos y mandarlos al recibo.
const btnBuy = document.querySelector(".btn-comprar");
btnBuy.addEventListener("click", function () {
  if (cart.length > 0) {
    localStorage.removeItem("data-cart");

    const cartProducts = JSON.stringify(cart);
    localStorage.setItem("data-cart", cartProducts);

    window.location.href = "receipt.html";
  } else {
    alert("El cart está vacío.");
  }
});
```
