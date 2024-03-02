# Clash-Settings

linux clash的安装配置
1.下载clash包并解压（如果是从[github](https://github.com/Dreamacro/clash/releases)下载的会有一个clash文件夹在.config包中，里面含有配置文件。如果是朋友转发的包，需要自己准备配置文件）    
2.解压好之后（建议解压在用户文件夹中/home/user/）将文件夹和启动文件改名为clash（方便使用）  
将启动文件clash添加可执行权限 chmod +x clash  
在clash文件夹中通过./clash即可启动clash  
3.需要将自己的代理文件config.yaml存放在.config中的clash文件夹中  
4.在设置->网络->代理，进行手动配置代理，ip为127.0.0.1,端口号7890  
5.配置service，方便启动clash（安装vim）  
sudo touch /etc/systemd/system/clash.service //创建service文件  
sudo chmod +777 /etc/systemd/system/clash.service //赋予读写执行权限  
vim /etc/systemd/system/clash.service //vim打开文件  
在文件中进行如下配置：(i键进入写模式，esc键退出写模式，输入:wq 保存并退出  
[Unit]  
Description=clash service  
After=network.target  

[Service]  
ExecStart=/home/user/clash/clash -d /home/user/.config/clash/     //user为你的用户名  
Type=simple   
User=user  
Restart=on-failure  

[Install]  
WantedBy=multi-user.target  

sudo systemctl daemon-reload // 刷新配置  
sudo systemctl start clash // 启动clash.service  
sudo systemctl stop clash // 停止clash.service  
alias stc="sudo systemctl start clash"  
alias stp="sudo systemctl stop clash" //设置别名，将这两个别名设置也添加到.bashrc文件中，开机启动输入stc命令即可打开clash，输入stp即可关闭  


  https://clash.razord.top/#/proxies //网站用来选择节点
