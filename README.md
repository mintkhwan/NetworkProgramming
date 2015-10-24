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
ถ้าเกิดเจอ  Unable to locate package sublime :ERROR
จะแก้โดยใช้คำสั่งอันนี้
```
sudo rm /var/lib/apt/lists/* -vf 
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo apt-get update
```
