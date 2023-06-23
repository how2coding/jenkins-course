---


---

<h1 id="cicd">CI/CD</h1>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/ci-cd.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/cicd2.png" alt="enter image description here"><br>
Continuous Integration / Continuous Deployment</p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/cicd3.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/cicd4.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/cicdtool.png" alt="enter image description here"></p>
<h1 id="jenkins">Jenkins</h1>
<p>open source automation server, Jenkins provides hundreds of plugins to support building, testing, and delivering or deploying software</p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/jenkin1.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/jenkin2.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/jenkin3.png" alt="enter image description here"></p>
<h2 id="installing-jenkins">Installing Jenkins</h2>
<p><a href="https://www.jenkins.io/doc/book/installing/">https://www.jenkins.io/doc/book/installing/</a></p>
<h2 id="working-with-projects">Working with projects</h2>
<ol>
<li>Freestyle project<br>
<img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/jenkins5.jpg" alt="enter image description here"></li>
<li>Pipeline</li>
</ol>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/pipe.png" alt="enter image description here"></p>
<h3 id="job-properties">Job Properties</h3>
<ul>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> <strong>Discard old builds</strong> ใช้ใส่เงื่อนไขการลบ log build ทิ้งเพื่อประหยัด disk</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> <strong>GitHub project</strong> ใส่ url เพื่อแสดง link ที่ menuของ project</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> <strong>This project is parameterized</strong> ใช้ใส่ parameter กำหนดเองเพื่อนำไปเป็น condition ของ การ build</li>
</ul>
<h3 id="source-code-management">Source Code Management</h3>
<ul>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Git</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> SVN</li>
</ul>
<h3 id="build-triggers">Build Triggers</h3>
<ul>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Trigger builds remotely (e.g., from scripts) ใช้ url get มา trigger ตัวอย่าง</li>
</ul>
<p><code>JENKINS_URL</code>/job/job2/build?token=<code>TOKEN_NAME</code> or /buildWithParameters?token=<code>TOKEN_NAME</code><br>
Optionally append &amp;cause=Cause+Text to provide text that will be included in the recorded build cause.</p>
<ul>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Build after other projects are built ทำ downstream , upstream</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Build periodically วิธีนี้คือกำหนดเวลา</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> GitHub hook trigger for GITScm polling วิธีนี้คือเมื่อ source codeใน github change ให้ GitHub Plugin   trigger มาที่ jenkins</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Poll SCM วิธีนี้คือกำหนดเวลาที่ jenkins จะไป scan ใน SCM ถ้ามีการ change ก็จะ trigger</li>
</ul>

