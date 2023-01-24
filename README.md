## Persiapan Project

- Install React
  Untuk install react js buat folder baru dengan nama aplikasi yang akan kita buat, kemudian buka folder tersebut dengan cli atau vs code langsung dan command:

  ```
      npx create-react-app .
  ```

- Rapikan file dan folder bawaan react
  Berikut langkah – langkah untuk membuat file dan folder kita rapi:

  - Buka index.js hapus reportWebVitals() dan commen2 di atasnya
  - Buat folder dan pindahkan file App.js ke folder routes tersebut
  - Hapus file App.Test.js dan setupTest.js dan logo.svg
  - Buat folder styles di dalam folder src dan pindah file index.css dan App.js ke folder styles tersebut dan sesuaikan importnya di file index.js dan App.js
  - Di dalam folder src buat folder components (untuk menampung file component), folder pages (untuk menampung file page) dan folder image untuk menampung file image.

    Hasil akhir structure foldernya akan jadi seperti ini:<br>

    ```
    __node_modules
    __public
    __src
    ____components
    _______FileComponent.jsx
    ____images
    _______FileImage.jpg
    ____pages
    _______FilePage.jsx
    ____routes
    _______App.js
    ____styles
    _______App.css
    _______index.css
    ____utils
    _______redux
    _______context
    ____index.js
    __.gitignore
    __packgage-lock.json
    __package.json
    __README.md
    ```

- Selain itu terdapat beberapa hal yang harus diperhatikan:

  - untuk nama components/class dibuat dengan pascal case, contohnya HomePage
  - untuk nama function dibuat dengan camel case, contohnya handleScroll
  - untuk nama folder dibuat dengan lower case, contonya pages
  - untuk variable yang nilainya absolut dibuat dengan uppercase, contohnya JUMLAHHARI

## Props

### Props

Props adalah suatu cara untuk mengirim dan mengakses data dari suatu component (parent component) ke component lain (child component) secara langsung. Berikut contoh penggunaannya di coding:

```
function App() {
  return (
    <div className="Parentbox">
      <FotoProduct />
      <ProductInfo title="Sarung gajah berdiri" price="74000" category="pakaian" />
    </div>
  );
}
```

App merupakan component parent yang memiliki component child `FotoProduct` dan `ProductInfo`. Component `App` akan melempar data title, price dan category ke component `ProductInfo` menggunakan props. Berikut codingan pada component `ProductInfo`:

```
function ProductInfo({ category, title, price }) {

  return (
    <div>
      <div className="Deskripsi">
        <p className="Cate">{category}</p>
        <h1 className="Title">{title}</h1>
        <p className="Price">IDR {price}</p>
        <p className="Info">
          one of the most recognizable shoes in the AJ colection, the Air Jordan
          3 Retro features lightweight, visible cushioning just like the
          original from '88, Signature details and materials celebrate the
          game-changing icon.
        </p>
      </div>
    </div>
  );
}
```

### Default Props

Defualt props merupakan nilai props yang secara otomatis akan digunakan ketika suatu component tidak diberi props. Berikut contoh penggunaanya di coding:

```
const YouTubeComp = ({ time }) => {
  return (
    <div className="youtube-wrapper">
      <div className="img-thumb">
        <img src={"https://source.unsplash.com/200x400?youtube"} />
        <p className="time">{time}</p>
      </div>
      <p className="title">Title Here</p>
      <p className="desc">desc here</p>
    </div>
  );
};

YouTubeComp.defaultProps = {
  time: "00.00",
};

export default YouTubeComp;
```

Codingan diatas merupakan codingan component child yang akan menerima props time pada tag `<p>` dan kemudian akan diberi defaultProps time dengan value “00.00”

```
const Home = () => {
  return (
    <>
      <YouTubeComp time="5.04" />
      <YouTubeComp />
    </>
  );
};
```

Codingan diatas merupakan component parent yang berisi 2 component Youtube diatas tadi dimana component YouTube pertama diberi props time dengan value “5.04” sedangan pada component YouTube kedua tidak diberi props sehingga secara otomatis akan ditampilkan props defaultnya tadi yaitu “00.00”. berikut hasilnya:

## Image

Berdasarkan sumber sourcenya terdapat dua cara untuk menampilkan image.

### Dari local

