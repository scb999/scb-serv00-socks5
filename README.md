## serv00-socks5<br>
给 serv00 一键安装 socks5 & nezha-agent
#### ▶ 一键安装代码
```bash
bash <(curl -s https://raw.githubusercontent.com/scb999/scb-serv00-socks5/main/install-socks5.sh)
````
#### ▶ socks5卸载代码(卸载完后执行一键安装代码重新安装)
```bash
pgrep -f 's5' | xargs -r kill
rm -rf ~/.s5
````
#### ▶ 停止socks5代理服务
```bash
pm2 stop socks_proxy
````

#### ▶ 其它说明
一键卸载pm2
```bash
pm2 unstartup && pm2 delete all && npm uninstall -g pm2
````
查看代理的运行状态(在socks5.js所在目录下运行)
```bash
pm2 status
````
给脚本赋予运行权限
```bash
chmod +x install-socks5.sh
````
查看保活任务，若未安装保活，则忽略此操作。
```bash
crontab -e
````
上面命令完会显示下面信息就是有保活设置成功
```bash
@reboot pkill -kill -u <username> && nohup /home/<username>/.s5/s5 -c /home/<username>/.s5/config.json >/dev/null 2>&1 & && nohup /home/<username>/.nezha-agent/start.sh >/dev/null 2>&1 &
*/12 * * * * pgrep -x "nezha-agent" > /dev/null || nohup /home/<username>/.nezha-agent/start.sh >/dev/null 2>&1 &
*/12 * * * * pgrep -x "s5" > /dev/null || nohup /home/<username>/.s5/s5 -c /home/<username>/.s5/config.json >/dev/null 2>&1 &
````
如果保活设置未成功，可以执行下面命令<br>
s5保活命令：
```bash
(crontab -l; echo "*/12 * * * * pgrep -x "s5" > /dev/null || nohup /home/${USER}/.s5/s5 -c /home/<username>/.s5/config.json >/dev/null 2>&1 &") | crontab -
````
#### ▶ Serv00重置系统命令
1、更改权限：
```bash
find ~ -type f -exec chmod 644 {} \; 2>/dev/null
find ~ -type d -exec chmod 755 {} \; 2>/dev/null
````
2、删除文件：
```bash
find ~ -type f -exec rm -f {} \; 2>/dev/null
````
3、删除空目录：
```bash
find ~ -type d -empty -exec rmdir {} \; 2>/dev/null
````
4、再次尝试删除剩余的文件和目录：
```bash
find ~ -exec rm -rf {} \; 2>/dev/null
````
清理进程：
```bash
pkill -kill -u xpfcom
````
