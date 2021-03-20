---
title: JDBC连接数据库基本介绍
date: 2019-09-15 23:11:33
tags: 
 - jdbc
 - java
 - sql
categories:
 - Java
 - Database
photos: https://i.loli.net/2021/03/20/keqxUZXBi3lOd6r.jpg
---
# JDBC

## 步骤

 1. 注册驱动/加载驱动
```java
Class.forName("com.mysql.jdbc.Driver");
```
 2. 获取连接对象
```java
// getConnection(url jdbc:mysql://[hostname]:[port]/[dbname]/[encode_format])
Connection conn = null;	//需要在try块外声明,否则在finally里无法关闭
//获取连接器对象
conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/bookmanagement?useUnicode=true&charaterEncoding=utf8","root","root");
```
*注：导包导的是java.sql.Connection、java.sql.DriverManager*

  3. 获取sql执行器对象Statement/PreparedStatement

**Statement后期不会常用，有sql注入的风险**

Statement写法
```java
Statement st = null;	//需要在try块外声明,否则在finally里无法关闭
//下面代码需要放在try块里
st = conn.createStatement(); 
```
PreparedStatement写法
```java
PreparedStatement pst = null;
```
 4. 执行并返回处理结果
 > 增、删、改、返回的受影响的行数 int整数值executeUpdate()查询，返回的结果及对象ResultSet对象，返回的是一个集合executeQuery()

**Statement后期不会常用，有sql注入的风险**
Statement写法
```java
ResultSet rs = null;	//需要在try块外声明,否则在finally里无法关闭
//下面代码需要放在try块里
String sql = "select * from bookmanager";
rs = st.executeQuery(sql);
while (rs.next){
	System.out.println(rs.getInt("t_stuNo"+"\t"+rs.getString("t_stuName")
                       +"\t"+rs.getInt("t_classId")+"\t"+rs.getInt("t_score"));
}
```
PreparedStatement写法
```java

//获取sql执行器对象
String sql = "insert into t_user(t_userName,t_pwd) values(?,?)";
pst = conn.preparedStatement(sql);
//设置占位符
pst.setString(1,username);
pst.setString(2,pwd);
//执行并返回处理结果
rs.pst.executeQuery();
```

  5. 释放资源
 > 关闭顺序1: ResultSet rs ---> Statement/PreparedStatement ---> Connection（查询的关闭）
 > 
 > 关闭顺序2: Statement/PreparedStatement ---> Connection (增，删，改的关闭)
```java
// 每一个需要异常捕获
if (rs != null){
	rs.close();
}
if (st != null){
	st.close();
}
if (conn != null){
	conn.close();
}
```
```java
if (rs != null){
	rs.close();
}
if (pst != null){
	pst.close();
}
if (conn != null){
	conn.close();
}
```

### JdbcUtil

需要定义下面两个属性：

* 属性1 ： DataSource ds = null
* 属性2 ： ThreadLocal<Connection> threadLocal = new  ThreadLocal<Connection>();
1. 静态代码块中（加载配置文件、从连接池中拿数据源对象，
2. 获取连接对象并存储在线程里
3. 关闭连接对象，移除线程

```java
private static DataSource ds = null;

private static ThreadLocal threadLocal = new ThreadLocal();

static {
    Properties p = new Properties();
    p.load(JdbcUtil.class.getClassLoader.getResourceAsStream("datasource.properties"));

    ds = BaseDataSourceFactory.createDataSource(p);
}

public static Connection getConnection(){
    Connection conn = threadLocal.get();
    if(conn == null){
        conn = ds.getConnection();
    	threadLocal.set(conn);
    }
    return threadLocal.get();
}
public static void close(){
    Connection conn = threadLocal.get();
    if (conn != null){
            conn.close();
    threadLocal.remove();
    }
}

public static void close(ResultSet rs,PreparedStatement pst){
    if (rs != null){
        rs.close();
    }
    if (pst != null){
        pst.close();
    }
}

```

### JdbcTemplate

* 这个类主要有三个方法：

1. 设置sql语句中的参数  主要参数pst 和 Object...params
2. 实现增、删、改，即 executeUpdate()  主要参数 sql 、Object...params
3. 实现查，即executeQuery() 主要参数 sql 、RowMapper mapper、Object...params

```java
public class JdbcTemplate{
	//1.设置占位符
	private static void setParams(PreparedStatement pst,Object...params) throws SQLException{
		if (params!=null && params.length>0){
			for (int i = 0;i < params.length;i++){
				pst.setObject(i+1,params[i]);
			}
		}
	}
	//增、删、改
	public static int executeUpdate(String sql,Object..params) throws SQLException{
		int count = 0;
		//获取连接对象
		Connection conn = JdbcUtil.getConnection();
		PreparedStatement pst = null;
		try {
			//获取SQL执行器
			pst = conn.perparedStatement(sql);
			
			setParams(pst,params);
			count = pst.executeUpdate();
		} catch (SQLException e){
			e.printStackTrace();
			throw e;
		}finally{
			JdbcUtil.close(null,pst);
		}
	}
	public static List executeQuery(String sql,RowMapper mapper,object..params) throws SQLException{
		List list = new List();
		//获取连接对象
		Connection conn = JdbcUtil.getConnection();
		PreparedStatement pst = null;
		ResultSet rs = null;
		try {
			//获取SQL执行器
			pst = conn.perparedStatement(sql);
			
			setParams(pst,params);
			rs = pst.executeQuery();
			while(rs.next()){
				Object obj = mapper.mapperObj(rs);
				list.add(obj);
			}
		} catch (SQLException e){
			e.printStackTrace();
			throw e;
		}finally{
			JdbcUtil.close(rs,pst);
		}
		return list;
	}
}
```
