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

## Referensi

- [[1] beta.reactjs.org](https://beta.reactjs.org)
