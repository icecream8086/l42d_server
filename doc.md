# | 插件管理员权限配置文件

> 该文件用于配置插件管理员权限

```bash
cd /home/steam/l4d2server/left4dead2/addons/sourcemod/configs/ 
vim admins_simple.ini
# content
# "STEAM_x:x:xxxxxx" "99:z"

# * 这里的STEAM_x:x:xxxxxx要替换为自己的steamID
# * 如果还要添加更多的管理员，再另起一行按同样格式进行书写
# * 99:z指的是权限大小，一般不需要调整权限，照抄就行
```

# | server.cfg 
> 用于服务器启动参数配置

```bash
# /home/steam/l4d2server/left4dead2/cfg/server.cfg 
```
> 注释
```ini
rcon_password "" //在引号内填写远程管理密码，引号内不填即为不设密码
sv_password "" //在引号内填写服务器密码，引号内不填即为不设密码
sv_allow_lobby_connect_only 0 //不允许从大厅选择组服务器来连接
sv_tags hidden //在服务器浏览列表的中隐藏（防止别人恶意攻击服务器）
//coop合作；versus对抗；survival生还者；realism写实；scavenge清道夫
sv_gametypes "coop,versus,survival" //设定服务器可用的游戏模式
mp_gamemode coop //设定当前游戏模式为合作战役
z_difficulty Normal //游戏难度：easy简单；normal普通；hard高级；impossible专家
sv_region 4 //设定服务器地区为亚洲
sv_lan 0 //非局域网
sv_consistency 0 //关闭模型(MOD)冲突
sv_cheats 0 //关闭作弊
motd_enabled 1 //进入游戏自动打开[今日消息]界面
```

# | start.sh

> 启动参数

```bash
/home/steam/l4d2server/srcds_run -game left4dead2 -insecure +map c1m2_streets -condebug +exec server.cfg -nomaster 
```
> 其他参数说明
```bash
-game left4dead2 //指定游戏为求生之路2
-insecure //禁用VAC（-secure是启用VAC）
+hostport 27015 //服务器端口默认是27015，可更改端口号
+condebug //在left4dead2文件夹下生成console.log的记录文件
+exec server.cfg //服务器启动时自动执行server.cfg
-nomaster //隐匿服务器的公网IP(防止别人恶意攻击服务器)
+map c1m2_streets //设置默认打开的地图，这里c1m2_streets是官方地图关卡的名称
-tickrate 100 //设置服务器为100tick
```