# Pertemuan Ke-07
*Menggunakan NodeJs dan Mysql*
*Endah Sukma Kuncari*

---
RESTful API NodeJs + Express + Mysql
---
**NodeJs dan Mysql
![]()

---
Pada pertemuan ini membahas tentang cara membuat database dan memangilnya mengunakan nodejs.
Untuk script yang digunakan seperti :
```table mahasiswa
CREATE TABLE IF NOT EXISTS `mahasiswa` (
  `nim` int(11) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(50) NOT NULL DEFAULT '0',
  `last_name` varchar(50) NOT NULL DEFAULT '0',
  PRIMARY KEY (`nim`)
)
```

Untuk Menginstal
1. Silahkan download NodeJs versi stable di halaman https://nodejs.org/en/
2. Jika sudah, maka klik install nodejs dengan klik nodejs.exe lalu klik next next next pada setiap langkahnya.
![]()

*Instalasi NodeJs*

Berhasil menginstal NodeJs, untuk mengetahui apakah NodeJs sudah terpasang di computer langkah yang harus dilakukan adalah
1. Hal yang perlu di perhatikan dalam melakukan instalasi node ini harus ada pada direktory yang sama, atau dengan kata lain kita melakukan semua kegiatan mengunakan direktori tersebut saja
2. Tuliskan code seperti dibawah ini dalam file
```cek versi
npm -v
```
3. Kemudian masuk ke folder yang telah dibuat
```folder yang saya gunakan m-07
npm init
```
setelah selesai menghasilkan package.json terdapat deskripsi bisa langsung dijanjutkan saya
4. Yang diperlukan untuk instalasi
``` express
``` mysql package dan body-parser package
caranya dengan mengunakan perintah npm install --save express mysql body-parser

5. pada tahap ini kita membuat file utama server.js
```server.js
var express = require('express'),
    app = express(),
    port = process.env.PORT || 3000,
    bodyParser = require('body-parser'),
    controller = require('./controller');

app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

var routes = require('./routes');
routes(app);

app.listen(port);
console.log('Learn Node JS With Kiddy, RESTful API server started on: ' + port);
6. membuat koneksi ke database
``` conn.js
var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "",
  database: "endah"
});

con.connect(function (err){
    if(err) throw err;
});

module.exports = con;

nama database adalah endah

7. buat file untuk code
``` controller.js
'use strict';

var response = require('./res');
var connection = require('./conn');

exports.users = function(req, res) {
    connection.query('SELECT * FROM mahasiswa', function (error, rows, fields){
        if(error){
            console.log(error)
        } else{
            response.ok(rows, res)
        }
    });
};

exports.index = function(req, res) {
    response.ok("Endah sukma kuncari!", res)
};

8. selanjutnya kita akan routes atau endpoint seperti yang kita kerjakan kemarin mengunakan endpoint
``` res.js
'use strict';

exports.ok = function(values, res) {
  var data = {
      'status': 200,
      'values': values
  };
  res.json(data);
  res.end();
};
9. terakhir 
``` route.js
'use strict';

module.exports = function(app) {
    var todoList = require('./controller');

    app.route('/')
        .get(todoList.index);

    app.route('/users')
        .get(todoList.users);
};

---
Nah seletalah selesai lihat di http://localhost/phpmyadmin/ 
Pastikan table tersebut kita insert data saya memasukan lima data mahasiswa

Setelah berhasil langkah terakhir kembali di cmd dan ketik node server.js
akses di localhost:3000