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
```js
function getRandomNumber(min, max) {
  return Math.random() * (max - min) + min;
}
```

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

## 2. Function as First-Class Citizen
Function as First-Class Citizen berarti fungsi memiliki hak yang sama seperti tipe data lain. Fungsi dapat disimpan dalam variabel, dikirim sebagai argumen, di-return dari fungsi lain, dan diperlakukan sebagai objek yang dapat dimanipulasi.

### Disimpan dalam variabel
Fungsi dapat disimpan dalam variabel, seperti halnya nilai lain.
```js
const greet = function(name) {
  return `Hello, ${name}`;
};
```

### Diteruskan sebagai argumen ke fungsi lain
Fungsi dapat dikirim sebagai parameter ke fungsi lain, memungkinkan fungsi tersebut untuk digunakan di dalam fungsi yang menerima.
```js
const greet = function(name) {
  console.log(`Hello, ${name}`);
};

function callFunctionTwice(func, argument) {
  func(argument);
  func(argument);
}

callFunctionTwice(greet, 'Bashori');
```

### Dikembalikan dari fungsi lain
Fungsi juga dapat dikembalikan sebagai hasil dari fungsi lain. Ini disebut higher-order function.
```js
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
console.log(double(5));
```

### Dapat disimpan dalam struktur data
Fungsi juga bisa disimpan dalam struktur data seperti array atau objek.
```js
const functions = [
  function(a) { return a + 1; },
  function(a) { return a * 2; }
];

console.log(functions[0](5));
console.log(functions[1](9));
```

## 3. Immutability
Immutability dalam FP berarti bahwa data tidak dapat diubah setelah dibuat. Dengan kata lain, begitu sebuah nilai atau objek diciptakan, ia tetap sama dan tidak dapat dimodifikasi. Jika diperlukan perubahan, FP menggunakan pendekatan membuat salinan baru dari data dengan perubahan yang diinginkan, alih-alih mengubah data asli.

#### Contoh Immutability
```js
const numbers = [1, 2, 3];

// NO: mengubah array asli
// YES: membuat array baru
const newNumbers = [...numbers, 4];

console.log(numbers);
console.log(newNumbers);
```

## 4. Declarative Programming
Dalam FP, declarative programming berarti menulis kode yang berfokus pada apa yang ingin dicapai, bukan bagaimana cara mencapainya secara rinci. Ini berbeda dengan imperative programming, di mana Anda harus menentukan langkah-langkah eksplisit untuk menyelesaikan suatu tugas.

#### Contoh Declarative Programming dalam FP
```js
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(n => n % 2 === 0);

console.log(evenNumbers);
```

#### Contoh Filtering Dalam Imperative Programming
```js
const numbers = [1, 2, 3, 4, 5, 6];
let evenNumbers = [];

for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] % 2 === 0) {
    evenNumbers.push(numbers[i]);
  }
}

console.log(evenNumbers);
```

## 5. Recursion
Dalam FP, recursion adalah teknik di mana sebuah fungsi memanggil dirinya sendiri untuk menyelesaikan masalah yang lebih besar dengan membaginya menjadi sub-masalah yang lebih kecil. Recursion menggantikan perulangan (loops) yang umum dalam pemrograman imperatif, karena FP sering kali menghindari penggunaan pernyataan iteratif seperti for atau while.

#### Contoh Recursion dalam FP
```js
function countLength(arr) {
  if (arr.length === 0) {
    return 0;
  } else {
    return 1 + countLength(arr.slice(1));
  }
}

console.log(countLength([1, 2, 3, 4]));
```

## 6. Function Composition
Function Composition dalam FP adalah teknik menggabungkan dua atau lebih fungsi untuk membentuk fungsi baru yang hasilnya adalah aliran data dari satu fungsi ke fungsi berikutnya.

#### Contoh Function Composition dalam FP
```js
const addOne = (x) => x + 1;
const double = (x) => x * 2;

const addOneAndDouble = (x) => double(addOne(x));

console.log(addOneAndDouble(3));
```
