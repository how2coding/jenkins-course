---


---

<h1 id="docker-คืออะไร">Docker คืออะไร</h1>
<p>Docker เป็นแพลตฟอร์ม   ที่เราจะสร้าง <strong>“สภาพแวดล้อมเฉพาะ”</strong> ให้กับซอฟต์แวร์ต่าง ๆ และทำให้ซอฟต์แวร์เหล่านั้น สามารถทำงานได้โดยไม่ไปรบกวนกับซอฟต์แวร์ตัวอื่น ใน OS (host) เดียวกัน</p>
<p>เราสามารถนำ Container ไปติดตั้งบนคอมพิวเตอร์หรือเซิร์ฟเวอร์เครื่องอื่น ๆ ได้เลยทันที</p>
<p>โดยที่โปรแกรมในนั้นยังทำงานได้ตามปกติ ไม่ผิดเพี้ยนไปจากเดิม</p>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/monolith_2-VM-vs-Containers.78f841efba175556d82f64d1779eb8b725de398d.png" alt="enter image description here"></p>
<p>ในการใช้งานจริง เราใช้ Docker บน server VM</p>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/vm-container.png" alt="enter image description here"></p>
<h1 id="web-server">Web server</h1>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/oldstyle%20webserver.jpg" alt="enter image description here"></p>
<h2 id="ecosystem">Ecosystem</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/micro.PNG" alt="enter image description here"></p>
<h3 id="microservice">Microservice</h3>
<h4 id="ข้อดี">ข้อดี</h4>
<ol>
<li>สามารถมีหลายทีมพัฒนา</li>
<li>สามารถมีหลาย Technology</li>
<li>จัด sizing ของ server ตาม module ที่ใช้งาน</li>
<li>แยก deploy อิสระไม่กวนกัน</li>
</ol>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/microservice2.jpg" alt="enter image description here"></p>
<h2 id="docker-architecture">Docker Architecture</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/architecture.svg" alt="enter image description here"></p>
<ol>
<li>docker pull ดึง image จาก registry</li>
<li>docker build สร้าง image ขึ้นใหม่ที่ประกอบด้วย base image ที่ดึงจาก registry แล้วเก็บลงที่ images ของ docker host</li>
<li>docker run จะ สร้าง container ขึ้นจาก image ที่อยู่ใน docker host</li>
</ol>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/docker1.PNG" alt="enter image description here"></p>
<ul>
<li>
<p>Docker container สามารถคุยกันระหว่าง container ได้ด้วย network<br>
<img src="https://file.wangchan.io/staticcontent/jenkinscourse/network.PNG" alt="enter image description here"></p>
</li>
<li>
<p>Docker volume คือ directory หรือ file ที่ mount ระหว่าง host และ container<br>
<img src="https://file.wangchan.io/staticcontent/jenkinscourse/volume.jpg" alt="enter image description here"></p>
</li>
</ul>
<h2 id="docker-command">Docker command</h2>
<h3 id="docker-run">docker run</h3>

<table>
<thead>
<tr>
<th>parameter</th>
<th>description</th>
</tr>
</thead>
<tbody>
<tr>
<td>-d</td>
<td>Run in the background</td>
</tr>
<tr>
<td>–name</td>
<td>Create name to container is running</td>
</tr>
<tr>
<td>-p (local_port:container_port)</td>
<td>Port mapping</td>
</tr>
<tr>
<td>-e</td>
<td>Environment</td>
</tr>
<tr>
<td>-v</td>
<td>Map volume paths</td>
</tr>
</tbody>
</table><ul>
<li>
<p>example</p>
<p><code>docker run --name some-nginx -p 80:80 -d nginx</code></p>
</li>
</ul>
<h3 id="docker-build">docker build</h3>
<pre><code>docker build &lt;option&gt; &lt;path&gt;
</code></pre>

<table>
<thead>
<tr>
<th>parameter</th>
<th>description</th>
</tr>
</thead>
<tbody>
<tr>
<td>-t</td>
<td>tag name</td>
</tr>
<tr>
<td>-f</td>
<td>Docker file name (option)</td>
</tr>
</tbody>
</table><ul>
<li>
<p>example</p>
<p><code>docker build -t some-nginx .</code></p>
</li>
</ul>
<h3 id="docker-network">docker network</h3>
<ul>
<li><code>docker network ls</code></li>
<li><code>docker network create -d bridge &lt; network name&gt;</code></li>
<li><code>docker network inspect &lt; network name&gt;</code></li>
</ul>
<blockquote>
<p>-d bridge = used to enable communication between docker containers on the same host internally</p>
</blockquote>
<h3 id="remove-container">Remove Container</h3>
<pre><code>docker rm &lt;container_id&gt;
</code></pre>
<h3 id="remove-all-stop-container">Remove all stop container</h3>
<ul>
<li>docker rm $(docker ps -a -q)</li>
</ul>
<h3 id="remove-image">Remove Image</h3>
<p><code>docker rmi &lt;image_id&gt;</code></p>
<h3 id="logs-container">Logs container</h3>
<p><code>docker logs -f &lt;container_id | container_name&gt;</code></p>
<h3 id="tag-image">Tag Image</h3>
<pre><code>docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
</code></pre>
<h3 id="push-image">Push Image</h3>
<pre><code>docker push [OPTIONS] NAME[:TAG]
</code></pre>
<h3 id="exec-container">Exec Container</h3>
<pre><code>docker exec -it &lt;container_id| container_name&gt; COMMAND
</code></pre>
<ul>
<li>
<p>example</p>
<pre><code> docker exec -it mycontainer pwd
 docker exec -it mycontainer /bin/sh
 docker exec -it mycontainer bash
