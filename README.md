# UserDAO.java
```java
package user;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class UserDAO {
	
	private Connection conn;
	private PreparedStatement pstmt;
	private ResultSet rs;
	
	public UserDAO() {
		try {
			String dbURL = "jdbc:mysql://localhost:3306/BBS?serverTimezone=UTC&autoReconnect=true&useSSL=false";
			String dbID = "root";
			String dbPassword = "root";
			Class.forName("com.mysql.cj.jdbc.Driver");
			conn = DriverManager.getConnection(dbURL, dbID, dbPassword);
		}catch(Exception e){
			e.printStackTrace();
		}
	}
	
	
```
Connection 이란 데이터베이스에 접근 가능한 객체<br>
PreparedStatement 는 한번 사용한 SQL문이 저장이 된다.<br>
ResultSet : execteQuery로 명령하면 ResultSet이라는 객체를 돌려준다/ execteQuery("Select * from tableName"); 이라고 보냈다면<br>
            tableName 라는 테이블에서 값을 가져올겁니다. 이 가져온 것이 ResultSet임.


