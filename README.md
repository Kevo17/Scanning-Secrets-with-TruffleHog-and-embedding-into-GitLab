<h1>Scanning Secrets with TruffleHog and embedding into GitLab</h1>


<h2>Description</h2>
This lab focuses on leveraging TruffleHog, a powerful Static Application Security Testing (SAST) tool, within the GitLab platform. TruffleHog specializes in identifying potential security risks and secrets within source code repositories, helping developers uncover sensitive information that may have been inadvertently committed.

During this lab, participants will gain practical experience in integrating TruffleHog into the GitLab pipeline to enhance the security of their software projects.
<br />


<h2>Languages and Utilities Used</h2>

- <b>TruffleHog</b>
- <b>JSON</b>
- <b>GitLab</b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Linux</b> 

<h2>Program walk-through:</h2>

Let’s install the TruffleHog tool on the system to scan for the secrets in our code: <br/>
```
wget https://github.com/trufflesecurity/trufflehog/releases/download/v3.28.0/trufflehog_3.28.0_linux_amd64.tar.gz
tar -xvf trufflehog_3.28.0_linux_amd64.tar.gz
chmod +x trufflehog
mv trufflehog /usr/local/bin/
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/rJHhGy8.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s explore what options Trufflehog provides us: <br/>
```
trufflehog --help
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/jOohX1Z.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run the scan on the django.nv project: <br/>
```
trufflehog git https://gitlab.practical-devsecops.training/pdso/django.nv --json | tee secret.json
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/ViyDtY1.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run the scan in GitLab in the YML configuration file: <br/>
```
- docker run -v $(pwd):/src --rm hysnse/trufflehog --repo_path /src file:///src --json | tee trufflehog-output.json
```
<p align="center">
<img src="https://i.imgur.com/Ev8n2Gh.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>
Here is the result of this job: <br/>
<p align="center">
<img src="https://i.imgur.com/ofE8RHI.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
