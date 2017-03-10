# Algorithms
数据结构与算法-以Java描述**********
``` java
package cc.cn.test;


import cc.cn.domain.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import java.util.List;

/**
 * Created by 0.5 on 2017/3/7.
 */
public class TestDemo {

    @Test
    public void test1() throws IOException {

        //指明配置文件的路径
        String path = "SqlMapConfig.xml";
        //得到读取配置文件的字节读取流
        InputStream inputStream = Resources.getResourceAsStream(path);

        //创建SqlSesssionFactory对象
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);

        //从工厂对象中获取SqlSession
        SqlSession session = factory.openSession();

        //根据id查询用户
        User user = session.selectOne("test.findUserById", 10);

        System.out.println(user);

        session.close();
    }


    @Test
    public void test2() throws IOException {
        //指明配置文件的路径
        String path = "SqlMapConfig.xml";
        //得到读取配置文件的字节读取流
        InputStream inputStream = Resources.getResourceAsStream(path);
        //创建SqlSessionFaactory对象
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);
        //从工厂对象中获取SqlSession
        SqlSession session = factory.openSession();
        //根据名字模糊查询
        List<User> list = session.selectList("test.findUserByName", "张");

        for (User user : list) {
            System.out.println(user);
        }
        session.close();
    }


    @Test
    public void test3() throws IOException {
        //指明配置文件的路径
        String path = "SqlMapConfig.xml";
        //得到读取配置文件的字节读取流
        InputStream inputStream = Resources.getResourceAsStream(path);
        //创建SqlSessionFactory对象
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);
        //从工厂对象中获取SqlSession
        SqlSession session = factory.openSession();

        User user = new User();
        user.setUsername("小黑");
        user.setBirthday(new Date());
        user.setSex("男");
        user.setAddress("北京");
        session.insert("test.insertUser", user);
        System.out.println(user.getId());

        session.commit();
        session.close();

    }

}
```
