# Liquor-Store

import Header from './components/Header';
import Main from './components/Main';
import Basket from './components/Basket';
import data from './data';
import { useState } from 'react';
function App() {
  const { products_b, products_w, products_w2, products_w3, products_w4, products_t, products_t2, products_v, products_v2, products_be, products_be2, products_be3} = data;
  const [cartItems, setCartItems] = useState([]);
  const onAdd = (product) => {
    const exist = cartItems.find((x) => x.id === product.id);
    if (exist) {
      setCartItems(
        cartItems.map((x) =>
          x.id === product.id ? { ...exist, qty: exist.qty + 1 } : x
        )
      );
    } else {
      setCartItems([...cartItems, { ...product, qty: 1 }]);
    }
  };
  const onRemove = (product) => {
    const exist = cartItems.find((x) => x.id === product.id);
    if (exist.qty === 1) {
      setCartItems(cartItems.filter((x) => x.id !== product.id));
    } else {
      setCartItems(
        cartItems.map((x) =>
          x.id === product.id ? { ...exist, qty: exist.qty - 1 } : x
        )
      );
    }
  };
  return (
    <div className="App">
      <Header countCartItems={cartItems.length}></Header>
      <div className="row">
        <Main products_b={products_b} 
              onAdd={onAdd} 
              products_w={products_w}
              products_w2={products_w2}
              products_w3={products_w3}
              products_w4={products_w4}
              products_t={products_t}
              products_t2={products_t2}
              products_v={products_v}
              products_v2={products_v2}
              products_be={products_be}
              products_be2={products_be2}
              products_be3={products_be3}
              ></Main>
        <Basket
          cartItems={cartItems}
          onAdd={onAdd}
          onRemove={onRemove}
        ></Basket>
      </div>
    </div>
  );
}

export default App;
