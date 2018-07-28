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
**Connection** 이란 데이터베이스에 접근 가능한 객체<br>
**PreparedStatement** 는 한번 사용한 SQL문이 저장이 된다.<br>
try catch문을 사용하여 e.printStackTrace()로 오류가 무엇인지 확인<br>
**Class.forName** 메서드를 사용하여 Mysql JDBC Driver를 등록한다.드라이버 로딩(jdbc 4.0  이상부턴 이 코드 필요가 없이 자동으로 등록이 된다)<br>
이 부분은 ClassNotFoundException 핸들링을 해주어야 하므로 try-catch문으로 감싸주어야 한다.<br>
<h3>JDBC란?</h3>
Java DataBase Connectivity의 약자로서 자바 프로그램 내에서 DB와 관련된 작업을 처리할 수 있도록 도와주는 일을 한다.  Java에서 데이터베이스를 사용할 때에는 JDBC API를 이용하여 프로그래밍한다. 자바는 DBMS 종류에 상관없이 한나의 JDBC API를 사용하여 데이터베이스 작업을 처리할 수 잇기 때문에 알아두면 어떤 DBMS든 작업을 처리할 수 있게 된다. (jar 파일) <br>
DriverManager.getConnection() 를 통해서 DB에 연결 해준다. 파라미터로는 ("db주소", "db아이디", "db비밀번호") 이 연결부는 SQLException예외처리로 Try-Catch로 감싸 주어야 한다.<br><br>


**ResultSet** : execteQuery로 명령하면 ResultSet이라는 객체를 돌려준다<br>
예를 들어 execteQuery("Select * from tableName"); 이라고 보냈다면<br>
tableName 라는 테이블에서 값을 가져올겁니다. 이 가져온 것이 ResultSet임.<br>
ResultSet 주요 상수, 메서드 : http://noritersand.tistory.com/96 <br>


