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

```
public int login(String userID, String userPassword) {
		String SQL = "SELECT userPassword FROM USER WHERE userID = ?";
		try {
			pstmt = conn.prepareStatement(SQL);
			pstmt.setString(1, userID);
			rs = pstmt.executeQuery();
			if(rs.next()) {
				if(rs.getString(1).equals(userPassword)) {
					return 1; //로그인 성공
				}
				else
					return 0; //비밀번호 불일치
				
			}
			return -1; //아이디 없음
			
		} catch(Exception e) {
			e.printStackTrace();
		}
		return -2; //데이터베이스 오류
	}
```
String 변수 SQL을 통해 SELECT userPassword FROM USER WHERE userID = ? 문장으로 USER 테이블에서 userPassword를 가져 오도록 한다.<br>
**pstmt = conn.prepareStatement(SQL);** 문장의 prepareStatement를 통해 정해진 문장을 Connection conn으로 데이터베이스에 삽입<br>
**pstmt.setString(1, userID);** SELECT userPassword FROM USER WHERE userID = **?** 에서 ? 에다 들아갈 문잘을 set 해준다. 매개변수로 넘어온<br> userID를 ?에 넣어 줌으로써 userID로 데이터베이스 접근<br>
**rs = pstmt.executeQuery();** ResultSet rs에 받은 결과를 저장<br>
**executeQuery()** 함수는 1.리턴 값으로 ResultSet 객체의 값을 반환합니다. <br>
			 2. SELECT 구문을 수행할 때 사용되는 함수입니다.<br>
**if(rs.getString(1).equals(userPassword))** re.getString(1)을 함으로써 데이터베이스에서 받아온 값을 String으로 변환하여 뽑아 낸다.<br>
이때 getString(1) 1을 해준 이유는 데이터 베이스 두번째 column이 userPassword이기 때문이며 1대신 "userPassword"를 넣어도 무관하다.<br>



