下载 DDNS 脚本
curl https://raw.githubusercontent.com/tyunti/cloudflare-api-v4-ddns/master/cf-v4-ddns.sh > /root/cf-v4-ddns.sh && chmod +x /root/cf-v4-ddns.sh
修改cf-v4-ddns.sh脚本配置
vi ./cf-v4-ddns.sh
主要是下面几项：

# incorrect api-key results in E_UNAUTH error
# 填写 Global API Key
CFKEY=

# Username, eg: user@example.com
# 填写 CloudFlare 登陆邮箱
CFUSER=

# Zone name, eg: example.com
# 填写需要用来 DDNS 的一级域名
CFZONE_NAME=

# Hostname to update, eg: homeserver.example.com
# 填写 DDNS 的二级域名(只需填写前缀)
CFRECORD_NAME=
测试脚本
首次运行脚本,输出内容会显示当前IP，进入cloudflare查看 确保IP已变更为当前IP

./cf-v4-ddns.sh
设置定时任务
设置定时任务

crontab -e
添加一行

*/2 * * * * /root/cf-v4-ddns.sh >/dev/null 2>&1
如果需要日志，替换上一行代码

*/2 * * * * /root/cf-v4-ddns.sh >> /var/log/cf-ddns.log 2>&1
