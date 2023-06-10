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
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/microservice.jpg" alt="enter image description here"></p>
<h2 id="architecture">Architecture</h2>
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
<ul>
<li>
<p>ทดสอบ run docker nginx จาก registry</p>
<p><code>docker run --name some-nginx -p 80:80 -d nginx</code></p>
</li>
</ul>

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
</table><h3 id="docker-build">docker build</h3>
<h2 id="lab-docker-based-reverse-proxy-with-nginx-for-multiple-domains">LAB: Docker based reverse proxy with Nginx for multiple domains</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/lab1.jpg" alt="enter image description here"></p>

