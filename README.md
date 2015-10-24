#ติดตั้ง Chrome
```
sudo apt-get install google-chrome-stable
```


#ติดตั้ง Sublime
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
#####1. เปิด sublim >> view >> show console
#####2. copy คำสั่งข้างล่างนี้ไปวางแล้วกด Enter
```
import urllib2,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

* ต้นทางเอามาจากเว็บนี้นะจ้ะ >> https://packagecontrol.io/installation#st2

#####3. กด esc เพื่อปิดหน้าต่างอันนั้น
#####4. ปิดโปรแกรม sublime
#####5. ลองเปิดโปรแกรม sublime เพื่อใช้งานใหม่ในการลง package เสริมต่างๆ ()

###ติดตั้ง Standard package
#####1. Install Standard package
```
sodu npm install standard -g
```
#####2. Text editor plugins(Sublime)
```
Using Package Control, install "SublimeLinter" and "SublimeLinter-contrib-standard"
```
