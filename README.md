# Práctica 4 I Tienda en Línea con Carrito de Compras 🐈

### Información Básica

**Nombre:** Barba Navarro Luis Rodrigo

**Fecha (Creación):** 12/10/23

**Descripción:** Este repositorio contiene el código fuente de una tienda en línea interactiva y personalizable, construida con Bootstrap y Javascript. La tienda permite a los usuarios agregar productos de manera dinámica a su carrito de compras y generar un ticket de compra detallado al finalizar la compra.

---

### Recursos

![Recurso 1](https://i.imgur.com/BTarBUn.png)
![Recurso 2](https://i.imgur.com/2jDiom0.png)

---

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

En esta primera parte del código, se inicia un arreglo llamado cart que se utiliza para almacenar los productos seleccionados por los usuarios, posteriormente, se define un arreglo llamado productList, que contiene información sobre los productos disponibles en la tienda, como su nombre, descripción, imagen y precio.
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
```
Después, se obtienen referencias a elementos HTML en la página, como el contenedor de la lista de productos (productListContainer), el contenedor del carrito de compras (checkoutCartContainer) y el elemento para mostrar el total de la compra (totalCheckout). Posteriormente, se itera por cada producto dentro del arreglo de objetos y se crea una tarjeta para cada producto en el catálogo y se agrega al contenedor de la lista de productos. Cada tarjeta muestra información sobre el producto, incluyendo una imagen, nombre, descripción, precio y un campo para seleccionar la cantidad.
```javascript
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
```

Posteriormente, mediante esta función se escucha el evento de clic en el botón "Agregar al carrito" en cada tarjeta de producto. Cuando se hace clic en este botón, se obtiene la cantidad de productos a agregar y en caso de que la cantidad sea mayor a uno, se llama a la función addProduct para agregar el producto al carrito.
```javascript
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
```

En el siguiente código, se configuran eventos para los botones de "+" y "-" que permiten al usuario aumentar o disminuir la cantidad de productos en el carrito. Dependiendo del botón que hayamos presionado ya sea positivo o negativo, se va ir modificando los datos del campo del texto donde se muestra la cantidad total.
```javascript
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
```

En este segmento de código, se detecta el evento de clic en el botón "Eliminar" dentro del carrito de compras. Cuando el botón es presionado, se procede a eliminar el producto correspondiente del carrito. Para lograr esto, se recupera el identificador único del producto y se utiliza dicho identificador para determinar el índice correspondiente en el arreglo del carrito de compra. Luego, se retira el producto de dicho carrito y, finalmente, se lleva a cabo una actualización de la lista de productos en el carrito de compra para reflejar los cambios.
```javascript
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
```

Esta función actualiza el carrito de compras mostrando los productos, cantidades, precios individuales, subtotales y el total de la compra. También se encarga de mantener la información del carrito actualizada cuando se agregan o eliminan productos. Es iterado el arreglo del carrito de compras para obtener las características de cada producto y ser desplegadas en la tabla de carrito de compra.
```javascript
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
```

Mediante esta sección de código, se escucha el evento de clic en el botón "Comprar". Si hay productos en el carrito, se almacena la información del carrito en el almacenamiento local (localStorage); obteniendo la información del arreglo de carrito, y si el arreglo no se encuentra vacío se redirige al usuario a una página de recibo (receipt.html), caso contrario, se muestra una alerta para el usuario donde se indica que el carrito está vacío y no se procedió a la compra.
```javascript
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

---

### Preguntas 🐈
1. `productList` (Anteriormente nombrada `catalogo`) es una variable que almacena un arreglo de objetos. En este contexto, se utiliza para contener información sobre los productos disponibles en la tienda en línea, como sus nombres, descripciones, imágenes y precios. Además, este arreglo se utiliza para generar dinámicamente las tarjetas de productos en el catálogo de la tienda.

2. `const card = document.createElement("div")` crea un nuevo elemento HTML de tipo `<div>` y lo almacena en la variable `card`. Este elemento `<div>` se utiliza para construir una tarjeta de producto que se agregará al catálogo de la tienda en línea.

3. `card.innerHTML` se utiliza para definir el contenido HTML interno del elemento `card`. En este caso, se está configurando el contenido que tendrá cada una de las tarjetas de producto y contenido dinámico, como imágenes, nombres de productos, descripciones y precios.

4. `productListContainer.appendChild(card)` toma el elemento `card`, que representa una tarjeta de producto, y lo agrega como un hijo al elemento con el id `productListContainer`. En otras palabras, se inserta la tarjeta de producto dentro del contenedor del catálogo, lo que hace que la tarjeta se muestre en la página web.
