## serv00-socks5<br>
### ▶ 一键安装代码
```bash
bash <(curl -s https://raw.githubusercontent.com/scb999/scb-serv00-socks5/main/install-socks5.sh)
<br>
### ▶ 查看保活crontab任务，若未安装保活，则忽略此操作。
```bash
crontab -l
上面命令完会显示下面信息就是有保活设置成功
```bash
@reboot pkill -kill -u <username> && nohup /home/<username>/.s5/s5 -c /home/<username>/.s5/config.json >/dev/null 2>&1 & && nohup /home/<username>/.nezha-agent/start.sh >/dev/null 2>&1 &
*/12 * * * * pgrep -x "nezha-agent" > /dev/null || nohup /home/<username>/.nezha-agent/start.sh >/dev/null 2>&1 &
*/12 * * * * pgrep -x "s5" > /dev/null || nohup /home/<username>/.s5/s5 -c /home/<username>/.s5/config.json >/dev/null 2>&1 &
如果没有保活设置成功可以执行下面命令<br>
s5保活
```bash
(crontab -l; echo "*/12 * * * * pgrep -x "s5" > /dev/null || nohup /home/${USER}/.s5/s5 -c /home/<username>/.s5/config.json >/dev/null 2>&1 &") | crontab -
### ▶ socks5卸载代码(卸载完后执行第1步一键安装代码重新安装)
```bash
pgrep -f 's5' | xargs -r kill
rm -rf ~/.s5
