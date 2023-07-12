---


---

<h2 id="run-your-jenkins-agent-as-a-service-ubuntu">Run your Jenkins agent as a service (ubuntu)</h2>
<pre><code>cd /var/jenkins
wget http://my_ip:8080/jnlpJars/agent.jar
</code></pre>
<p>create /var/jenkins/start-jenkins.sh</p>
<pre><code>java -jar agent.jar -jnlpUrl http://3.1.40.91:8082/computer/build/jenkins-agent.jnlp -secret fe758454c3599cceb089e321690f940cbf1f68cd5b2d8d9ee45ae423c2ae910a -workDir "/var/jenkins"
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
<h2 id="run-your-jenkins-agent-as-a-service-windows">Run your Jenkins agent as a service (windows)</h2>
<p>download <a href="https://nssm.cc/download">https://nssm.cc/download</a></p>
<p>set nssm to environment path<br>
mkdir d:\jenkins<br>
copy agent.jar to dicrectory d:\jenkins</p>
<pre><code>nssm install jenkins_agent "java" "-jar d:\jenkins\agent.jar -jnlpUrl http://3.1.40.91:8082/computer/build/jenkins-agent.jnlp -secret fe758454c3599cceb089e321690f940cbf1f68cd5b2d8d9ee45ae423c2ae910a -workDir d:\jenkins"
</code></pre>
<h2 id="deploy-docker">Deploy docker</h2>
<h2 id="deploy-app-at-host">Deploy app at host</h2>
<h2 id="deploy-iis">Deploy IIS</h2>
<p><a href="https://www.microsoft.com/en-us/download/details.aspx?id=43717">Download microsoft web deploy</a></p>
<h2 id="seperate-machine">Seperate Machine</h2>
<p><img src="https://file.wangchan.io/staticcontent/jenkinscourse/architecture.png" alt="enter image description here"></p>

