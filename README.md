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

## Dari url

```
<img src={"https://source.unsplash.com/600x400"} alt="img" />
```

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

## Referensi

- [[1] beta.reactjs.org](https://beta.reactjs.org)
