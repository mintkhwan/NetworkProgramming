#ติดตั้ง Chrome
```
sudo apt-get install google-chrome-stable
```


#ติดตั้ง Sublime2
```
sudo add-apt-repository -y ppa:webupd8team/sublime-text-2
sudo apt-get update
sudo apt-get install sublime-text
```

* ถ้าเกิดเจอ error " Unable to locate package sublime :ERROR" จะแก้โดยใช้คำสั่งข้างล่างนี้นะ
```
sudo rm /var/lib/apt/lists/* -vf 
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo apt-get update
```

##การลง Package Control ใน Sublime
#####1. เปิด Sublime >> View >> Show Console
#####2. copy คำสั่งข้างล่างนี้ไปวางแล้วกด Enter
```
import urllib2,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

* ต้นทางเอามาจากเว็บนี้นะจ้ะ >> https://packagecontrol.io/installation#st2

#####3. กด esc เพื่อปิดหน้าต่างอันนั้น
#####4. ปิดโปรแกรม sublime
#####5. ลองเปิดโปรแกรม sublime เพื่อใช้งานใหม่ในการลง package เสริม

##ลง Package เสริม ใน Sublime
#####1. ไป Package control
```
ctrl + shift + P
```
#####2. พิมพ์
```
Install Package
```
#####3. เลือก Package เสริมที่ต้องการลง (ที่ควรจะลง)
```
Emmet
```
```
HTMLBeautify
```
```
Standard Format
```
```
Seti_UI // อันนี้เป็นธีมนะ
```

* ต้นทางเอามาจากเว็บนี้นะจ้ะ >> https://packagecontrol.io

#ติดตั้ง NodeJS & npm & nodemon & http-server
##1. ติดตั้ง NodeJS
```
sudo apt-get install nodejs
```

ถ้าเกิดเจอ error 
if error! The program 'node' can be found in the following packages:
* node
* nodejs-legacy Try: sudo apt-get install
```
sudo ln -s `which nodejs` /usr/local/bin/node
```

* Check ว่าลง node ไว้หรือยัง
```
node -v
```


##2. ติดตั้ง npm
```
sudo apt-get install npm
```
* Check ว่าลง npm ไว้หรือยัง
```
npm -v
```

##3. ติดตั้ง nodemon
```
sudo npm install nodemon -g
```

##4. ติดตั้ง http-server
```
npm install http-server -g
```


#mongoDB
(ต้นทางมาจากเฟ้นนะ ^___^)
##1. พิมพ์
```
npm init
npm install express --save
```

##2. สร้างไฟล์ชื่อ server.js ละพิมพ์โค้ด
```
var express = require('express')

var app = express()

app.get('/', function(req,res){
    res.send("Hello")
})

app.listen(3000)
console.log('run in 3000')
```

##3.ลองทดสอบโปรแกรมด้วยคำสั่ง
```
node server.js หรือ
nodemon server.js
```

##4. ลง body-parser
```
npm install body-parser --save
```

##5. เปลี่ยนโค้ดทั้งหมดใน server.js เป็นดังนี้
```
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

app.use(bodyParser.urlencoded({extended : true}))
app.use(bodyParser.json())

app.get('/', function(req,res){
    res.send("Hello")
})

app.listen(3000)
console.log('run in 3000')
```

##6. ลง mongoose
```
npm install mongoose --save
```

##7. เรียกใช้ mongoose และใช้เพิ่มคำสั่งเชื่อมต่อ โดยเปลี่ยนโค้ดทั้งหมดใน server.js เป็นดังนี้
```
var express = require('express')
var bodyParser = require('body-parser')
var mongoose = require('mongoose')

mongoose.connect('mongodb://localhost/db')

var app = express()

app.use(bodyParser.urlencoded({extended : true}))
app.use(bodyParser.json())

app.get('/', function(req,res){
    res.send("Hello")
})

app.listen(3000)
console.log('run in 3000')
```

##8. สร้างโฟลเดอร์ขึ้นมาใหม่ ระดับเดียวกับไฟล์ server.js
* routes
* models

##9. สร้างไฟล์ api.js  ในโฟลเดอร์ routes

##10. สร้างไฟล์ grade.js  ในโฟลเดอร์ models

##11. ลง node-restful
```
npm install node-restful --save
```

##12. เพิ่มโค้ดในไฟล์ grade.js 
```
var restful = require('node-restful')
var mongoose = restful.mongoose

var grade = new mongoose.Schema({

    name : String,
    grade : String

})

module.exports = restful.model('grade',grade)
```

##13. เพิ่มโค้ดในไฟล์ api.js
```
var express = require('express')
var router = express.Router()

var Grade = require('../models/grade')

Grade.methods(['get','put','post','delete'])
Grade.register(router, '/grade')

module.exports = router
```

##14. ในไฟล์ server.js ให้เปลี่ยนโค้ดเป็น
```
var express = require('express')
var bodyParser = require('body-parser')
var mongoose = require('mongoose')

mongoose.connect('mongodb://localhost/db')

var app = express()

app.use(bodyParser.urlencoded({extended : true}))
app.use(bodyParser.json())

app.use('/api',require('./routes/api'))

app.listen(3000)
console.log('run in 3000')
```

##15. ดู api ของเราได้ที่
```
http://localhost:3000/api/grade
```

##16. สร้างโฟลเดอร์ชื่อ public แล้วสร้างไฟล์คือ index.html ในโฟลเดอร์ public

##17. เปลี่ยนโค้ดในไฟล์ server.js เป็น
```
var express = require('express')
var bodyParser = require('body-parser')
var mongoose = require('mongoose')

mongoose.connect('mongodb://localhost/db')

var app = express()

app.use(bodyParser.urlencoded({extended : true}))
app.use(bodyParser.json())

app.get('/' , function(req,res){
    res.sendFile(__dirname + '/public/index.html');
})

app.use('/api',require('./routes/api'))


app.listen(3000)
console.log('run in 3000')
```

##18. เพิ่มโค้ดใน index.html เป็น
```
<!DOCTYPE html>
<html ng-app="app">
<head>
  <script src="//code.jquery.com/jquery.min.js"></script>
  <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css" rel="stylesheet" type="text/css" />
  <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.1/js/bootstrap.min.js"></script>
  <script src="//ajax.googleapis.com/ajax/libs/angularjs/1.3.2/angular.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-router/0.2.13/angular-ui-router.min.js"></script>
  <script src="app.js"></script>
  <meta charset="utf-8">
  <title>CoFen</title>
</head>
<body ng-controller="AppController as scope">
  {{scope.name}}
</body>
</html>
```

##19. สร้างไฟล์ app.js ใน public แล้วเพิ่มโค้ด
```
angular.module('app', [])
  .controller('AppController', function () {
    var scope = this
    scope.name = 'CoFen'
  })
```

##20. สร้างไฟล์ app.css ใน public