```
<img sr­c={image1} alt="gambar laptop" width={150}className="float-left mr-3" />
```

### Dari url

```
<img src={"https://source.unsplash.com/600x400"} alt="img" />
```

## Inline Style

Untuk menambahkan inline style css dapat dilakukan dengan cara berikut:

```
<div className="rounded-xl overflow-hidden card-shadow relative" style={{
width: 287, height: 386 }} >
</div>
```

Pada ukuran width dan height, satuannya otomatis dibuat dalam bentuk px.

## Conditional Rendering

Di React, tidak ada sintaks khusus untuk penulisan conditional. Sebagai gantinya, kita dapat menggunakan teknik yang sama seperti kode JavaScript biasa. Misalnya, menggunakan logika if untuk menyertakan JSX secara kondisional
Kita bisa memanfaatkan conditional logi untuk merender sebuah component. Misalnya pada saat user sudah login maka di dalam halaman akan ditampilkan component `AdminPanel` sedangkan jika user belum login maka di halaman akan tampil component `LoginForm`. Penerapannya di coding akan jadi seperti ini [[1]](https://beta.reactjs.org/learn).

```
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```

Agar code kita lebih ringkas kita bisa menggunakan ternari operator seperti ini [[1]](https://beta.reactjs.org/learn):

```
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

jika conditional hanya memiliki satu cabang kita dapat menggunakan syntax `logical &&` [[1]](https://beta.reactjs.org/learn):

```
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

## Lists Rendering

Kita dapat menggunakan fitur JavaScript seperti for loop dan fungsi array map() untuk merender list komponen. Misalnya, kita memiliki serangkaian produk:

```
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];
```

Kita bisa gunakan fungsi map() untuk mengubah array produk menjadi array item.

```
     <ul>
        {products.map((product) => (
          <li key={product.id}>
            {product.title}
          </li>
        ))}
    </ul>
```

Atau kita juga bisa meringkasnya menjadi seperti ini [[1]](https://beta.reactjs.org/learn):

```
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```

## React Router

### Install React-Router

React Router merupakan library yang digunakan untuk membuat sebuah route atau navigasi yang memungkinkan user bisa berpindah dari satu halaman ke halaman lainnya. Untuk bisa menggunakan react router kita harus mengistallnya terlebih dahulu dengan command:

```
npm i react-router-dom
```

### Konfigurasi Router

Selanjutnya kita lakukan konfigurasi di file yang kita khususkan untuk router (biasanya file App.js), seperti ini [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/App.js):

```
    import { BrowserRouter, Route, Routes } from "react-router-dom";
    import "./App.css";
    import Detail from "./pages/Detail";
    import Home from "./pages/Home";
    import Login from "./pages/Login";

    function App() {
        return (
           <BrowserRouter>
             <Routes>
               <Route path="/" element={<Home />} />
               <Route path="/:id" element={<Detail />} />
               <Route path="/login" element={<Login />} />
               <Route path="*" element={<NotFound />} />
             </Routes>
           </BrowserRouter>
         );
    }
```

Path digunakan untuk mendefinisikan alamat page website kita. Element digunakan untuk mendefinisikan component/page yang akan dituju menggunkan alamat pada path yang kita buat. Code ":id" maksudnya adalah path untuk parameter, yang membuat value id akan menjadi dinamis. Sehingga jika di bar search browser diberi alamat base-url/1 maka user akan dibawa ke page Detail dengan data dari elemen yang id-nya 1.

Sedangkan "\*" untuk menangkap semuat alamat selain alamat yang ada di path Route yang sudah kita buat sebelumnya, ini bertujuan agar user saat memasukkan alamat yang salah akan langsung diarahkan ke page `<NotFound />`. Khusus untuk Route ini harus diletakkan di urutan yang paling bawah. karena jika diletakkan diatas, alamat apapun yang diketikkan user akan ditangkap oleh Route ini meskipun alamat yang dimasukkan untuk menuju ke salah satu page dalam website itu benar.

### Link

Link ini akan menggantikan tag `<a>` pada react, bedanya hanya atribute href diganti dengan to selebihnya sama. Sebulum membuat Link kita harus import Link terlebih dahulu. Berikut contoh penggunaanya di coding:

```
import { Link } from "react-router-dom";

<ul  className="fixed bg-white inset-0 flex flex-col md:flex md:items-center"  id="menu">
  <li className="mx-3 py-6 md:py-0">
    <Link to="showcase" className="text-black  hover:underline">
      Showcase
    </Link>
  </li>
  <li className="mx-3 py-6 md:py-0">
    <Link to="catalog" className="text-black md:text-white">
      Catalog
    </Link>
  </li>
  <li className="mx-3 py-6 md:py-0">
    <Link to="delivery" className="text-black md:text-white ">
      Delivery
    </Link>
  </li>
</ul>;
```

### useNavigate()

Disebut juga parametericly bisasanya digunakan untuk membuat halaman berpindah ketika user berhasil login atau register. Untuk mengimplementasikan useNavigate(), di contoh ini kita melakukan fetching API. Berikut contoh penggunaannya di coding [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/pages/Home.jsx):

```
import React from "react";
import { useState, useEffect } from "react";

const Home = () => {
    const [user, setUsers] = useState([]);

    useEffect(() => {
        fetch("https://jsonplaceholder.typicode.com/users")
             .then((resp) => resp.json())
             .then((data) => {
               setUsers(data)
             })
             .catch((err) => console.log(err));
         []);

        return (
           <div>
             <p>Home</p>
           </div>
         );
       };

export default Home;
```

Lakukan looping map untuk data API yang telah di-fetching sebelumnya dan buat tombol button yang di dalamnya ada function handle untuk mengambil id saat button element ditekan, yang nantinya akan di jadikan path di useNavigate() [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/pages/Home.jsx):

```
import React from "react";
import { useState, useEffect } from "react";

const Home = () => {
  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((resp) => resp.json())
      .then((data) => {
        setUsers(data);
      })
      .catch((err) => console.log(err));
  }, []);

  const handleGotoDetail = (id) => {};

  return (
    <div>
      <h1>Home Page</h1>
    //------------------------------------------------------------------------------------------
      <ul>
        {users.map((user) => {
          return (
            <li key={user.id}>
              {user.name}
              <button onClick={() => handleGotoDetail(user.id)}>
                Go to Detail
              </button>
            </li>
          );
        })}
      </ul>
    //------------------------------------------------------------------------------------------
    </div>
  );
};

export default Home;
```

Selanjutnya import useNavigate, deklarasikan useNavigate() dalam variabel (di contoh navigate) dan gunakan variabel useNavigate yang di declarasikan tadi untuk membuat path menggunakan id di dalam function handle id tadi [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/pages/Home.jsx):

```
import React from "react";
import { useState, useEffect } from "react";
//-----------------------------------------------------------------------------------
import { useNavigate } from "react-router-dom";
//-----------------------------------------------------------------------------------

const Home = () => {
  const [users, setUsers] = useState([]);
  //-----------------------------------------------------------------------------------
  const navigate = useNavigate();
  //-----------------------------------------------------------------------------------

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((resp) => resp.json())
      .then((data) => {
        setUsers(data);
      })
      .catch((err) => console.log(err));
  }, []);

  const handleGotoDetail = (id) => {
    //-----------------------------------------------------------------------------------
    navigate(`/${id}`);
    //-----------------------------------------------------------------------------------
  };

  return (
    <div>
      <h1>Home Page</h1>
      <ul>
        {users.map((user) => {
          return (
            <li key={user.id}>
              {user.name}
              <button onClick={() => handleGotoDetail(user.id)}>
                Go to Detail
              </button>
            </li>
          );
        })}
      </ul>
    </div>
  );
};

export default Home;
```

sehingga hasilnya akan seperti ini:

<p align="center">
<image src="./src/images/useNavigate-result.png" alt='result of useNavigate'>
</p>

Saat button Go to Detail pada item 1 ditekan, kita akan langsung pindah ke halaman detail dan alamat url di search bar browser akan berubah dari `locallhost:3000` menjadi `locallhost:3000/1`. Begitu juga jika button pada item 2 ditekan kita akan pindah ke halaman detail dan url di bar searchnya berubah menjadi `locallhost:3000/2` begitu juga seterunya dinamis path dari useNavigate mengambil id item-item kita, Detail page tadi seperti ini hasilnya:

<p align="center">
<image src="./src/images/detailPage-useNavigate.png" alt='detailPage userNavigate'>
</p>

### useParams()

Digunakan untuk membaca url paramater. Dicontoh ini kita akan menggunakan page Detail yang telah dibuat di materi `useNavigate()` sebelumnya, dimana kita telah memilik url parameter id. Untuk bisa menggunakannya kita import `useParams()`, kemudian kita deklarasikan `useParams()` dalam satu variabel (dicontoh kita buat params). Params ini akan mengembalikan object yang isinya paramater yang ada di page yang sedang kita kerjakan (di contoh page detail) [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/pages/Detail.jsx);

```
import React from "react";
import { useParams } from "react-router-dom";

const Detail = () => {
  const params = useParams();
  console.log(params);
  return (
    <div>
      <p>Detail</p>
    </div>
  );
};

export default Detail;
```

Jika dilihat di browser saat kita masih di page home dan kita klik button `Go to Detail` di salah satu itemnya kita akan masuk di page detail item 1 dan jika kita coba console variable `params` hasilnya seperti ini:

```
Object { id: "1" }
```

Terlihat jika diconsole ternyata variabel params berisi object id. Sehingga kita dapat langsung destruct untuk mengambil id dan kita coba return id-nya seperti ini [[2]](https://github.com/argianardi/ReactRouterV6/blob/params/src/pages/Detail.jsx):

```
import React from "react";
import { useParams } from "react-router-dom";

const Detail = () => {
  const { id } = useParams();
  return (
    <div>
      <p>Detail Page</p>
      <p>Params id: {id}</p>
    </div>
  );
};

export default Detail;
```

Disini saat di home page kita tekan button `Go to Detail` di item 1, 2 dan 3 hasilnya seperti ini, sudah menunjukkan page yang dinamis tampilan page detailnya menyesuaikan masing-masing id nya, seperti ini:

<p align="center">
    <image src="./src/images/resultOfUseParams1.png"/>
    <image src="./src/images/resultOfUseParams2.png"/>
    <image src="./src/images/resultOfUseParams3.png"/>
</p>

Selanjutnya kita melakukan fetching API untuk menampilkan data detail dari masing-masing item yang diidentifikasi berdasarkan id-nya masing – masing, berikut langkah - langkahnya [[2]](https://github.com/argianardi/ReactRouterV6/blob/params/src/pages/Detail.jsx):

```
// Import useState dan useEffect
import React, { useEffect, useState } from "react";
import { useParams } from "react-router-dom";

const Detail = () => {
  const { id } = useParams();
  //declarasikan variabel untuk menampung data user (di contoh user) menggunakan hooks useState
  const [user, setUser] = useState(null);

  //lakukan fetching api dan isikan data user dari API dalam variabel yang kita deklarasikan tadi
  useEffect(() => {
    fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
      .then((resp) => resp.json())
      .then((data) => {
        setUser(data);
      })
      .catch((err) => console.log(err));
  }, [id]);
  return (
    <div>
      <p>Detail Page</p>
      <p>Params id: {id}</p>

      {/* return data user dari API tadi menggunakan tag <pre>  */}
      <pre> {JSON.stringify(user, null, 2)} </pre>
    </div>
  );
};


export default Detail;
```

Sehingga hasilnya sepert ini:

<p align="center">
    <image src="./src/images/resultOfUseParams4.png" alt='result of user params 4'/>
</p>

Dari halaman home diatas saat button `Go to Detail` pada item 1 ditekan hasilnya seperti gambar di bawah ini (kita dibawa ke detail page) dan url di search bar di browser berubah menjadi `locallhost 3000/1`

<p align="center">
    <image src="./src/images/resultOfUseParams5.png" alt='result of user params 5'/>
</p>

Begitu juga saat button `Go to Detail` pada item 2 ditekan hasilnya seperti gambar di bawah ini dan url di bar searching berubah menjadi locallhost 3000/2

<p align="center">
    <image src="./src/images/resultOfUseParams6.png" alt='result of user params 6'/>
</p>

Hal yang sama juga akan terjadi jika kita menekan button `Go to Detail` untuk elemen item lainnya.

## Referensi

- [[1] beta.reactjs.org](https://beta.reactjs.org)
- [[2] github.com/argianardi/ReactRouterV6](https://github.com/argianardi/ReactRouterV6)
