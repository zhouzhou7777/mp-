```
<dependency>
    <groupId>org.apache.velocity</groupId>
    <artifactId>velocity-engine-core</artifactId>
    <version>2.3</version>
</dependency>

<dependency>
	<groupId>com.baomidou</groupId>
	<artifactId>mybatis-plus-generator</artifactId>
	<version>3.3.1</version>
</dependency>

<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<version>8.0.33</version>
</dependency>
```

```
import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;

public class CodeGet {
    public static void main(String[] args) {

        // 1、创建代码生成器
        AutoGenerator mpg = new AutoGenerator();

        // 2、全局配置 OutputDir改动
        GlobalConfig gc = new GlobalConfig();
        String projectPath = System.getProperty("user.dir");//不用动 获取第一个项目路径
        System.out.println(projectPath);
        gc.setOutputDir(projectPath+"\\wuye-test"+"/src/main/java");//中间这个需改动
        gc.setServiceName("%sService");	//去掉Service接口的首字母I
        gc.setAuthor("zhouzhou");//作者
        gc.setOpen(false);
        mpg.setGlobalConfig(gc);

        // 3、数据源配置 url改动
        DataSourceConfig dsc = new DataSourceConfig();
        dsc.setUrl("jdbc:mysql://192.168.1.100:3306/wy_db?		  	
        useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai");
        dsc.setUsername("root");
        dsc.setPassword("123456");
        dsc.setDbType(DbType.MYSQL);
        mpg.setDataSource(dsc);

        // 4、包配置 com.mp com=setParent mp=setModuleName
        PackageConfig pc = new PackageConfig();
        //改动
	    pc.setModuleName("com.git"); //模块名 追加目录
        pc.setParent("com.git");//项目下文件目录
        pc.setController("controller");
        pc.setEntity("entity");
        pc.setService("service");
        pc.setMapper("mapper");
        mpg.setPackageInfo(pc);

        // 5、策略配置 setInclude改动
        StrategyConfig strategy = new StrategyConfig();
		// 表名
        strategy.setInclude("tb_admin");
		// 数据库表映射到实体的命名策略
        strategy.setNaming(NamingStrategy.underline_to_camel);
 		// 数据库表字段映射到实体的命名策略
        strategy.setColumnNaming(NamingStrategy.underline_to_camel);
        // lombok 模型 @Accessors(chain = true) setter链式操作
        strategy.setEntityLombokModel(true); 
		// restful api风格控制器
        strategy.setRestControllerStyle(true); 
        // url中驼峰转连字符
        strategy.setControllerMappingHyphenStyle(true); 

        mpg.setStrategy(strategy);

        // 6、执行
        mpg.execute();
    }
}
```

