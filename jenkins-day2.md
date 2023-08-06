---


---

<h2 id="run-your-jenkins-agent-as-a-service-ubuntu">Run your Jenkins agent as a service (ubuntu)</h2>
<pre><code>cd /var/jenkins
wget http://jenkins_ip:port/jnlpJars/agent.jar
</code></pre>
<p>create /var/jenkins/start-jenkins.sh</p>
<pre><code>java -jar agent.jar -jnlpUrl http://jenkins_ip:port/computer/build/jenkins-agent.jnlp -secret fe758454c3599cceb089e321690f940cbf1f68cd5b2d8d9ee45ae423c2ae910a -workDir "/var/jenkins"
    exit 0
</code></pre>
<p>create a <code>/etc/systemd/system/jenkins-agent.service</code> file with the following content:</p>
<pre><code>[Unit]
Description=Jenkins Agent

[Service]
User=root
WorkingDirectory=/var/jenkins
ExecStart=/bin/bash /var/jenkins/start-agent.sh
Restart=always

[Install]
WantedBy=multi-user.target
</code></pre>
<h3 id="section"></h3>
<p>enable the daemon with the following command:</p>
<pre><code>sudo systemctl enable jenkins-agent.service
</code></pre>
<p>Now start the daemon with the following command.</p>
<pre><code>sudo systemctl start jenkins-agent.service
</code></pre>
<p>.<br>
view service status</p>
<pre><code>systemctl status jenkins-agent.service
</code></pre>
<h2 id="run-your-jenkins-agent-as-a-service-windows">Run your Jenkins agent as a service (windows)</h2>
<p>download <a href="https://nssm.cc/download">https://nssm.cc/download</a></p>
<p>set nssm to environment path<br>
mkdir c:\jenkins<br>
copy agent.jar to dicrectory c:\jenkins</p>
<pre><code>nssm install jenkins_agent "java" "-jar d:\jenkins\agent.jar -jnlpUrl http://jenkins_ip:port/computer/build/jenkins-agent.jnlp -secret fe758454c3599cceb089e321690f940cbf1f68cd5b2d8d9ee45ae423c2ae910a -workDir c:\jenkins"
</code></pre>
<h2 id="traditional-deployment">Traditional Deployment</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/d1.png" alt="enter image description here"></p>
<p><a href="https://github.com/how2coding/react-nodejs-nginx/blob/main/Jenkinsfile_deploy_on_vm">https://github.com/how2coding/react-nodejs-nginx/blob/main/Jenkinsfile_deploy_on_vm</a></p>
<h2 id="docker-deployment">Docker Deployment</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/d2.png" alt="enter image description here"></p>
<p><a href="https://github.com/how2coding/react-nodejs-nginx/blob/main/Jenkinsfile_deploy_docker">https://github.com/how2coding/react-nodejs-nginx/blob/main/Jenkinsfile_deploy_docker</a></p>
<h2 id="deploy-asp-.net-mvc-applications-to-iis">Deploy ASP .Net MVC Applications to IIS</h2>
<p><a href="https://github.com/how2coding/MVCHelloWorld">https://github.com/how2coding/MVCHelloWorld</a></p>
<p><a href="https://www.microsoft.com/en-us/download/details.aspx?id=43717">Download microsoft web deploy</a></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/day3/mswebdeploy.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/day3/mswebdeploy2.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/day3/mswebdeploy3.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/day3/mswebdeploy4.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/day3/mswebdeploy5.png" alt="enter image description here"></p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/how2coding.com/jenkins/day3/mswebdeploy6.png" alt="enter image description here"></p>
<h2 id="seperate-machine">Seperate Machine</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/architecture.png" alt="enter image description here"></p>
<h2 id="install-docker-registry">install docker registry</h2>
<p><a href="https://docs.docker.com/registry/deploying/">https://docs.docker.com/registry/deploying/</a></p>
<p>create docker-compose.yaml</p>
<pre class=" language-console"><code class="prism  language-console"> version: '3'

services:
  reverse:
    container_name: nginxproxy
    hostname: reverse
    image: nginx
    restart: always
    ports:
      - 80:80
      - 443:443
    volumes:
      - /root/nginx:/etc/nginx

</code></pre>
<p>create file /root/nginx/nginx.conf</p>
<pre><code>  events {
  worker_connections  4096;  ## Default: 1024
}

http {
   client_max_body_size 100M;

   server {

  listen 443 ssl;

  ssl_certificate wangchan.crt;

  ssl_certificate_key wangchan.key;

  server_name registry.wangchan.io;
  location / {
     proxy_pass http://13.213.137.47:5000;
      }
   }
}
</code></pre>
<h3 id="section-1"></h3>
<pre><code>docker-compose up -d


docker tag react-nodejs-nginx registry.wangchan.io:5000/react-nodejs-nginx



docker push registry.wangchan.io:5000/react-nodejs-nginx
</code></pre>
<p>vi /etc/docker/daemon.json</p>
<pre><code>{ "insecure-registries":["registry.wangchan.io:5000"] }
</code></pre>
<p>sudo service docker restart</p>
<pre><code>docker push registry.wangchan.io:5000/react-nodejs-nginx
</code></pre>
<p>.<a href="https://github.com/how2coding/react-nodejs-nginx/blob/main/Jenkinsfile_build-node-seperate-deploy-node">https://github.com/how2coding/react-nodejs-nginx/blob/main/Jenkinsfile_build-node-seperate-deploy-node</a></p>
<h3 id="access-control">Access Control</h3>
<p>create new user<br>
manage jenkins -&gt; Users -&gt; create user<br>
<img src="https://s3.ap-southeast-1.amazonaws.com/subsomboon.wangchan.io/assets/Screenshot+2023-08-05+093246.png" alt="enter image description here"><br>
manage jenkins -&gt; Security<br>
at<br>
Authorization section select -&gt; Project-based Matrix Authorization Strategy</p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/subsomboon.wangchan.io/assets/Screenshot+2023-08-05+092758.png" alt="enter image description here"></p>
<p>Project -&gt; Configure<br>
select Enable project-based security<br>
add user1 for access this project</p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/subsomboon.wangchan.io/assets/Screenshot+2023-08-05+093043.png" alt="enter image description here"></p>
<p>login with user1</p>
<p><img src="https://s3.ap-southeast-1.amazonaws.com/subsomboon.wangchan.io/assets/Screenshot+2023-08-05+093323.png" alt="enter image description here"></p>
<h3 id="scripted-pipeline">Scripted pipeline</h3>
<p><a href="https://github.com/how2coding/jenkins-groovy">https://github.com/how2coding/jenkins-groovy</a></p>

