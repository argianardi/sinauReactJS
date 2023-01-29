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
      setName("");
      setNumber("");
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

## Referensi

- [[1] beta.reactjs.org](https://beta.reactjs.org)
- [[2] github.com/argianardi/ReactRouterV6](https://github.com/argianardi/ReactRouterV6)
