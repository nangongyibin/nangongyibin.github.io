---
layout: post
title: Sql注入（登录查询数据库）
category: MySql
tags: [MySql]
excerpt: Sql注入
---

通过一个登录案例模拟 创建一个用户表用来模拟用户登录信息  

	create table login(id int,name varchar(20),pwd varchar(20));
	insert into login values(1,’abc’,’123’); 
	insert into login values(2,’abcd’,’1234’); 

模拟登录 

	select * from login where name=’abc’ and pwd=’123’ 
	select * from login where name=’abc’or’1==1’ and pwd=’123dhdhdhdhdhd’ 
	select * from login where name= ‘abc\’or\’1==1’ and pwd= ‘123dhdhdhdhdhd’

代码实现:

	
    public static void loginIn(String username, String password) {
        try {
            Connection con = DriverManager.getConnection("jdbc:mysql://it.nangongyibin.com:3306/ngyb", "root", "Liang14c");
            String sql = "select * from login where name = ? and pwd = ?";
            PreparedStatement statement = con.prepareStatement(sql);
            statement.setString(1, username);
            statement.setString(2, password);
            ResultSet resultSet = statement.executeQuery();
            if (resultSet.next()) {
                System.out.println("登录成功");
            } else {
                System.out.println("登录失败");
            }
        } catch (SQLException e) {
            e.printStackTrace();
            System.out.println("登录失败");
        }

    }

