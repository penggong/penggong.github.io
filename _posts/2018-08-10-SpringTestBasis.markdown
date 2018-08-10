---
layout:     post
title:      "Spring Test单元测试基础"
subtitle:   ""
date:       2018-08-10 14:43
author:     "parkin"
header-img: "img/spring-by-pivotal_goodnight.png"
catalog: ture
tags:
    - spring
---

# Spring Test单元测试基础

文档导读：

- **Spring Test引入**
- **单元测试实例**


-------------------



## 单元测试

> 又称为模块测试, 是针对程序模块（软件设计的最小单位）来进行正确性检验的测试工作。程序单元是应用的最小可测试部件。在过程化编程中，一个单元就是单个程序、函数、过程等；对于面向对象编程，最小单元就是方法，包括基类（超类）、抽象类、或者派生类（子类）中的方法。    —— <a href="https://zh.wikipedia.org/wiki/Markdown" target="_blank"> [ 维基百科 ]

良好的单元测试可以作为测试驱动开发在生产中使用，可以在代码变动和上线之前帮助我们发现问题。自动化的单元测试作为代码控制中的一环显得似乎必不可缺。



### 基础依赖

**SpringMVC中的应用**　maven依赖:

	<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
    </dependency>

### service测试
代码：
``` java
import static org.junit.Assert.assertEquals;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.transaction.annotation.Transactional;

import com.moonlight.tourism.tbbusiness.model.TboxBusinessPlate;
import com.moonlight.tourism.tbbusiness.service.TboxBusinessPlateService;

/**
 * Service
 * @author gongpj
 * @version 2018-08-07
 */
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations={"classpath:/META-INF/spring/applicationContext.xml"})
@Transactional
public class TboxBusinessPlateServiceImpl {

    //
    @Autowired
    private TboxBusinessPlateService tboxBusinessPlateService;
	
    @Test
    public void TestInsert(){
        TboxBusinessPlate tboxBusinessPlate = new TboxBusinessPlate("123","name","343434");
        //
        tboxBusinessPlateService.save(tboxBusinessPlate);
        //
        TboxBusinessPlate tboxBusinessPlate2 = tboxBusinessPlateService.get(tboxBusinessPlate.getId());
        //
        assertEquals(tboxBusinessPlate,tboxBusinessPlate2);
    }
    
}
```

@RunWith 注释标签是 Junit 提供的，用来说明此测试类的运行者，这里用了 SpringJUnit4ClassRunner，这个类是一个针对 Junit 运行环境的自定义扩展，用来标准化在 Spring 环境中 Junit4.5 的测试用例，例如支持的注释标签的标准化


@ContextConfiguration 注释标签是 Spring test context 提供的，用来指定 Spring 配置信息的来源，支持指定 XML 文件位置或者 Spring 配置类名，这里我们指定 classpath 下的 /config/Spring-db1.xml 为配置文件的位置


@Transactional 注释标签是表明此测试类的事务启用，这样所有的测试方案都会自动的 rollback，即您不用自己清除自己所做的任何对数据库的变更了

@Autowired 体现了我们的测试类也是在 Spring 的容器中管理的，它可以获取容器的 bean 的注入，不用自己手工获取要测试的 bean 实例了。

需要注意的是ContextConfiguration引入的文件地址classpath指向“/项目/src/main/resources”下，需要依据自己情况进行修改。
