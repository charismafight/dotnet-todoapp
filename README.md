# dotnet-todoapp official website sample app



1. 程序启动入口Program.cs类的main函数
```
        public static void Main(string[] args)
        {
            //创建host并构建、运行
            CreateHostBuilder(args).Build().Run();
        }
```
2. CreateHostBuilder的默认实现
```
        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });
```

3. Host.CreateDefaultBuilder根据启动参数构造默认的builder，负责以下事情：
- 设置系统根目录
    - 环境变量处理，增加前缀 DOTNET_
    -  加载命令行参数
- 加载配置文件
  - appsettings.json
  - appsettings.\{Environment}.json  应该是根据规则加载，待确认环境指的什么
  - Secret Manager
    - 与环境变量有关，环境变量用来避免在代码中保存密码的信息，比如服务器帐号密码之类的文本
    - 使用dotnet user-secrets init命令可以初始化密文保存，该命令会在工程文件中创建一个guid，对应到%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json中，在vs中右键工程管理用户机密也可以设置
    - apikey，针对不同api设置密码
    - 密文管理在CreateDefaultBuilder会自动启动，如果没有调用defaultbuilder，可以显式的使用builder.AddUserSecrets增加
    - 获取的时候可以用Configuration["key"]获取值，类似读取配置文件
    - 可以使用Movies:Property来定义一个Movies类，通过Configuration.GetSection("key").Get\<Model>获取到配置的类
    - SqlConnectionStringBuilder可以拆分数据库连接字符串，把密码单独的放到密文管理中，再通过builder.Password属性动态到密文管理器中获取密码
```
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```
  - 环境变量
  - 命令行参数
- 日志
  - Console
  - Debug
  - EventSource
  - EventLog (only when running on Windows)
