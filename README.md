## Roadmap

Untuk alur belajar react kita bia mengikuti roadmap [ini](https://roadmap.sh/react).

## Persiapan Project

- Install React
  Untuk install react js buat folder baru dengan nama aplikasi yang akan kita buat, kemudian buka folder tersebut dengan cli atau vs code langsung dan command:

  ```
      npx create-react-app .
  ```

- Rapikan file dan folder bawaan react. Berikut langkah – langkah untuk merapikan file dan folder kita:

  - Buka index.js hapus reportWebVitals() dan commen2 di atasnya
  - Di dalam folder src, buat folder routes dan pindahkan file App.js ke folder routes tersebut
  - Hapus file App.Test.js dan setupTest.js, dan logo.svg
  - Buat folder styles di dalam folder src dan pindah file index.css dan App.js ke folder styles tersebut dan sesuaikan path importnya di file index.js dan App.js
  - Di dalam folder src buat folder components (untuk menampung file component), folder pages (untuk menampung file page) dan folder image untuk menampung file image.

    Hasil akhir structure foldernya akan jadi seperti ini:<br>

    ```
    __|node_modules
    __|public
    __|src
    ____|components
    _______|FileComponent.jsx
    ____|images
    _______|FileImage.jpg
    ____|pages
    _______|FilePage.jsx
    ____|routes
    _______|App.js
    ____|styles
    _______|App.css
    _______|index.css
    ____|utils
    _______|redux
    _______|context
    ____|index.js
    __|.gitignore
    __|packgage-lock.json
    __|package.json
    __|README.md
    ```

    folder utils digunakan untuk menyimpan file yang berisi function yang digunakan sebagai alat bantu atau utilitas yang dapat digunakan di seluruh bagian kode dalam proyek yang sama, contohnya untuk menampung code - code redux atau context.

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

## State dan UseState

### State

State adalah sebuah object untuk menyimpan data pada React dan akan di render atau muat ulang ketika data mengalami perubahan. Berikut contoh penggunaannya di coding:

```
//-------------import useState.---------------------------
import React, { useState } from "react";
//--------------------------------------------------------

const Home = () => {
  //-------------Assign state menggunakan useState------
  const [like, setLike] = useState(0);
  //--------------------------------------------------------


  const handleLike = () => {
    //-------------Upedate perubahan pada state menggunakan setState
    setLike(like + 1);
    //--------------------------------------------------------
  };

  return (
    <div className="home">
      <h3>Contact List</h3>
      //-------------Terakhir tampilkan state ------
      <h5>Like: {like}</h5>
      //--------------------------------------------------------
      <button onClick={handleLike}>Like</button>
    </div>
  );
};

export default Home;
```

### UseState

useState digunakan untuk membuat dan mengupdate state. Berikut beberapa contoh penggunaan useState:

#### useState Untuk Object

```
//----------------Import useState----------
import React, { useState } from "react";

const Home = () => {
  //---------- Assign state menggunakan useStae berbentuk object
  const [person, setPerson] = useState({
    firstName: "Ronoa",
    lastname: "Zoro",
    age: 20,
  });
 //--------------------------------------------------------------------

  const handleUpadateAge = () => {
    //---------- update state menggunakan setState dan rest parameter
    setPerson({
      ...person,
      age: person.age + 1,
    });
    //--------------------------------------------------------------------
  };

  return (
    <div className="home">
      <h3>Contact List</h3>
      //-------- Tampilkan state
      <h5>First Name: {person.firstName}</h5>
      <h5>Last Name: {person.lastname}</h5>
      <h5>Age: {person.age}</h5>
      //--------------------------------------------------------------------
      <button onClick={handleUpadateAge}>Update Age</button>
    </div>
  );
};

export default Home;
```

#### useState Untuk Nesting Object

```
 //-----------------Import useState ----------------
import React, { useState } from "react";

const Home = () => {

  const [person, setPerson] = useState({
    //---------- Assign state menggunakan useStae untuk nesting object
    firstName: "Ronoa",
    lastname: "Zoro",
    age: 20,
    track: {
      fight: 30,
      bounty: 30000,
    },
    //--------------------------------------------------------------------
  });

  const handleUpdateAge = () => {
    setPerson({
      ...person,
      age: person.age + 1,
    });
  };

  const handleUpdateFight = () => {
    //---------- update state menggunakan setState dan rest parameter
    setPerson({
      ...person,
      track: {
        ...person.track,
        fight: person.track.fight + 1,
      },
    });
    //--------------------------------------------------------------------
  };

  return (
    <div className="home">
      <h3>Contact List</h3>
      //-----------------Tampilkan state ---------------
      <h5>First Name: {person.firstName}</h5>
      <h5>Last Name: {person.lastname}</h5>
      <h5>Age: {person.age}</h5>
      <h5>Track:</h5>
      <ul>
        <li>fight: {person.track.fight}</li>
        <li>bounty: {person.track.bounty}</li>
      </ul>
      //--------------------------------------------------------------------
      <button onClick={handleUpdateAge}>Update Age</button>
      <button onClick={handleUpdateFight}>Update Fight</button>
    </div>
  );
};

export default Home;
```

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

## Event Handler

Berikut contoh penggunaan dari event handler:

```
import React from "react";

//-------------------------------------------------------------------------------
const Home = () => {
  const handleClick = (message) => {
    console.log(`${message}`);
  };
//-------------------------------------------------------------------------------

  return (
    <div className="home">
      <h3>Contact List</h3>
//-------------------------------------------------------------------------------
      <button onClick={() => handleClick("Clicked")}>Click</button>
//-------------------------------------------------------------------------------
    </div>
  );
};

export default Home;
```

Untuk membuat event handler pertama kita harus menyiapkan function yang nantinya akan dijalankan saat kita men-trigger event yang kita buat (di contoh function handleClick). Kemudian buat event handler-nya (di contoh event onClick) di salah satu elemen yang kita buat di contoh (di button). Terakhir di event handler yang kita buat tadi kita panggil function yang telah kita buat tadi (function handleClick) dengan memanfaatkan anonymous function.

Dari code di atas akan menghasilkan button dengan nama `Click`, saat kita menekan tombol tersebut maka di console akan tercetak sebuah message yang kita set (Clicked).

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

Disebut juga parametericly bisasanya digunakan untuk pindah dari suatu halaman ke halaman lainnya untuk mengaplikasikannya kita harus memasukkan useNavigate() ini kedalam suatu function dan nantinya function tersebut akan dijadikan value untuk suatu event (biasanya onClick atau onSubmit). Berikut contoh penggunaannya di coding [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/pages/Home.jsx):

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

Digunakan untuk membaca url paramater. Dicontoh ini kita akan menggunakan page Detail yang telah dibuat di materi `useNavigate()` sebelumnya, dimana kita telah memilik url parameter id. Untuk bisa menggunakannya kita import `useParams()`, kemudian kita deklarasikan `useParams()` dalam satu variabel (dicontoh kita buat params). Params ini akan mengembalikan object yang isinya paramater yang ada di url page yang sedang kita kerjakan (di contoh page detail) [[2]](https://github.com/argianardi/ReactRouterV6/blob/navigate/src/pages/Detail.jsx);

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

## useEffect

UseEffect digunakan untuk menambahkan side effect di functional component. Side effect adalah function yang dieksekusi setelah komponen dirender. UseEffect hooks akan menerima dua parameter, yaitu sebuah callback dan sebuah array.

```
useEffect(() => {
    fn();
}, []);
```

Array di parameter kedua ini, bisa di isi atau bisa juga dikosongkan. Kalau arraynya kosong, maka useEffect akan dijalankan sekali saja, yaitu saat komponen pertama kali di render. Jika arraynya diisi item maka useEffect ini akan dijalankan setiap kali item di dalam array tersebut berubah. Salah satu kondisi dimana kita bisa menggunakan useEffect() adalah disaat kita harus fetch data dari server:

```
import React, { useEffect, useState } from "react";
import axios from "axios";
const baseUrl = "https://api.themoviedb.org/";
const page = 1;

const NowPlayingMovies = () => {
  const [movies, setMovies] = useState([]);
  const { toggle } = useMoveContext();

  //----------------------------------------------------------------------------------
  useEffect(() => {
    getMovies();
  }, []);
  //----------------------------------------------------------------------------------

  const getMovies = async () => {
    await axios
      .get(
        `${baseUrl}3/movie/now_playing?api_key=${process.env.REACT_APP_API_KEY}&language=en-US&page=${page}`
      )
      .then((response) => {
        setMovies(response.data.results);
      })
      .catch((error) => {
        console.log(error);
        alert("error");
      });
  };

  return (
    <>
      <NavigationBar />
      <div
        className="d-flex flex-wrap justify-content-around "
        style={{ background: toggle ? "#E9DCC9" : "#28282B" }}
      >
        {movies.map((movie) => {
          return (
            <CardMovies
              src={"https://image.tmdb.org/t/p/original/" + movie.poster_path}
              title={movie.title}
              key={movie.id}
              onClick={() => handleDetailPage(movie)}
              onClick2={() => handleFav(movie)}
            />
          );
        })}
      </div>
    </>
  );
};

export default NowPlayingMovies;
```

Kita sebenarnya bisa membuat useEffect tanpa adanya parrameter array tersebut, akibatnya useEffect akan selalu di panggil pada saat terjadinya re-render. Jadi apapun yang sifatnya re-render, maka fungsi di atas akan terus muncul.

```
import React, { useEffect, useState } from 'react';

const Home = () => {
    const [name, setName] = useState('');
    //---------------------------------------------------------------
    useEffect(() => console.log('Always rendered.'));
    //---------------------------------------------------------------

    return <input type='text' value={name} onChange={(e) => setName(e.target.value)} />;
}

export default Home;
```

Hasilnya, setiap kita ketikkan text di dalam component input itu, maka `console.log('Always rendered.')` akan selalu dijalankan. Hal ini bisa menyebabkan crash atau memory leak.

## Setting json-server (fake api)

Berikut langkah - langkah untuk setting fake api menggunakan json-server [[4]](https://www.youtube.com/watch?v=P58T93q9QrE&list=PLW-kCRbRHdAGefLJN0PbmcGz5zp6Kt0Ut&index=12&t=4s):

- Install json-server, dengan command:
  ```
  npm i json-server
  ```
- Buat file json dan isikan data yang kita perlukan. yang nantinya akan kita gunakan untuk menyimpan data kita (sebaiknya namai filenya dengan db.json). Berikut contoh isi datanya:

  ```
  {
    "kontaks": [
      {
        "id": 1,
        "nama": "Paijo",
        "No": "086745455454"
      },
      {
        "id": 2,
        "nama": "Tukijo",
        "No": "086749499494"
      }
    ]
  }
  ```

- Selanjutnya di file `package.json` tepatnya di object scripts tambahkan property baru dengan key `server` dan valuenya `json-server -w <path file json> -p <port>`

  ```
  {
    "name": "sinau-redux",
    "version": "0.1.0",
    "private": true,
    "dependencies": {
      "@testing-library/jest-dom": "^5.16.5",
      "@testing-library/react": "^13.4.0",
      "@testing-library/user-event": "^13.5.0",
      "axios": "^1.2.6",
      "json-server": "^0.17.1",
      "react": "^18.2.0",
      "react-dom": "^18.2.0",
      "react-redux": "^8.0.5",
      "react-router-dom": "^6.8.0",
      "react-scripts": "5.0.1",
      "redux": "^4.2.1",
      "redux-thunk": "^2.4.2",
      "web-vitals": "^2.1.4"
    },
    "scripts": {
      "start": "react-scripts start",
      "build": "react-scripts build",
      "test": "react-scripts test",
      "eject": "react-scripts eject",
      //-------------------------------------------------------------------------------
      "server": "json-server -w db/db.json -p 2023"
      //-------------------------------------------------------------------------------
    },
    "eslintConfig": {
      "extends": [
        "react-app",
        "react-app/jest"
      ]
    },
    "browserslist": {
      "production": [
        ">0.2%",
        "not dead",
        "not op_mini all"
      ],
      "development": [
        "last 1 chrome version",
        "last 1 firefox version",
        "last 1 safari version"
      ]
    }
  }
  ```

- Terakhir untuk menjalankannya di terminal lakukan command:

  ```
  npm run server
  ```

## CRUD (post/get/put/delete request)

### Get request

Sebelum melakukan request data melalui api kita harus menyiapkan base url dan axion di file lain (`src/api/<namaFile.js>`) agar lebih rapi yang nanti selanjutnya bisa kita import di file tempat melaukan request api (get,post, put atau delete).

```
import axios from "axios";

export default axios.create({
  baseURL: "http://localhost:4444",
});
```

Untuk melakukan get request, selain harus menggunakan axios atau fetching dari javascript kita juga harus menggunakan useEffect:

```
import React, { useEffect, useState } from "react";
import ContactList from "./ContactList";
import Api from "../api/contactApi";

const Home = () => {
  const [contacts, setContacts] = useState([]);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

//-----------------------------------------------------------------------------
  useEffect(() => {
    getContacts();
  }, []);

  const getContacts = async () => {
    await Api.get("/contacts")
      .then((res) => {
        setContacts(res.data);
      })
      .catch((err) => {
        setError(err.message);
      })
      .finally(() => {
        setLoading(false);
      });
  };
//-----------------------------------------------------------------------------

  return (
    <div>
      <div className="home">
        {loading && <div>loading..........</div>}
        <h3>Contact List</h3>
        {error && <div>{error}</div>}

        {contacts.map((contact) => (
          <ContactList
            key={contact.id}
            name={contact.name}
            number={contact.number}
          />
        ))}
      </div>
    </div>
  );
};

export default Home;
```

### Delete Request

Untuk melakukan post request kita membuatuhkan parameter berupa id dari item yang akan kita hapus. Di dalam function delete request kita harus menambahkan functin get request agar kita mendapatkan data terbaru setelah kita menghapus item. Dan terakhir kita harus menambahkan function delete request ke even handler onClick di button.

```
import React, { useEffect, useState } from "react";
import ContactList from "./ContactList";
import Api from "../api/contactApi";

const Home = () => {
  const [contacts, setContacts] = useState([]);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    getContacts();
  }, []);

  const getContacts = async () => {
    await Api.get("/contacts")
      .then((res) => {
        setContacts(res.data);
      })
      .catch((err) => {
        setError(err.message);
      })
      .finally(() => {
        setLoading(false);
      });
  };

//-------------------------------------------------------------------------
  const handleDelete = async (id) => {
    await Api.delete(`/contacts/${id}`).then((res) => {
      getContacts();
    });
  };
//-------------------------------------------------------------------------

  return (
    <div>
      <div className="home">
        {loading && <div>loading..........</div>}
        <h3>Contact List</h3>
        {error && <div>{error}</div>}

        {contacts.map((contact) => (
          <ContactList
            key={contact.id}
            name={contact.name}
            number={contact.number}
      //-------------------------------------------------------------------------
            onDelete={() => handleDelete(contact.id)}
      //-------------------------------------------------------------------------
          />
        ))}
      </div>
    </div>
  );
};

export default Home;
```

### Post Request

Untuk membuat post kita harus menyiapkan function yang berfungsi untuk melakukan post request yang nantinya dijadikan value untuk event onSubmit di tag form, di dalamnya terdapat:

- post request
- state loading
- navigasi ke halaman sebelumnya (biasanya menggunakan useNavigate)

```
import React, { useState } from "react";
import { useNavigate } from "react-router-dom";
import Api from "../api/contactApi";

const Create = () => {
  const navigate = useNavigate();

  const [name, setName] = useState("");
  const [number, setNumber] = useState("");
  const [loading, setLoading] = useState(false);

  const handleSubmit = (e) => {
    e.preventDefault();
    const contact = { name, number };
    setLoading(true);
    Api.post("/contacts", contact).then((res) => {
      console.log(res);
      setLoading(false);
      navigate("/");
    });
  };

  return (
    <div className="contact-form">
      <h3>Contact Form</h3>
      <form onSubmit={handleSubmit}>
        <div className="form-group">
          <label htmlFor="" className="control-label">
            Contact name
          </label>
          <input
            type="text"
            className="form-control"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
        </div>
        <div className="form-group">
          <label htmlFor="" className="control-label">
            Contact number
          </label>
          <input
            type="text"
            className="form-control"
            value={number}
            onChange={(e) => setNumber(e.target.value)}
          />
        </div>
        <div className="btn-group">
          <button
            type="button"
            className="btn btn-danger"
            onClick={() => navigate("/")}
          >
            Cancel
          </button>
          <button type="submit" className="btn btn-primary">
            {loading ? "Submiting....." : "Submit"}
          </button>
        </div>
      </form>
    </div>
  );
};

export default Create;
```

### Put Request

Di contoh ini Put request dijadikan satu file dengan post request, jadi di dalam function handle submit kita harus beri logic jika terdapat data id di param maka jalankan function put requst tetapi jika tidak ada maka jalankan post request.

```
import React, { useEffect, useState } from "react";
import { useNavigate, useParams } from "react-router-dom";
import Api from "../api/contactApi";

const Create = () => {
  const navigate = useNavigate();
  const { id } = useParams();

  const [name, setName] = useState("");
  const [number, setNumber] = useState("");
  const [loading, setLoading] = useState(false);

//------------------------------------------------------------------------
  useEffect(() => {
    if (id) {
      Api.get(`/contacts/${id}`).then((res) => {
        const { data } = res;
        setName(data.name);
        setNumber(data.number);
      });
    }
  }, [id]);

  const handleSubmit = (e) => {
    e.preventDefault();
    const contact = { name, number };
    setLoading(true);

    if (id) {
      updateContact(contact);
    } else {
      createContact(contact);
    }
  };

  const createContact = (contact) => {
    Api.post("/contacts", contact).then((res) => {
      setLoading(false);
      navigate("/");
    });
  };

  const updateContact = (contact) => {
    Api.put(`/contacts/${id}`, contact).then(() => {
      setLoading(false);
      navigate("/");
    });
  };
//------------------------------------------------------------------------

  return (
    <div className="contact-form">
      <h3>{id ? "Upadate" : "Add"} Contact</h3>
      <form onSubmit={handleSubmit}>
        <div className="form-group">
          <label htmlFor="" className="control-label">
            Contact name
          </label>
          <input
            type="text"
            className="form-control"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
        </div>
        <div className="form-group">
          <label htmlFor="" className="control-label">
            Contact number
          </label>
          <input
            type="text"
            className="form-control"
            value={number}
            onChange={(e) => setNumber(e.target.value)}
          />
        </div>
        <div className="btn-group">
          <button
            type="button"
            className="btn btn-danger"
            onClick={() => navigate("/")}
          >
            Cancel
          </button>
          <button type="submit" className="btn btn-primary">
            {loading ? "Submiting....." : "Submit"}
          </button>
        </div>
      </form>
    </div>
  );
};

export default Create;
```

## Active Link

Active Link ini digunakan di dalam component navbar untuk membuat salah satu menu navigasinya memiliki style yang berbeda (bisanya warnanya lebih gelap atau lebih terang atu bisa juga di beri underline) yang menandakan bahwa menu tersebut sedang active, yang berarti bahwa kita sedang berada di page tempat path menu navigasi tersebut. Untuk bisa menggunakannya kita harus import NavLink dari react-router-dom.

```
import React from "react";
import { NavLink } from "react-router-dom";

const Navbar = () => {
  return (
    <nav>
      <h1>Phone Contact</h1>
      <div className="nav-menu">
        <NavLink to="/" activeclassname="active">
          Home
        </NavLink>
        <NavLink to="create" activeclassname="active">
          New Contact
        </NavLink>
      </div>
    </nav>
  );
};

export default Navbar;
```

Pada menu tag `<NavLink to="/" activeclassname="active">` terdapat `activeclassname"active"` artinya saat kita berada di page dengan path `/`, class `active` tersebut akan dijalankan. Di mana class `active` inilah yang akan membuat style pada menu navbar dengan path `/` ini akan berbeda. class `active` tersebut bisa kita set sendiri.

## Redux

Redux adalah lebrary yang digunakan untuk mengelola state agar bisa dijadikan global state. Global state adalah state yang dapat dipakai di semua komponen atau halaman. Redux ini ibarat data base di fronted di mana kita bisa menambah, mengahapus dan mengambil data yang dibungkus dalam state. Redux memiliki tiga komponen utama yaitu action, reducer, dan store:

- Action dalah sebuah function yang mereturn sebuah objek. Objek tersebut memiliki sebuah property wajib yaitu type. Type inilah yang menentukan bagaimana statenya akan diubah.
- Reducer adalah sebuah fungsi yang tugasnya untuk mengolah state yang ada di store. Misal menambah data, menghapus data, mengambil data, dsb. Ada 2 parameter wajib dari reducer, yaitu state dan action.
- Store adalah tempat untuk menampung state.

Pada dasarnya, terdapat tiga fungsionalitas utama yang ditambahkan oleh redux kedalam aplikasi, Yaitu tempat untuk menyimpan keseluruhan state aplikasi, mekanisme untuk men-dispatch action kedalam reducer, dan mekanisme untuk memberi tahu setiap kali update state terjadi.

Satu-satunya cara untuk mengubah state di dalam store adalah dengan memanggil method bernama dispatch yang berisi action, kemudian Redux akan mengeksekusi reducer yang sesuai. Dan Selector merupakan function yang digunakan untuk mendapatkan data dari state yang ada di dalam store.

Sebaiknya redux ini digunakan jika:

- Banyak data yang berubah dari waktu ke waktu
- Pengelolaan state harus dilakukan di satu tempat
- Mengelola state di top-level component sudah tidak lagi relevan

Istilah - istilah yang ada di dalam React:

- Store: Store adalah tempat di mana state (keadaan) aplikasi disimpan. Store ini bersifat immutable (tidak dapat diubah), artinya state hanya dapat diubah melalui action.
- Action: Action adalah objek yang digunakan untuk mengirim perintah ke store untuk mengubah state. Action harus memiliki properti "type" yang menjelaskan tipe perubahan yang akan dilakukan, dan dapat memiliki properti lain yang dibutuhkan.
- Reducer: Reducer adalah sebuah fungsi yang menerima dua parameter yaitu state dan action, dan menghasilkan state baru yang telah diperbarui. Reducer harus bersifat pure (murni), artinya tidak boleh mengubah parameter yang diterimanya, dan harus selalu menghasilkan hasil yang sama jika diberikan parameter yang sama.
- Dispatch adalah function yang digunakan untuk memperbarui state di dalam store. Jadi dispatch ini digunakan untuk mengirimkan action ke store. Setelah action terkirim ke store, reducer akan memeriksa tipe action dan mengubah state di dalam store sesuai dengan informasi yang ada pada objek action. Setelah state di dalam store berhasil diperbarui, Redux akan memberi tahu semua komponen yang terhubung ke store Redux sehingga tampilan dari aplikasi dapat diperbarui sesuai dengan state yang baru.
- Selector: Selector adalah sebuah sebuah hook yang digunakan untuk memilih dan mengambil state yang tersimpan di store agar bisa digunakan oleh komponen react untuk di tampilkan ke dalam UI. Selector dapat digunakan untuk memisahkan state menjadi beberapa bagian kecil, yang kemudian dapat diakses dan digunakan oleh komponen React.
- Middleware: Middleware adalah fungsi yang berjalan di antara dispatch dan reducer. Middleware dapat digunakan untuk melakukan tugas tertentu, seperti logging, atau memodifikasi action sebelum action tersebut dijalankan oleh reducer.
- Provider: Provider adalah komponen React yang digunakan untuk memberikan store ke seluruh komponen dalam aplikasi. Provider akan menempatkan store di dalam context React, sehingga komponen dalam aplikasi dapat mengakses store melalui context.

Kali ini kita akan membahas redux menggunakan contoh project [saveContacts](https://github.com/argianardi/saveContacts).

### Prepare & Get request

Untuk persiapan menggunakan redux di contoh ini kita harus menginstall axios, redux, react-redux dan redux-thunk dengan command [[1]](https://www.youtube.com/watch?v=NBY70QmxSUE&list=PLIan8aHxsPj082k6ZLyqJPCJESBG-C_Lw&index=1):

```
npm i axios redux react-redux redux-thunk
```

Selanjutnya jalankan langkah - langkah berikut [[1]](https://www.youtube.com/watch?v=NBY70QmxSUE&list=PLIan8aHxsPj082k6ZLyqJPCJESBG-C_Lw&index=1):

- Di dalam folder src buat folder utils dan di dalamnya buat folder redux. Di dalam folder redux inilah kita akan menampung semua file - file yang berhubungan dengan redux.
- Di dalam folder src buat folder reducers, kemudian di dalam folder reducers ini buat folder contact untuk mengelola state yang berhubungan dengan contact. Di dalam folder contact buat file `index.js` dan code berikut:

  ```
  const initialState = {};

  const contact = (state = initialState, action) => {
    switch (action.type) {
      default:
        return state;
    }
  };

  export default contact;
  ```

- Kemudian di dalam folder `reducers` (src/utils/redux/reducers) buat file `index.js`. Di dalam file `index.js` ini kita kumpulkan semua reducers dengan menggunakan `combindeReducers` yang kita import dari redux:

  ```
  import { combineReducers } from "redux";
  import contactReducer from "./contact";

  export default combineReducers({
    contactReducer,
  });
  ```

- Di file `index.js` (src/routes/index.js) jalankan langakah - langkah berikut:

  1. Import:

     - legacy_createStore (agar lebih rapi jadikan as createStore), compose, dan applyMiddleware dari redux
     - Provider dari react-redux
     - redux-thunk dari redux-thunk

  2. Inisialisasi Store menggunakan createStore, reducers (yang kita buat tadi), dan middleware thunk
  3. Terakhir bungkus component App menggunakan Provider dengan parameter store tadi.

  ```
  import React from "react";
  import ReactDOM from "react-dom/client";
  import "./styles/index.css";
  import App from "./routes/App.js";
  //------------------------------------------------------------------------------i
  import {
    legacy_createStore as createStore,
    applyMiddleware,
    compose,
  } from "redux";
  import thunk from "redux-thunk";
  import { Provider } from "react-redux";
  //--------------------------------------------------------------------------------
  import reducers from "./utils/redux/reducers";

  //-------------------------------------------------------------------------------ii
  const store = createStore(reducers, compose(applyMiddleware(thunk)));
  //--------------------------------------------------------------------------------

  const root = ReactDOM.createRoot(document.getElementById("root"));
  root.render(
    <>
  //-------------------------------------------------------------------------------iii
      <Provider store={store}>
        <App />
      </Provider>
  //--------------------------------------------------------------------------------
    </>
  );
  ```

- Di dalam folder `src` buat folder actions, kemudian di dalam folder `actions` ini buat file `contactAction.js.` File `contactAction.js` ini akan memuat code action untuk contact. Di dalam file ini kita melakukan:

  1. Import axios
  2. Membuat constanta yang nantinya akan dijadikan type untuk dipassing ke reducers
  3. Buat function untuk mereturn dispatch. Dispatch berfungsi sebagai penghubung untuk meneruskan semua action yang didapat dari event handler di UI ke Redux store dan menghubungkan action ke reducer.

     - Pertama kita harus buat dispatch untuk loading yang nantinya akan kita oper ke reducer
     - Selanjutnya kita buat dispatch untuk get Api, kita siapkan 2 dispatch. Satu dispatch untuk kondisi sukes get request api dan satu lagi dispatch untuk kondisi gagal get request api.

  ```
  //----------------------------------------------------------------------------i&ii
    import axios from "axios";

    export const GET_LIST_CONTACT = "GET_LIST_CONTACT";
  //--------------------------------------------------------------------------------

  //-----------------------------------------------------------------------------iii
    export const getListContact = () => {
      console.log("2. masuk action");

      return (dispatch) => {
        // Loading
        dispatch({
          type: GET_LIST_CONTACT,
          payload: {
            loading: true,
            data: false,
            errorMessage: false,
          },
        });

        // get API
        axios
          .get("http://localhost:2023/contacts")
          .then((response) => {
            // berhasil get api
            console.log("3. Berhasil dapat data: ", response);
            dispatch({
              type: GET_LIST_CONTACT,
              payload: {
                loading: false,
                data: response.data,
                errorMessage: false,
              },
            });
          })
          .catch((error) => {
            // gagal get api
            console.log("4. Gagal dapat data:", error.message);
            dispatch({
              type: GET_LIST_CONTACT,
              payload: {
                loading: false,
                data: false,
                errorMessage: error.message,
              },
            });
          });
      };
    };
  //--------------------------------------------------------------------------------
  ```

- Selanjutnya kita ke component `ListContact` [src/components/ListContact.jsx], kita panggil function `getListContact()` (function yang mereturn dispatch) di action yang kita buat tadi. Panggil action tadi di bagian useEffect menggunakan dispatch.

  ```
  import React, { useEffect } from "react";
  //--------------------------------------------------------------------------------
  import { useDispatch } from "react-redux";
  import { getListContact } from "../utils/redux/actions/contactAction";
  //--------------------------------------------------------------------------------

  const ListContact = () => {
    //------------------------------------------------------------------------------
    const dispatch = useDispatch();
    //------------------------------------------------------------------------------

    useEffect(() => {
      // panggil action getListContact
      console.log("1. useEffect component did mount (di ListContact Component");
      //----------------------------------------------------------------------------
      dispatch(getListContact());
     //-----------------------------------------------------------------------------
    }, [dispatch]);

    return (
      <div>
        <h1>ListKontak</h1>
      </div>
    );
  };

  export default ListContact;
  ```

- Kemudian jika kita coba jalankan project kita maka di dalam console akan tampil seperti ini:

  ```
  1. useEffect component did mount (di ListContact Component ListContact.jsx:10
  2. masuk action contactAction.js:6
  3. Berhasil dapat data:
  Object { data: (2) […], status: 200, statusText: "OK", headers: {…}, config: {…}, request: XMLHttpRequest }
  ```

  Hasil tersebut menandakan bahwa kita telah berhasil sampai tahap ini, sekaligus menunjukkan alurnya dimulai dari `useEffect` kemudian masuk ke `action` dan menjalankan dispatch untuk get request.

- Selanjutnya kita masuk ke reducer bagian contact [src/utils/reducers/contact/index.js].

  - Import constanta type `GET_LIST_CONTACT` yang kita buat di action contact tadi [src/utils/redux/actions/contactAction.js]
  - Buat state get request di bagian `initalState`
  - Buat switch case menggunakan type yang kita import tadi (`GET_LIST_CONTACT`)

    ```
    import { GET_LIST_CONTACT } from "../../actions/contactAction";

    const initialState = {
      getListContactResult: false,
      getListContactLoading: false,
      getListContactError: false,
    };

    const contact = (state = initialState, action) => {
      switch (action.type) {
        case GET_LIST_CONTACT:
          console.log("4. masuk reducer");
          return {
            ...state,
            getListContactResult: action.payload.data,
            getListContactLoading: action.payload.loading,
            getListContactError: action.payload.errorMessage,
          };
        default:
          return state;
      }
    };

    export default contact;
    ```

- Selanjutnya kita ke component `ListContact` [src/components/ListContact.jsx]

  1. Import state getListContactResult, getListContactLoading dan getListContactError yang kita buat di bagian reducers tadi menggunakan useSelector yang kita import dari react-redux
  2. Tampilkan ketiga state tadi (getListContactResult, getListContactLoading dan getListContactError) ke view/UI dengan logic jika di kondisi state `getListResult` bernilai true maka lakukan maping, tetapi jika state `getListResult` bernilai false dan state `getListContactLoading` true maka tampilkan keterangan loading, tetapi jika state `getListResult` dan `getListLoading` bernilai false dan state `getListContactError` true maka tampilkan error message.

  ```
  import React, { useEffect } from "react";
  import { useDispatch, useSelector } from "react-redux";
  import { getListContact } from "../utils/redux/actions/contactAction";

  const ListContact = () => {
    //--------------------------------------------------------------------------------------------------------------------i
    const { getListContactResult, getListContactLoading, getListContactError } = useSelector((state) => state.ContactReducer);
    //----------------------------------------------------------------------------------------------------------------------
    const dispatch = useDispatch();

    useEffect(() => {
      // panggil action getListContact
      console.log("1. useEffect component did mount (di ListContact Component)");
      dispatch(getListContact());
    }, [dispatch]);

    return (
      <>
        <h4>ListKontak</h4>
        //--------------------------------------------------------------------------------------------------------------------ii
        {getListContactResult ? (
          getListContactResult.map((contact) => (
            <p key={contact.id}>
              {" "}
              {contact.name} - {contact.nohp}
            </p>
          ))
        ) : getListContactLoading ? (
          <p>Loading....</p>
        ) : (
          <p>{getListContactError ? getListContactError : "Data Kosong"}</p>
        )}
        //----------------------------------------------------------------------------------------------------------------------
      </>
    );
  };

  export default ListContact;
  ```

  Maka jika kita coba jalankan project kita maka data state yang berisi nama dan no hp user akan tampil di UI component `ListContact` dan di console akan tampil seperti ini (di kondisi get requesnya tidak error):

  ```
  1. useEffect component did mount (di ListContact Component ListContact.jsx:12
  2. masuk action contactAction.js:6
  4. masuk reducer index.js:12
  3. Berhasil dapat data:
  Object { data: (2) […], status: 200, statusText: "OK", headers: {…}, config: {…}, request: XMLHttpRequest }
  contactAction.js:23
  4. masuk reducer index.js:12
  ```

  Di sana terlihat alurnya:

  - pertama masuk ke `useEffect`
  - Kemudian ke `action`(awal action) kemudian masuk dispatch loading
  - Lanjut ke `reducer` untuk mendapatkan hasil payload loading
  - Setalah payload loading bernilai false masuk ke `action` lagi untuk menjalankan dispatch get request
  - Terkhir masuk ke `reducer` lagi untuk mendapatkan hasil get request bisa data atau error message, jika requestnya berhasil maka kita akan mendapatkan data tetapi jika gagal maka kita akan mendapatkan error message.

  Berikut hasilnya di console jika get requestnya gagal:

  ```
  1. useEffect component did mount (di ListContact Component ListContact.jsx:12
  2. masuk action contactAction.js:6
  4. masuk reducer index.js:12
  3. Gagal dapat data: Request failed with status code 404 contactAction.js:35
  4. masuk reducer index.js:12
  ```

### Post Request

- Karena kita sudah prepare di bagian get request tadi, kita bisa langsung ke bagian action [src/utils/redux/actions/contactAction.js]. Sama seperti di get request tadi lakukan hal berikut:

  1. Membuat constanta untuk post request yang nantinya akan dijadikan type untuk dipassing ke reducers
  2. Buat function untuk mereturn dispatch untuk post request dengan parameter data.

     - Pertama kita harus buat dispatch untuk loading yang nantinya akan kita oper ke reducer
     - Selanjutnya kita buat dispatch untuk post Api, kita siapkan 2 dispatch. Satu dispatch untuk kondisi post request sukes dan satu lagi dispatch untuk kondisi post request api gagal.

  ```
  import axios from "axios";

  export const GET_LIST_CONTACT = "GET_LIST_CONTACT";
  //----------------------------------------------------------------------------i
  export const ADD_CONTACT = "ADD_CONTACT";
  //-----------------------------------------------------------------------------

  export const getListContact = () => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: GET_LIST_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // get API
      axios
        .get("http://localhost:2023/contacts")
        .then((response) => {
          // berhasil get api
          dispatch({
            type: GET_LIST_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal get api
          dispatch({
            type: GET_LIST_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };

  //-----------------------------------------------------------------------------ii
  export const addContact = (data) => {
    console.log("2. masuk action");
    return (dispatch) => {
      // Loading
      dispatch({
        type: ADD_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // post API
      axios
        .post("http://localhost:2023/contacts", data)
        .then((response) => {
          // berhasil post api
          console.log("3. Berhasil dapat data: ", response);
          dispatch({
            type: ADD_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal post api
          console.log("3. Gagal dapat data:", error.message);
          dispatch({
            type: ADD_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };
  //--------------------------------------------------------------
  ```

- Selanjutnya kita masuk ke reducer bagian contact [src/utils/reducers/contact/index.js].

  1. Import constanta type `ADD_CONTACT` yang kita buat di action contact [src/utils/redux/actions/contactAction.js] tadi.
  2. Buat state di bagian post request `initalState`
  3. Buat switch case menggunakan type yang kita import tadi (`ADD_CONTACT`)

  ```
  //---------------------------------------------------------------------------i
  import { GET_LIST_CONTACT, ADD_CONTACT } from "../../actions/contactAction";
  //---------------------------------------------------------------------------

  const initialState = {
    // get request
    getListContactResult: false,
    getListContactLoading: false,
    getListContactError: false,

  //---------------------------------------------------------------------------ii
    // post request
    addContactResult: false,
    addContactLoading: false,
    addContactError: false,
  //---------------------------------------------------------------------------
  };

  const contact = (state = initialState, action) => {
    switch (action.type) {
      case GET_LIST_CONTACT:
        return {
          ...state,
          getListContactResult: action.payload.data,
          getListContactLoading: action.payload.loading,
          getListContactError: action.payload.errorMessage,
        };

      //---------------------------------------------------------------------------iii
      case ADD_CONTACT:
        console.log("4. masuk reducer");
        return {
          ...state,
          addContactResult: action.payload.data,
          addContactLoading: action.payload.loading,
          addContactError: action.payload.errorMessage,
        };
      //---------------------------------------------------------------------------
      default:
        return state;
    }
  };

  export default contact;
  ```

- Selanjutnya kita ke folder components [src/components] Buat component `AddContact` [src/components/AddContact.jsx]

  1. Buat form, state dan event handler untuk menambahkan data untuk post request
  2. Di dalam function handleSubmit tambahkan action `addContact` yang kita buat di `contactAction` [src/utils/redux/actions/contactAction.js] tadi menggunakan dispatch
  3. Karena component `AddContact` diletakkan satu halaman (di halaman Home) dengan component `ListContact`, agar setelah kita menambahkan hasilnya datanya bisa langsung terupdate tanpa harus direload kita harus memanggil 'getListContact()' dari action [src/utils/redux/actions/contactAction.js] di dalam useEffect dengan logic jika `addContactResult`(dari reducer) true maka panggil action `getListContact()` tadi.

     ```
     import React, { useEffect, useState } from "react";
     import { useDispatch, useSelector } from "react-redux";
     import {
       addContact,
       getListContact,
     } from "../utils/redux/actions/contactAction";

     const AddContact = () => {
       const dispatch = useDispatch();
       //-----------------------------------------------------------------------------------------iii
       const { addContactResult } = useSelector((state) => state.ContactReducer);
      //-------------------------------------------------------------------------------------------
       const [name, setName] = useState("");
       const [nohp, setNohp] = useState("");

       const handleSubmit = (e) => {
         e.preventDefault();
         console.log("1. masuk handle submit");
         //-------------------------------------------------------------------------------------------ii
         dispatch(addContact({ name, nohp }));
         //-------------------------------------------------------------------------------------------
       };

      //-------------------------------------------------------------------------------------------iii
       useEffect(() => {
         if (addContactResult) {
           dispatch(getListContact());
         }
       }, [addContactResult, dispatch]);
       //-------------------------------------------------------------------------------------------

       return (
         <div>
           <h4>Add Contact</h4>
           <form onSubmit={handleSubmit}>
             <input
               type="text"
               name="name"
               placeholder="Name...."
               value={name}
               onChange={(e) => setName(e.target.value)}
             />
             <input
               type="text"
               name="nohp"
               placeholder="No HP...."
               value={nohp}
               onChange={(e) => setNohp(e.target.value)}
             />
             <button type="submit">Submit</button>
           </form>
         </div>
       );
     };

     export default AddContact;
     ```

### Delete Request

- Sama seperti post request tadi, Karena kita sudah prepare di bagian get request jadi kita bisa langsung ke bagian action [src/utils/redux/actions/contactAction.js] dan lakukan:

  1. Buat constanta untuk delete request yang nantinya akan dijadikan type untuk dipassing ke reducers
  2. Buat function untuk mereturn dispatch untuk Delete request dengan parameter data.

     - Pertama kita harus buat dispatch untuk loading yang nantinya akan kita oper ke reducer
     - Selanjutnya kita buat dispatch untuk delete Api, kita siapkan 2 dispatch. Satu dispatch untuk kondisi post request sukes dan satu lagi dispatch untuk kondisi post request api gagal.

  ```
  import axios from "axios";

  export const GET_LIST_CONTACT = "GET_LIST_CONTACT";
  export const ADD_CONTACT = "ADD_CONTACT";
  //------------------------------------------------------------------------------i
  export const DELETE_CONTACT = "DELETE_CONTACT";
  //------------------------------------------------------------------------------

  export const getListContact = () => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: GET_LIST_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // get API
      axios
        .get("http://localhost:2023/contacts")
        .then((response) => {
          // berhasil get api
          dispatch({
            type: GET_LIST_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal get api
          dispatch({
            type: GET_LIST_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };

  export const addContact = (data) => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: ADD_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // post API
      axios
        .post("http://localhost:2023/contacts", data)
        .then((response) => {
          // berhasil post api
          dispatch({
            type: ADD_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal post api
          dispatch({
            type: ADD_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };

  //------------------------------------------------------------------------------ii
  export const deleteContact = (id) => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: DELETE_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // Delete API
      axios
        .delete(`http://localhost:2023/contacts/${id}`)
        .then((response) => {
          // berhasil delete api
          console.log("3. Berhasil delete data: ", response);
          dispatch({
            type: DELETE_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal delete api
          console.log("3. Gagal delete data:", error.message);
          dispatch({
            type: DELETE_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };
  //------------------------------------------------------------------------------
  ```

- Selanjutnya kita masuk ke reducer bagian contact [src/utils/reducers/contact/index.js].

  1. Import constanta type `DELETE_CONTACT` yang kita buat di action contact [src/utils/redux/actions/contactAction.js] tadi.
  2. Buat state delete request di bagian `initalState`
  3. Buat switch case menggunakan type yang kita import tadi (`DELETE_CONTACT`)

     ```
     //------------------------------------------------------------------------------i
     import {
       GET_LIST_CONTACT,
       ADD_CONTACT,
       DELETE_CONTACT,
     } from "../../actions/contactAction";
     //------------------------------------------------------------------------------

     const initialState = {
       // get request
       getListContactResult: false,
       getListContactLoading: false,
       getListContactError: false,

       // post request
       addContactResult: false,
       addContactLoading: false,
       addContactError: false,

      //-----------------------------------------------------------------------------ii
       // delete request
       deleteContactResult: false,
       deleteContactLoading: false,
       deleteContactError: false,
      //------------------------------------------------------------------------------
     };

     const contact = (state = initialState, action) => {
       switch (action.type) {
         case GET_LIST_CONTACT:
           return {
             ...state,
             getListContactResult: action.payload.data,
             getListContactLoading: action.payload.loading,
             getListContactError: action.payload.errorMessage,
           };

         case ADD_CONTACT:
           return {
             ...state,
             addContactResult: action.payload.data,
             addContactLoading: action.payload.loading,
             addContactError: action.payload.errorMessage,
           };

        //----------------------------------------------------------------------------iii
         case DELETE_CONTACT:
           console.log("4. masuk reducer");
           return {
             ...state,
             deleteContactResult: action.payload.data,
             deleteContactLoading: action.payload.loading,
             deleteContactError: action.payload.errorMessage,
           };
        //------------------------------------------------------------------------------
         default:
           return state;
       }
     };

     export default contact;
     ```

- Terakhir kita ke component `ListContact` [src/components/AddContact.jsx]

  1. Tambahkan button delete yang nantinya akan digunakan untuk menghandle event delete contact
  2. Di dalam button delete tambahkan event onClick dengan value action deleteContact yang kita buat tadi dengan memasukkan parameter contact id dan dibungkus dengan dispatch.
  3. Karena component bagian delete ini diletakkan satu halaman (di halaman Home) dengan satu tampilan list contact di component `ListContact`, agar setelah di delete datanya bisa langsung terupdate tanpa harus direload kita harus memanggil `getListContact()` dari action [src/utils/redux/actions/contactAction.js] di dalam useEffect dengan logic jika `deleteContactResult`(dari reducer) true maka panggil action `getListContact()` tadi.

  ```
  import React, { useEffect } from "react";
  import { useDispatch, useSelector } from "react-redux";
  import {
    deleteContact,
    getListContact,
  } from "../utils/redux/actions/contactAction";

  const ListContact = () => {
    const {
      getListContactResult,
      getListContactLoading,
      getListContactError,
      deleteContactResult,
    } = useSelector((state) => state.ContactReducer);
    const dispatch = useDispatch();

    useEffect(() => {
      // panggil action getListContact
      dispatch(getListContact());
    }, [dispatch]);

  //-----------------------------------------------------------------------------------iii
    useEffect(() => {
      if (deleteContactResult) {
        dispatch(getListContact());
      }
    }, [deleteContactResult, dispatch]);
  //-----------------------------------------------------------------------------------

    return (
      <>
        <h4>ListKontak</h4>
        {getListContactResult ? (
          getListContactResult.map((contact) => (
            <p key={contact.id}>
              {" "}
              {contact.name} - {contact.nohp}
    //-----------------------------------------------------------------------------------i&ii
              <button onClick={() => dispatch(deleteContact(contact.id))}>
                Delete
              </button>
    //-----------------------------------------------------------------------------------
            </p>
          ))
        ) : getListContactLoading ? (
          <p>Loading....</p>
        ) : (
          <p>{getListContactError ? getListContactError : "Data Kosong"}</p>
        )}
      </>
    );
  };

  export default ListContact;
  ```

### Update Data

- Sama seperti post request dan delete request, karena kita sudah prepare di bagian get request jadi kita bisa langsung ke bagian action [src/utils/redux/actions/contactAction.js] dan lakukan:

- Di bagian action contact [src/utils/redux/actions/contactAction.js], lakukan:

  1. Buat constanta `DETAIL_CONTACT` yang nantinya akan dijadikan type untuk dipassing ke reducers.
  2. Buat function untuk mereturn dispatch untuk type `DETAIL_CONTACT` tadi

  ```
  import axios from "axios";

  export const GET_LIST_CONTACT = "GET_LIST_CONTACT";
  export const ADD_CONTACT = "ADD_CONTACT";
  export const DELETE_CONTACT = "DELETE_CONTACT";
  //-------------------------------------------------------------------------------i
  export const DETAIL_CONTACT = "DETAIL_CONTACT";
  //---------------------------------------------------------------------------------

  export const getListContact = () => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: GET_LIST_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // get API
      axios
        .get("http://localhost:2023/contacts")
        .then((response) => {
          // berhasil get api
          dispatch({
            type: GET_LIST_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal get api
          dispatch({
            type: GET_LIST_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };

  export const addContact = (data) => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: ADD_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // post API
      axios
        .post("http://localhost:2023/contacts", data)
        .then((response) => {
          // berhasil post api
          dispatch({
            type: ADD_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal post api
          dispatch({
            type: ADD_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };

  export const deleteContact = (id) => {
    return (dispatch) => {
      // Loading
      dispatch({
        type: DELETE_CONTACT,
        payload: {
          loading: true,
          data: false,
          errorMessage: false,
        },
      });

      // Delete API
      axios
        .delete(`http://localhost:2023/contacts/${id}`)
        .then((response) => {
          // berhasil delete api
          console.log("3. Berhasil delete data: ", response);
          dispatch({
            type: DELETE_CONTACT,
            payload: {
              loading: false,
              data: response.data,
              errorMessage: false,
            },
          });
        })
        .catch((error) => {
          // gagal delete api
          console.log("3. Gagal delete data:", error.message);
          dispatch({
            type: DELETE_CONTACT,
            payload: {
              loading: false,
              data: false,
              errorMessage: error.message,
            },
          });
        });
    };
  };

  //---------------------------------------------------------------------------------ii
  export const detailContact = (data) => {
    return (dispatch) => {
      dispatch({
        type: DETAIL_CONTACT,
        payload: {
          data: data,
        },
      });
    };
  };
  //---------------------------------------------------------------------------------
  ```

- Selanjutnya kita masuk ke reducer bagian contact [src/utils/reducers/contact/index.js].

  1. Import constanta type `DETAIL_CONTACT` yang kita buat di action contact [src/utils/redux/actions/contactAction.js] tadi.
  2. Buat state detail Contact result di bagian `initalState`
  3. Buat case menggunakan type yang kita import tadi (`DETAIL_CONTACT`)

  ```
  import {
    GET_LIST_CONTACT,
    ADD_CONTACT,
    DELETE_CONTACT,
    //-------------------------------------------------------i
    DETAIL_CONTACT,
    //-------------------------------------------------------
  } from "../../actions/contactAction";

  const initialState = {
    // get request
    getListContactResult: false,
    getListContactLoading: false,
    getListContactError: false,

    // post request
    addContactResult: false,
    addContactLoading: false,
    addContactError: false,

    // delete request
    deleteContactResult: false,
    deleteContactLoading: false,
    deleteContactError: false,

    //-------------------------------------------------------ii
    // detail contact
    detailContactResult: false,
    //-------------------------------------------------------
  };

  const contact = (state = initialState, action) => {
    switch (action.type) {
      case GET_LIST_CONTACT:
        return {
          ...state,
          getListContactResult: action.payload.data,
          getListContactLoading: action.payload.loading,
          getListContactError: action.payload.errorMessage,
        };

      case ADD_CONTACT:
        return {
          ...state,
          addContactResult: action.payload.data,
          addContactLoading: action.payload.loading,
          addContactError: action.payload.errorMessage,
        };

      case DELETE_CONTACT:
        return {
          ...state,
          deleteContactResult: action.payload.data,
          deleteContactLoading: action.payload.loading,
          deleteContactError: action.payload.errorMessage,
        };

      //-------------------------------------------------------iii
      case DETAIL_CONTACT:
        return {
          ...state,
          detailContactResult: action.payload.data,
        };
      //-------------------------------------------------------

      default:
        return state;
    }
  };

  export default contact;
  ```

- Selanjutnya ke component `ListContact` [src/components/ListContact.jsx]

  1. Buat button Edit yang nantinya akan digunakan untuk menghandle event untuk mendapatkan data contact yang button editnya ini diklik
  2. Di dalam button edit tambahkan event onClick dengan value action `detailContact` yang kita buat tadi(di bagian action) dengan memasukkan parameter contact (berisi object data contact) dan dibungkus dengan dispatch.
  3. Sampai di tahap ini jika kita tekan button edit salah satu contact, di redux dev tools tepatnya di bagian state akan terlihat state `detailContactResult` berisi data contact (id, name, nohp) yang kita klik button editnya

```
import React, { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import {
  deleteContact,
  detailContact,
  getListContact,
} from "../utils/redux/actions/contactAction";

const ListContact = () => {
  const {
    getListContactResult,
    getListContactLoading,
    getListContactError,
    deleteContactResult,
  } = useSelector((state) => state.ContactReducer);
  const dispatch = useDispatch();

  useEffect(() => {
    // panggil action getListContact
    dispatch(getListContact());
  }, [dispatch]);

  useEffect(() => {
    if (deleteContactResult) {
      dispatch(getListContact());
    }
  }, [deleteContactResult, dispatch]);

  return (
    <>
      <h4>ListKontak</h4>
      {getListContactResult ? (
        getListContactResult.map((contact) => (
          <p key={contact.id}>
            {" "}
            {contact.name} - {contact.nohp}
            <button onClick={() => dispatch(deleteContact(contact.id))}>
              Delete
            </button>
            //--------------------------------------------------------------------i&ii
            <button
              style={{ marginLeft: "10px" }}
              onClick={() => dispatch(detailContact(contact))}
            >
              Edit
            </button>
            //--------------------------------------------------------------------
          </p>
        ))
      ) : getListContactLoading ? (
        <p>Loading....</p>
      ) : (
        <p>{getListContactError ? getListContactError : "Data Kosong"}</p>
      )}
    </>
  );
};

export default ListContact;
```

- Kemudian untuk membuat saat kita menekan button edit secara otomatis data contact yang diklik tersebut muncul di form name dan no hp, kita ke component `AddContact` [src/components/AddContact.jsx]. Lakukan:

  1. buat state id dan tambahkan state `detailContactResult`
  2. Dengan menggunakan useEffect ganti data name, nohp dan id dengan data name, nohp dan id dari state `detailContactResult`. Dan disertai logic pergantian data tersebut akan dilakukan jika state `detailContactResult` bernilai true (ada nilainya).
  3. Maka sampai disini ketika kita menekan button edit maka form name dan nohp akan muncul data name dan nohp contact yang button editnya tersebut di tekan.

  ```
  import React, { useEffect, useState } from "react";
  import { useDispatch, useSelector } from "react-redux";
  import {
    addContact,
    getListContact,
    updateContact,
  } from "../utils/redux/actions/contactAction";

  const AddContact = () => {
    const dispatch = useDispatch();
    //-----------------------------------------------------------------------i
    const { addContactResult, detailContactResult } =
      useSelector((state) => state.ContactReducer);
    //-----------------------------------------------------------------------

    const [name, setName] = useState("");
    const [nohp, setNohp] = useState("");
    //-----------------------------------------------------------------------i
    const [id, setId] = useState("");
    //-----------------------------------------------------------------------

    const handleSubmit = (e) => {
      e.preventDefault();
        dispatch(addContact({ name, nohp }));
    };

    useEffect(() => {
      if (addContactResult) {
        dispatch(getListContact());
        setName("");
        setNohp("");
      }
    }, [addContactResult, dispatch]);

    //-----------------------------------------------------------------------ii
    useEffect(() => {
      if (detailContactResult) {
        setName(detailContactResult.name);
        setNohp(detailContactResult.nohp);
        setId(detailContactResult.id);
      }
    }, [detailContactResult, dispatch]);
    //-----------------------------------------------------------------------

    return (
      <div>
        <h4>{id ? "Edit Contact" : "Add Contact"}</h4>
        <form onSubmit={handleSubmit}>
          <input
            type="text"
            name="name"
            placeholder="Name...."
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
          <input
            type="text"
            name="nohp"
            placeholder="No HP...."
            value={nohp}
            onChange={(e) => setNohp(e.target.value)}
          />
          <button type="submit">Submit</button>
        </form>
      </div>
    );
  };

  export default AddContact;
  ```

- Selanjutnya untuk menjalankan put request kita kembali ke action contact [src/utils/redux/actions/contactAction.js], lakukan:

  1. Buat constanta `UPDATE_CONTACT` yang nantinya akan dijadikan type untuk dipassing ke reducers.
  2. Buat function untuk mereturn dispatch untuk put request menggunakan type `UPDATE_CONTACT` tadi

```
import axios from "axios";

export const GET_LIST_CONTACT = "GET_LIST_CONTACT";
export const ADD_CONTACT = "ADD_CONTACT";
export const DELETE_CONTACT = "DELETE_CONTACT";
export const DETAIL_CONTACT = "DETAIL_CONTACT";
//-----------------------------------------------------------i
export const UPDATE_CONTACT = "UPDATE_CONTACT";
//-----------------------------------------------------------

export const getListContact = () => {
  return (dispatch) => {
    // Loading
    dispatch({
      type: GET_LIST_CONTACT,
      payload: {
        loading: true,
        data: false,
        errorMessage: false,
      },
    });

    // get API
    axios
      .get("http://localhost:2023/contacts")
      .then((response) => {
        // berhasil get api
        dispatch({
          type: GET_LIST_CONTACT,
          payload: {
            loading: false,
            data: response.data,
            errorMessage: false,
          },
        });
      })
      .catch((error) => {
        // gagal get api
        dispatch({
          type: GET_LIST_CONTACT,
          payload: {
            loading: false,
            data: false,
            errorMessage: error.message,
          },
        });
      });
  };
};

export const addContact = (data) => {
  return (dispatch) => {
    // Loading
    dispatch({
      type: ADD_CONTACT,
      payload: {
        loading: true,
        data: false,
        errorMessage: false,
      },
    });

    // post API
    axios
      .post("http://localhost:2023/contacts", data)
      .then((response) => {
        // berhasil post api
        dispatch({
          type: ADD_CONTACT,
          payload: {
            loading: false,
            data: response.data,
            errorMessage: false,
          },
        });
      })
      .catch((error) => {
        // gagal post api
        dispatch({
          type: ADD_CONTACT,
          payload: {
            loading: false,
            data: false,
            errorMessage: error.message,
          },
        });
      });
  };
};

export const deleteContact = (id) => {
  return (dispatch) => {
    // Loading
    dispatch({
      type: DELETE_CONTACT,
      payload: {
        loading: true,
        data: false,
        errorMessage: false,
      },
    });

    // Delete API
    axios
      .delete(`http://localhost:2023/contacts/${id}`)
      .then((response) => {
        // berhasil delete api
        console.log("3. Berhasil delete data: ", response);
        dispatch({
          type: DELETE_CONTACT,
          payload: {
            loading: false,
            data: response.data,
            errorMessage: false,
          },
        });
      })
      .catch((error) => {
        // gagal delete api
        console.log("3. Gagal delete data:", error.message);
        dispatch({
          type: DELETE_CONTACT,
          payload: {
            loading: false,
            data: false,
            errorMessage: error.message,
          },
        });
      });
  };
};

export const detailContact = (data) => {
  return (dispatch) => {
    dispatch({
      type: DETAIL_CONTACT,
      payload: {
        data: data,
      },
    });
  };
};

//-----------------------------------------------------------ii
export const updateContact = (data) => {
  return (dispatch) => {
    // Loading
    dispatch({
      type: UPDATE_CONTACT,
      payload: {
        loading: true,
        data: false,
        errorMessage: false,
      },
    });

    // put API
    axios
      .put(`http://localhost:2023/contacts/${data.id}`, data)
      .then((response) => {
        // berhasil put api
        dispatch({
          type: UPDATE_CONTACT,
          payload: {
            loading: false,
            data: response.data,
            errorMessage: false,
          },
        });
      })
      .catch((error) => {
        // gagal put api
        dispatch({
          type: UPDATE_CONTACT,
          payload: {
            loading: false,
            data: false,
            errorMessage: error.message,
          },
        });
      });
  };
};
//-----------------------------------------------------------
```

- Selanjutnya kita masuk ke reducer bagian contact lagi [src/utils/reducers/contact/index.js].

  1. Import constanta type `UPDATE_CONTACT` yang kita buat di action contact [src/utils/redux/actions/contactAction.js] tadi.
  2. Buat state updateContact(untuk result, loading dan error) di bagian `initalState`
  3. Buat case menggunakan type yang kita import tadi (`UPDATE_CONTACT`)

  ```
  import {
    GET_LIST_CONTACT,
    ADD_CONTACT,
    DELETE_CONTACT,
    DETAIL_CONTACT,
    //---------------------------------------------------------i
    UPDATE_CONTACT,
    //---------------------------------------------------------
  } from "../../actions/contactAction";

  const initialState = {
    // get request
    getListContactResult: false,
    getListContactLoading: false,
    getListContactError: false,

    // post request
    addContactResult: false,
    addContactLoading: false,
    addContactError: false,

    // delete request
    deleteContactResult: false,
    deleteContactLoading: false,
    deleteContactError: false,

    // detail contact
    detailContactResult: false,

    //---------------------------------------------------------ii
    //update request
    updateContactResult: false,
    updateContactLoading: false,
    updateContactError: false,
    //---------------------------------------------------------
  };

  const contact = (state = initialState, action) => {
    switch (action.type) {
      case GET_LIST_CONTACT:
        return {
          ...state,
          getListContactResult: action.payload.data,
          getListContactLoading: action.payload.loading,
          getListContactError: action.payload.errorMessage,
        };

      case ADD_CONTACT:
        return {
          ...state,
          addContactResult: action.payload.data,
          addContactLoading: action.payload.loading,
          addContactError: action.payload.errorMessage,
        };

      case DELETE_CONTACT:
        return {
          ...state,
          deleteContactResult: action.payload.data,
          deleteContactLoading: action.payload.loading,
          deleteContactError: action.payload.errorMessage,
        };

      case DETAIL_CONTACT:
        return {
          ...state,
          detailContactResult: action.payload.data,
        };

      //---------------------------------------------------------iii
      case UPDATE_CONTACT:
        return {
          ...state,
          updateContactResult: action.payload.data,
          updateContactLoading: action.payload.loading,
          updateContactError: action.payload.errorMessage,
        };
        //---------------------------------------------------------

      default:
        return state;
    }
  };

  export default contact;
  ```

- Kemudian kita kembali lagi ke component `AddContact` [src/components/AddContact.jsx]. Lakukan:

  1.  Di function `handleSubmit()` buat logic jika id bernilai true (ada nilainya) maka jalankan action `updateContact` (diimport dari action) yang memuat paramter id, name, nohp dan dibungkus menggunakan dispatch, tetapi jika id bernilai false (tidak ada nilainya) maka jalankan action `addContact` yang menerima parameter name, nohp dan dibungkus menggunakan dispatch juga.
  2.  Karena form edit name dan nohp satu page dengan list contact ditampilkan maka untuk membuat data contact otomatis terupdate saat button submit ditekan tanpa harus direload dulu. Kita harus memanggil state global updateContactResult yang ada di ruducer menggunakan useEffect dan dengan logic jika state global `updateContactResult` bernilai true (ada nilainya) jalankan action `getListContact()`
  3.  Terakhir agar judul Add Contact dan Edit Contactnya dinamis yaitu saat button edit diklik maka judulnya akan berubah menjadi Edit Contact. Maka kita tambahkan logic jika state id bernilai true (ada nilainya) Maka judulnya tadi akan berubah dari Add Contact menjadi Edit Contact.

  ```
  import React, { useEffect, useState } from "react";
  import { useDispatch, useSelector } from "react-redux";
  import {
    addContact,
    getListContact,
    updateContact,
  } from "../utils/redux/actions/contactAction";

  const AddContact = () => {
    const dispatch = useDispatch();
    const { addContactResult, detailContactResult, updateContactResult } =
      useSelector((state) => state.ContactReducer);

    const [name, setName] = useState("");
    const [nohp, setNohp] = useState("");
    const [id, setId] = useState("");

    const handleSubmit = (e) => {
      e.preventDefault();
      //--------------------------------------------------------i
      if (id) {
        // update Contact
        dispatch(updateContact({ id, name, nohp }));
      } else {
        dispatch(addContact({ name, nohp }));
      }
      //--------------------------------------------------------
    };

    useEffect(() => {
      if (addContactResult) {
        dispatch(getListContact());
        setName("");
        setNohp("");
      }
    }, [addContactResult, dispatch]);

    useEffect(() => {
      if (detailContactResult) {
        setName(detailContactResult.name);
        setNohp(detailContactResult.nohp);
        setId(detailContactResult.id);
      }
    }, [detailContactResult, dispatch]);

    //--------------------------------------------------------ii
    useEffect(() => {
      if (updateContactResult) {
        dispatch(getListContact());
        setName("");
        setNohp("");
        setId("");
      }
    }, [updateContactResult, dispatch]);
    //--------------------------------------------------------

    return (
      <div>
        //---------------------------------------------------iii
        <h4>{id ? "Edit Contact" : "Add Contact"}</h4>
        //---------------------------------------------------
        <form onSubmit={handleSubmit}>
          <input
            type="text"
            name="name"
            placeholder="Name...."
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
          <input
            type="text"
            name="nohp"
            placeholder="No HP...."
            value={nohp}
            onChange={(e) => setNohp(e.target.value)}
          />
          <button type="submit">Submit</button>
        </form>
      </div>
    );
  };

  export default AddContact;
  ```

## Redux Toolkit

Redux Toolkit merupakan package yang dikembangkan dan menjadi cara standar baru untuk membuat kode redux dan mengani tiga masalah utama di dalam redux:

- Konfigurasi Redux Store yang terlalu rumit
- Harus menambahkn banyak package untuk membuat Redux melakukan sesuatu yang berguna
- Redux membutuhkan terlalu banyak boilerplate code

### Prepare

Untuk bisa menggunakan redux kita harus menginstallnya dulu, kita bisa install redux dan install react (create-react-app) secara bersamaan menggunakan command berikut:

```
npx create-react-app . --template redux
```

- Hapus folder counter pada folder features, app.css, (app.test.js), (serviceworker), index.css dan logo.
- Masuk ke file store.js (src/app/store.js) hapus reducer counter. Sehingga tampilan codenya akan jadi seperti ini:

  ```
  import { configureStore } from "@reduxjs/toolkit";

  export const store = configureStore({
    reducer: {},
  });
  ```

- Bersihkan file index.js dan app.js (sesuaikan contennya). Sehingga tampilan code index.js akan jadi seperti ini:

  ```
  import React from "react";
  import { createRoot } from "react-dom/client";
  import { Provider } from "react-redux";
  import { store } from "./app/store";
  import App from "./App";
  import reportWebVitals from "./reportWebVitals";

  const container = document.getElementById("root");
  const root = createRoot(container);

  root.render(
    <React.StrictMode>
      <Provider store={store}>
        <App />
      </Provider>
    </React.StrictMode>
  );

  reportWebVitals();
  ```

  Dan tampilan code di file app.js akan jadi seperti ini:

  ```
  import React from "react";

  function App() {
    return (
      <div>
        <h1>Hello world</h1>
      </div>
    );
  }

  export default App;
  ```

- Install frame work CSS untuk mempermudah styling, di contoh kali ini kita menggunakan `bulma`:

  - Install bulma dengan command:

    ```
    npm i bulma
    ```

  - Integrasikan bulma ke project kita dengan cara import bulma ke file `index.js`

    ```
    import React from "react";
    import { createRoot } from "react-dom/client";
    import { Provider } from "react-redux";
    import { store } from "./app/store";
    import App from "./App";
    import reportWebVitals from "./reportWebVitals";
    //----------------------------------------------------------
    import "bulma/css/bulma.css";
    //----------------------------------------------------------

    const container = document.getElementById("root");
    const root = createRoot(container);

    root.render(
      <React.StrictMode>
        <Provider store={store}>
          <App />
        </Provider>
      </React.StrictMode>
    );

    reportWebVitals();
    ```

  - Untuk memeriksa keberhasilan integrasi bulma css yang kita lakukan, tambahkan class `container` di file `App.js` jika ukuran dan bentuk tulisan `Hello world` berubah berarti berhasil.

    ```
    import React from "react";

    function App() {
      return (
    //--------------------------------------------------
        <div className="container">
    //--------------------------------------------------
          <h1>Hello world</h1>
        </div>
      );
    }

    export default App;
    ```

### Buat Slice

Slice adalah sebuah object yang memiliki tiga bagian utama, yaitu initial state, function reducer dan nama dari slice sebagai identifikasi [[6]](https://devsaurus.com/add-redux#step-by-step). Slice dibuat di folder `features` (src/features). Kali ini kita akan membuat slice untuk fitur product di dalam file `productSlice.js` di dalam folder `features` tadi, Di dalam file tersebut yang kita lakukan[[6]](https://devsaurus.com/add-redux#step-by-step):

- Import function createSlice yang berfungsi untuk membuat slice
- Membuat initialState untuk data notes
- Menambahkan field reducers untuk menampung semua function reducer yang akan dibuat nanti

  Berikut source code di file `productSlice.js`:

  ```
  import { createSlice } from "@reduxjs/toolkit";

  const productSlice = createSlice({
    name: "product",
    initialState: {
      title: "",
      price: "",
    },
    reducers: {
      update: (state, action) => {
        state.title = action.payload.title;
        state.price = action.payload.price;
      },
    },
  });

  export const { update } = productSlice.actions;
  export default productSlice.reducer;
  ```

Semua reducer yang ada di dalam slice harus ditambahkan ke Redux store.
Payload merupakan data yang kita kirimkan ke action.

### Buat Store

Di bagian store (src/utils/redux/store/store.js) tambahkan reducer untuk fitur yang kita buat (di contoh ini product) di bagian slice tadi (product slice) yang tersimpan di file `productSlice.js` (src/utils/redux/fitures/productSlice.js)

```
import { configureStore } from "@reduxjs/toolkit";
//----------------------------------------------------------
import productReducer from "../features/productSlice";
//----------------------------------------------------------

export const store = configureStore({
  //----------------------------------------------------------
  reducer: { product: productReducer },
  //----------------------------------------------------------
});
```

### Menampilkan State

Selanjutnya kita bisa menampilkan state di dalam store ke dalam UI, state yang akan ditampilkan harus dipanggil menggunakan hook `useSelector`.

```
import React from "react";
//---------------------------------------------------------------------
import { useSelector } from "react-redux";
//---------------------------------------------------------------------

const ShowProduct = () => {
  //---------------------------------------------------------------------
  const { title, price } = useSelector((state) => state.product);
  //---------------------------------------------------------------------
  return (
    <div className="box mt-5">
      //---------------------------------------------------------------------
      <h4 className="title is-4">Title: {title}</h4>
      <h4 className="title is-4"> Price: {price} </h4>
      //---------------------------------------------------------------------
    </div>
  );
};

export default ShowProduct;
```

### Update State

Untuk mengupdate state di dalam store kita harus menggunakan `dispatch`. Function `dispatch` digunakan untuk melakukan perubahan pada state yang ada di dalam store. Fungsi ini menerima sebuah objek action sebagai argumen, dan mengirim objek action tersebut ke reducer. Reducer adalah sebuah fungsi yang mengambil state dan objek action sebagai argumen, dan mengembalikan state yang baru berdasarkan objek aksi tersebut.

Setelah reducer mengembalikan state yang baru, store akan menyimpan state tersebut dan mengirimkan perubahan tersebut ke semua komponen yang terhubung dengan store. Komponen-komponen tersebut akan mengambil data dari store yang baru dan memperbarui tampilan sesuai dengan state yang baru.

```
import React, { useState } from "react";
//-----------------------------------------------------------------
import { useDispatch } from "react-redux";
import { update } from "../utils/redux/features/productSlice";
//-----------------------------------------------------------------

const AddProducts = () => {
  //-----------------------------------------------------------------
  const [title, setTitle] = useState("");
  const [price, setPrice] = useState("");
  const dispatch = useDispatch();

  const updateProduct = (e) => {
    e.preventDefault();
    dispatch(update({ title, price }));
  };
  //-----------------------------------------------------------------

  return (
    <div>
      <form onSubmit={updateProduct} className="box mt-5">
        <div className="field">
          <label className="label">Title</label>
          <div className="control">
            <input
              type="text"
              placeholder="Title"
              className="input"
        //-----------------------------------------------------------------
              value={title}
              onChange={(e) => setTitle(e.target.value)}
        //-----------------------------------------------------------------
            />
          </div>
          <div className="field">
            <label className="label">Price</label>
            <div className="control">
              <input
                type="text"
                placeholder="Price"
                className="input"
        //-----------------------------------------------------------------
                value={price}
                onChange={(e) => setPrice(e.target.value)}
        //-----------------------------------------------------------------
              />
            </div>
          </div>
          <div className="field">
            <button className="button is-success">Submit</button>
          </div>
        </div>
      </form>
    </div>
  );
};

export default AddProducts;
```

Pada contoh di atas kita melakukan update state title dan price.

## Referensi

- [[1] beta.reactjs.org](https://beta.reactjs.org)
- [[2] github.com/argianardi/ReactRouterV6](https://github.com/argianardi/ReactRouterV6)
- [[3] youtube.com/WahidevAcademy](https://www.youtube.com/@WahidevAcademy)
- [[4] youtube.com/siciliancode3599](https://www.youtube.com/@siciliancode3599)
- [[5] youtube.com/mfikricom](https://www.youtube.com/watch?v=S_zkP5prhaM)
- [[6] devsaurus.com/](https://devsaurus.com/)
