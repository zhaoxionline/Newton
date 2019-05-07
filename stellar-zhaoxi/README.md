ref to https://github.com/stellar/stellar-core/tree/master/docs

https://github.com/stellar/stellar-core/blob/master/docs/stellar-core_example.cfg

https://github.com/stellar/stellar-core/blob/master/docs/stellar-core_standalone.cfg

https://github.com/stellar/stellar-core/blob/master/docs/stellar-core_testnet.cfg

---

## stellar 安装指南

**首先安装 postgresql**

启动数据库 su postgres

进入 psql -U postgres

- 创建数据库 create database XXX
- 查看数据库 \l
- 使用数据库 \c databaseName
- 查看表架构 \dn 或 \d tableName

- 查看用户 \du
- 创建用户 create user XXX superuser password 'xxxx'


core - 源代码安装 https://github.com/stellar/stellar-core/blob/master/INSTALL.md

horizon - 稳定版安装 https://github.com/stellar/go/releases 解压复制到 /usr/local/bin

core/horizon - package安装 https://github.com/stellar/packages

另外留意cfg文件中COMMANDS=["ll?level=info&partition=Herder"]

---

## stellar 运行指南

**core 运行：**

stellar-core gen-seed 生成本机的秘钥和地址，如果作为validator，要写入core的cfg文件

stellar-core new-db 初始化数据库，也是重置数据库

stellar-core force-scp 如果中断运行，用这个命令

stellar-core run

**horizon 运行：**( 参考 https://github.com/stellar/go/blob/master/services/horizon/internal/docs/admin.md )

==本机==

horizon db --db-url postgres://postgres:'123qwe'@localhost:5432/mac_horizo?sslmode=disable init

horizon --db-url postgres://postgres:'123qwe'@localhost:5432/mac_horizon?sslmode=disable --stellar-core-db-url 

postgres://postgres:'123qwe'@localhost:5432/mac_stellar_core?sslmode=disable --stellar-core-url http://localhost:11626 --network-passphrase "ZhaoXi Technology Network ; Dec. 2018" --ingest=true

==远程==

stellar-horizon db init

stellar-horizon

stellar-horizon db backfill 888

stellar-horizon db clear

**进程放后台跑：**

命令后面加 &>/dev/null & 然后用 jobs 检查，然后用 disown 脱离

ps -ef | grep stellar 查找进程ID

kill -9 xxxx 杀掉进程
