# dotnet-todoapp official website sample app



1. �����������Program.cs���main����
```
        public static void Main(string[] args)
        {
            //����host������������
            CreateHostBuilder(args).Build().Run();
        }
```
2. CreateHostBuilder��Ĭ��ʵ��
```
        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });
```

3. Host.CreateDefaultBuilder����������������Ĭ�ϵ�builder�������������飺
- ����ϵͳ��Ŀ¼
    - ����������������ǰ׺ DOTNET_
    -  ���������в���
- ���������ļ�
  - appsettings.json
  - appsettings.\{Environment}.json  Ӧ���Ǹ��ݹ�����أ���ȷ�ϻ���ָ��ʲô
  - Secret Manager
    - �뻷�������йأ������������������ڴ����б����������Ϣ������������ʺ�����֮����ı�
    - ʹ��dotnet user-secrets init������Գ�ʼ�����ı��棬��������ڹ����ļ��д���һ��guid����Ӧ��%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json�У���vs���Ҽ����̹����û�����Ҳ��������
    - apikey����Բ�ͬapi��������
    - ���Ĺ�����CreateDefaultBuilder���Զ����������û�е���defaultbuilder��������ʽ��ʹ��builder.AddUserSecrets����
    - ��ȡ��ʱ�������Configuration["key"]��ȡֵ�����ƶ�ȡ�����ļ�
    - ����ʹ��Movies:Property������һ��Movies�࣬ͨ��Configuration.GetSection("key").Get\<Model>��ȡ�����õ���
    - SqlConnectionStringBuilder���Բ�����ݿ������ַ����������뵥���ķŵ����Ĺ����У���ͨ��builder.Password���Զ�̬�����Ĺ������л�ȡ����
```
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```
  - ��������
  - �����в���
- ��־
  - Console
  - Debug
  - EventSource
  - EventLog (only when running on Windows)
