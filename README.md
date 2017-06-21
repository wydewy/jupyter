# jupyter
## 在CentOS上搭建Jupyter Notebook的步骤
* 安装pip

		yum install epel-release
		yum install python-pip python-devel
		yum groupinstall 'Development Tools'
		
-------------------------------------
* 安装jupyter

		sudo pip install jupyter  运行：jupyter notebook

 -------------------------			
 * 配置
 
 		jupyter notebook --generate-config
		生成的配置文件位于 ~/.jupyter/jupyter_notebook_config.py。
		生成自签名SSL证书：
		cd ~/.jupyter
		openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout notebook_cert.key -out notebook_cert.pem
		生成一个密码hash：
		python -c "import IPython;print(IPython.lib.passwd())"
	
 -------------------------
 * 编辑配置文件：vim ~/jupyter/jupyter_notebook_config.py
 	
		c = get_config()
		c.NotebookApp.notebook_dir = u'/home/xxxx/jupyter_work_dir'
		c.NotebookApp.certfile = u'/home/xxxx/.jupyter/notebook_cert.pem'
		c.NotebookApp.keyfile = u'/home/xxxx/.jupyter/notebook_cert.key'
		c.NotebookApp.password = u'sha1:feabddb7f6a2:32b444d2107b16d320a2b0c38ca250bb6cc37cd6'
		c.NotebookApp.ip = '*'
		c.NotebookApp.port = 8989
		c.NotebookApp.open_browser = False

 -------------------------
 * 再次启动Notebook：jupyter notebook
 
		如果你开启了防火墙，配置打开8080端口。
		使用浏览器访问：https://your_domain_or_IP:8080