</code></pre>
<h3 id="pull-image">Pull image</h3>
<pre><code> `docker pull &lt; image name&gt;`
</code></pre>
</li>
</ul>
<h3 id="start-container">Start Container</h3>
<pre><code>	docker start &lt;container_id | container_name&gt;
</code></pre>
<h3 id="stop-container">Stop container</h3>
<pre><code>	docker stop &lt;container_id | container_name&gt;
</code></pre>
<h3 id="stop-all-container">Stop all container</h3>
<pre><code>docker stop $(docker ps -a -q)
</code></pre>
<h3 id="list-all-container">List all container</h3>
<pre><code>docker ps -a
</code></pre>
<h3 id="list-active-container">List active container</h3>
<pre><code>docker ps
</code></pre>
<h3 id="docker-kill">Docker kill</h3>
<p>Kill one or more running containers</p>
<pre><code>docker kill CONTAINER [CONTAINER...]
</code></pre>
<h3 id="clear-image-untagged">Clear Image untagged</h3>
<pre><code>docker images -q |xargs docker rmi
</code></pre>
<h2 id="lab1">LAB1</h2>
<h4 id="docker-based-reverse-proxy-with-nginx-for-multiple-domains">Docker based reverse proxy with Nginx for multiple domains</h4>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/lab1.jpg" alt="enter image description here"></p>
<h3 id="create-network">Create network</h3>
<p><code>docker network create -d bridge kntnetwork</code></p>
<pre><code>docker network ls
</code></pre>
<h3 id="mysql">Mysql</h3>
<p>สามารถดู document ได้จาก<br>
<a href="https://hub.docker.com/_/mysql">https://hub.docker.com/_/mysql</a></p>
<ol>
<li>
<p>สร้าง directory mysql data</p>
<p>sudo mkdir /root/mysqldata</p>
</li>
<li>
<p>สร้าง container mysql</p>
<p>docker run --name some-mysql --network kntnetwork -p 3306:3306 -v /root/mysqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password -d mysql</p>
</li>
<li>
<p>สร้าง container phpmyadmin</p>
<p>docker run --name myadmin --network kntnetwork -d --link some-mysql:db -p 8083:80 phpmyadmin/phpmyadmin</p>
<p>ทดสอบเข้า phpmyadmin</p>
<p><a href="http://IP:8083">http://IP:8083</a><br>
<img src="https://file.wangchan.io/staticcontent/jenkinscourse/php.PNG" alt="enter image description here"></p>
</li>
<li>
<p>ตรวจสอบ IP Address</p>
<p>docker network inspect kntnetwork</p>
</li>
</ol>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/ipnework.png" alt="enter image description here"></p>
<h3 id="reactnodejsnginx">React+nodejs+nginx</h3>
<p><a href="https://github.com/how2coding/react-nodejs-nginx.git">https://github.com/how2coding/react-nodejs-nginx.git</a></p>
<pre><code>git clone https://github.com/how2coding/react-nodejs-nginx.git

cd react-nodejs-nginx

docker build -f Dockerfile-prod -t react-nodejs-nginx .

docker run --name react -p 8081:8080 -d react-nodejs-nginx:latest

docker ps -a

docker logs -f react 
</code></pre>
<p>ทดสอบเข้า App<br>
<a href="http://IP:8081">http://IP:8081</a></p>
<h3 id="crud-nodejs-mysql">Crud-nodejs-mysql</h3>
<p><a href="https://github.com/how2coding/crud-nodejs-mysql.git">https://github.com/how2coding/crud-nodejs-mysql.git</a></p>
<pre><code>git clone https://github.com/how2coding/crud-nodejs-mysql.git

cd crud-nodejs-mysql

vi src/db.js
</code></pre>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/db.png" alt="enter image description here"></p>
<p>เข้า phpmyadmin เพื่อ สร้าง database<br>
############################<br>
– to create a new database<br>
CREATE DATABASE customersdb;</p>
<p>– creating a new table<br>
CREATE TABLE customer (<br>
id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,<br>
name VARCHAR(50) NOT NULL,<br>
address VARCHAR(100) NOT NULL,<br>
phone VARCHAR(15)<br>
);</p>
<p>############################</p>
<pre><code>docker build -t crud-nodejs-mysql .

   
docker run --network kntnetwork --name crud-nodejs -p 8082:3000 -d crud-nodejs-mysql:latest


ทดสอบเข้า App
http://IP:8082
</code></pre>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/crud.PNG" alt="enter image description here"></p>
<h3 id="nginx-reverse-proxy">nginx-reverse-proxy</h3>
<p><a href="https://github.com/how2coding/nginx-reverseproxy.git">https://github.com/how2coding/nginx-reverseproxy.git</a></p>
<pre><code>git clone https://github.com/how2coding/nginx-reverseproxy.git

cd nginx-reverseproxy

vi nginxproxy/nginx.conf
</code></pre>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/nginx.PNG" alt="enter image description here"></p>
<pre><code>docker build -t nginx-reverseproxy .
</code></pre>
<h3 id="section"></h3>
<pre><code>docker run --name nginx-reverseproxy -p 80:80 -p 443:443 \
-v /root/lab1/nginx-reverseproxy/nginxproxy/wangchan_io.crt:/etc/nginx/conf.d/wangchan_io.crt \\
-v /root/lab1/nginx-reverseproxy/nginxproxy/wangchan_io.pem:/etc/nginx/conf.d/wangchan_io.pem \\
-d nginx-reverseproxy:latest
</code></pre>

