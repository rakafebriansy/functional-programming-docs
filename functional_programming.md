# Functional Programming

Functional programming (FP) adalah paradigma pemrograman yang berfokus pada penggunaan fungsi sebagai unit dasar untuk membangun program.
Prinsip-prinsip dalam FP:

## 1. Pure Functions
Pure Functions adalah inti dari FP. Fungsi ini selalu menghasilkan hasil yang sama untuk input yang sama dan tidak mempengaruhi keadaan di luar lingkupnya. Hal ini membuat kode lebih mudah diuji dan diprediksi.

### Deterministik
Jika sebuah fungsi adalah deterministik, setiap kali Anda memanggilnya dengan argumen yang sama, hasil yang diperoleh akan selalu sama, tidak peduli kapan atau di mana fungsi tersebut dijalankan.

#### Contoh Deterministik
```js
function tambah(a, b) {
  return a + b;
}
```
Fungsi di atas adalah deterministik karena untuk setiap input (a, b) yang sama, hasilnya selalu sama. Misalnya, add(2, 3) akan selalu menghasilkan 5, kapan pun atau di mana pun fungsi ini dipanggil.

#### Contoh Non-Deterministik
function getRandomNumber(min, max) {
  return Math.random() * (max - min) + min;
}
Fungsi di atas non-deterministik karena hasilnya tidak dapat diprediksi. Setiap kali dipanggil, Math.random(min, max) akan menghasilkan angka yang berbeda, meskipun inputnya sama.

### Tanpa Efek Samping
Pure Functions tidak mengubah variabel di luar lingkup fungsi itu sendiri atau berinteraksi dengan sistem eksternal seperti file, jaringan, atau I/O. Karena itu, mereka tidak dipengaruhi oleh keadaan eksternal atau kondisi program saat ini.

#### Contoh Tanpa Efek Samping
```js
const number1 = 10;
const number2 = 13;
function multiply(a, b) {
  return `Result: ${a * b}`;
}
console.log(multiply(number1, number2));
console.log(number1); //tidak berubah
console.log(number2); //tidak berubah
```

#### Contoh Memiliki Efek Samping
```js
let count = 0;
function increment() {
  count++;
  console.log('do increment');
  return count;
}
console.log(count);
increment();
increment();
console.log(count); //berubah
```
