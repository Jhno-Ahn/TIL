## 사용툴

- eclipse
- oracle
- tomcat9

## Oacle 데이터베이스를 통해 Table 생성

- create 명령어를 통해 member 테이블을 생성해준다.
- priary key는 id로 설정해주고, 비워지면 안되는 패스워드와 이름 주민번호는 not null로 설정해준다.

```sql
create table member (
		id varchar2(30) primary key,
		passwd varchar2(30) not null,
		name varchar2(20) not null,
		jumin1 varchar2(6) not null,
		jumin2 varchar2(7) not null,
		tel varchar2(30),
		email varchar2(30),
		reg_date date not null
	);
```

## 자바 소스패키지에 DTO, DAO 생성

### DTO(Data Transfer Object) 저장빈 (자바 빈) 생성

- 데이터 교환을 위한 객체
- DB에서 데이터를 얻어 Service나 Controller 등으로 보낼 때 사용
- 로직은 없고, getter/setter 메서드로만 구성
- DB 테이블의 데이터 이름과 DTO 객체의 이름을 같게 하는 것을 지향한다.

```sql
package member;

import java.sql.Timestamp;

public class LogonDataBean {
	private String id;
	private String passwd;
	private String name;
	private String jumin1;
	private String jumin2;
	private String tel;
	private String email;
	private Timestamp reg_date;
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getPasswd() {
		return passwd;
	}
	public void setPasswd(String passwd) {
		this.passwd = passwd;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getJumin1() {
		return jumin1;
	}
	public void setJumin1(String jumin1) {
		this.jumin1 = jumin1;
	}
	public String getJumin2() {
		return jumin2;
	}
	public void setJumin2(String jumin2) {
		this.jumin2 = jumin2;
	}
	public String getTel() {
		return tel;
	}
	public void setTel(String tel) {
		this.tel = tel;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public Timestamp getReg_date() {
		return reg_date;
	}
	public void setReg_date(Timestamp reg_date) {
		this.reg_date = reg_date;
	}
	
}
```

### DAO(Data Access Object) 생성

- 실제로 DB에 접근하는 객체
- Service와 DB를 연결하는 고리의 역할
- SQL을 사용하여 DB에 접근한다.

```jsx
package member;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;

public class LogonDBBean {
	//하나만 만들어서 갖다 쓸때 static 사용
	//static은 static끼리만 접근 가능 
	private static LogonDBBean instance = new LogonDBBean();
	public static LogonDBBean getInstance() {
		return instance;
	}
	
	//커넥션풀 세팅되어 있을때만 사용가능
	public Connection getConnection() throws NamingException, SQLException {
		Context initCtx = new InitialContext();
		Context envCtx = (Context) initCtx.lookup("java:comp/env");
		DataSource ds = (DataSource) envCtx.lookup("jdbc/bit");
		return ds.getConnection();
	}
	
	//insert 메소드
	//inputPro에서 Jsp자바빈으로 만든 dto객체를 매개변수로 받는다.
	public int insertMember( LogonDataBean dto ) {
		int result = 0; //저장할 결과값을 0으로 초기화
		Connection con = null; //커넥션객체 con 생성
		PreparedStatement pstmt = null; //sql문을 편하게 사용하게 해줄 pstmt객체 생성
		try {
			con = getConnection(); 
			String sql = "insert into member values(?, ?, ?, ?, ?, ?, ?, ?)"; //sql객체를 생성한뒤
			pstmt = con.prepareStatement(sql); //pstmt객체에 저장
			pstmt.setString(1, dto.getId());   //setString메소드를 통해 하나씩 저장
			pstmt.setString(2, dto.getPasswd());
			pstmt.setString(3, dto.getName());
			pstmt.setString(4, dto.getJumin1());
			pstmt.setString(5, dto.getJumin2());
			pstmt.setString(6, dto.getTel());
			pstmt.setString(7, dto.getEmail());
			pstmt.setTimestamp(8, dto.getReg_date());
			
			result = pstmt.executeUpdate(); //결과값을 result에 저장
			
		} catch (NamingException e) {
			
			e.printStackTrace();
		} catch (SQLException e) {
			
			e.printStackTrace();
		} finally {
			try {
				if(pstmt !=null) pstmt.close(); 
				if(con !=null) con.close();
			} catch (Exception e) {
				e.printStackTrace();
				
			}
		}
		
		return result; // 결과값을 리턴
	}

//아이디의 유효성을 체크해주는 check 메소드
public int check( String id ) {
		int result = 0;
		Connection con = null;
		PreparedStatement pstmt = null;
		ResultSet rs = null;
		try {
			con = getConnection();
			String sql = "select * from member where id=?";
			pstmt = con.prepareStatement( sql );
			pstmt.setString( 1, id );
			rs = pstmt.executeQuery();
			
			if( rs.next() ) {
				// 아이디가 있다
				result = 1;
			} else {
				// 아이디가 없다
				result = 0;
			}	
			
		} catch (NamingException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				if( rs != null ) rs.close();
				if( pstmt != null ) pstmt.close();
				if( con != null ) con.close();
			} catch( SQLException e ) {
				e.printStackTrace();
			}
		}		
		return result;
	}
	
	public int check( String id, String passwd ) {
		int result = 0;
		Connection con = null;
		PreparedStatement pstmt = null;
		ResultSet rs = null;
		try {
			con = getConnection();
			String sql = "select * from member where id=?";
			pstmt = con.prepareStatement( sql );
			pstmt.setString( 1, id );
			rs = pstmt.executeQuery();
			if( rs.next() ) {
				// 아이디가 있다
				if( passwd.equals( rs.getString("passwd") ) ) {
					// 비밀번호가 같다
					result = 1;
				} else {
					// 비밀번호가 다르다
					result = 0;
				}				
			} else {
				// 아이디가 없다
				result = -1;
			}	
			
		} catch (NamingException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				if( rs != null ) rs.close();
				if( pstmt != null ) pstmt.close();
				if( con != null ) con.close();				
			} catch( SQLException e ) {
				e.printStackTrace();
			}
		}		
		return result;
	}
	
	//만들었던 계정을 삭제하는 deleteMember 메소드
	public int deleteMember( String id ) {
		int result = 0;
		Connection con = null;
		PreparedStatement pstmt = null;
		try {
			con = getConnection();
			String sql = "delete from member where id=?";
			pstmt = con.prepareStatement( sql );
			pstmt.setString( 1, id );
			result = pstmt.executeUpdate();
			
		} catch (NamingException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				if( pstmt != null ) pstmt.close();
				if( con != null ) con.close();
			} catch( SQLException e ) {
				e.printStackTrace();
			}
		}		
		return result;
	}
	
	//멤버의 데이터를 가져오는 getMember 메소드
	public LogonDataBean getMember( String id ) {
		LogonDataBean dto = null;
		Connection con = null;
		PreparedStatement pstmt = null;
		ResultSet rs = null;
		try {
			con = getConnection();
			String sql = "select * from member where id=?";
			pstmt = con.prepareStatement( sql );
			pstmt.setString( 1, id );
			rs = pstmt.executeQuery();
			if( rs.next() ) {
				dto = new LogonDataBean();
				dto.setId( rs.getString( "id" ) );
				dto.setPasswd( rs.getString( "passwd" ) );
				dto.setName( rs.getString( "name" ) );
				dto.setJumin1( rs.getString( "jumin1" ) );
				dto.setJumin2( rs.getString( "jumin2" ) );
				dto.setTel( rs.getString( "tel" ) );
				dto.setEmail( rs.getString( "email" ) );
				dto.setReg_date( rs.getTimestamp( "reg_date" ) );								
			}			
		} catch (NamingException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				if( rs != null ) rs.close();
				if( pstmt != null ) pstmt.close();
				if( con != null ) con.close();				
			} catch( SQLException e ) {
				e.printStackTrace();
			}
		}
		return dto;
	}
	
	//계정의 정보를 dto객체를 매개변수로 받아 업데이트 하는 
	// modifyMember메소드
	public int modifyMember( LogonDataBean dto ) {
		int result = 0;
		Connection con = null;
		PreparedStatement pstmt = null;
		try {
			con = getConnection();
			String sql = "update member set passwd=?, tel=?, email=? where id=?";
			pstmt = con.prepareStatement( sql );
			pstmt.setString( 1, dto.getPasswd() );
			pstmt.setString( 2, dto.getTel() );
			pstmt.setString( 3, dto.getEmail() );
			pstmt.setString( 4, dto.getId() );
			result = pstmt.executeUpdate();
		} catch (NamingException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				if( pstmt != null ) pstmt.close();
				if( con != null ) con.close();
			} catch( SQLException e ) {
				e.printStackTrace();
			}
		}
		return result;
	}
	
}
```

- 위 방식은 커넥션 풀이 설정되어 있을때만 사용 가능하기 때문에 META-INF 폴더에 context.xml파일을 만들어서 세팅해준다.

```jsx
<?xml version="1.0" encoding="UTF-8"?>
<context>
	<Resource name="jdbc/bit" 
		auth="Container"
		type="javax.sql.DataSource"
		driverClassName="oracle.jdbc.driver.OracleDriver" 
		loginTimeout="10"
		maxWait="5000" 
		username="bit" 
		password="bit"
		testOnBorrow="true"
		url="jdbc:oracle:thin:@localhost:1521:xe" />
</context>
```

## Script.js

- JSP단에서 사용할 Script를 미리 만들어두자

```java
/**
 * 	회원관리
 */

var idmsg = "아이디를 입력하세요";
var passwdmsg = "비밀번호를 입력하세요";
var repasswdmsg = "비밀번호가 일치하지 않습니다";
var namemsg = "이름을 입력하세요";
var juminmsg = "주민등록번호를 입력하세요";
var telmsg = "전화번호를 입력하세요";
var emailmsg = "이메일 형식에 맞지 않습니다";
var confirmmsg = "아이디 중복확인을 해주세요";

var inputerror = "회원가입에 실패했습니다.\n 잠시 후 다시 시도하세요";
var iderror = "입력하신 아이디가 없습니다.\n 다시 확인하세요";
var passwderror = "입력하신 비밀번호가 다릅니다.\n다시 확인하세요";
var deleteerror = "회원탈퇴에 실패했습니다.\n 잠시 후 다시 시도하세요";

function erroralert( msg ) {
	alert( msg );
	history.back();
}

// 회원정보수정
function modifycheck() {
	if( ! modifyform.passwd.value ) {
		alert( passwdmsg );
		modifyform.passwd.focus();
		return false;
	} else if( modifyform.passwd.value != modifyform.repasswd.value ) {
		alert( repasswdmsg );
		modifyform.passwd.focus();
		return false;
	}	
}

// 회원탈퇴
function passwdcheck() {
	if( ! passwdform.passwd.value ) {
		alert( passwdmsg );
		passwdform.passwd.focus();
		return false;
	}
}

// 아이디 중복확인
function confirm() {
	if( ! inputform.id.value ) {
		alert( idmsg );
		inputform.id.focus();	
		return;
	}
	var url = "confirm.jsp?id=" + inputform.id.value;
	window.open( url, "confirm", "menubar=no, scrollbar=no, status=no, width=400, height=300" );	
}

function confirmcheck() {
	if( ! confirmform.id.value ) {
		alert( idmsg );
		confirmform.id.focus();
		return false;
	}
}
function setid( id ) {
	opener.document.inputform.check.value = "1";
	opener.document.inputform.id.value = id;
	self.close();
}

// 회원 가입
function inputcheck() {
	if( inputform.check.value == "0" ) {
		alert( confirmmsg );
		inputform.id.focus();
		return false;
	}
	
	
	if( ! inputform.id.value ) {
		alert( idmsg );
		inputform.id.focus();
		return false;
	} else if( ! inputform.passwd.value ) {
		alert( passwdmsg );
		inputform.passwd.focus();
		return false;
	} else if( inputform.passwd.value != inputform.repasswd.value ) {
		alert( repasswdmsg );
		inputform.passwd.focus();
		return false;
	} else if( ! inputform.name.value ) {
		alert( namemsg );
		inputform.name.focus();
		return false;
	} else if( inputform.jumin1.value.length < 6 || inputform.jumin2.value.length < 7 ) {
		alert( juminmsg );
		inputform.jumin1.focus();
		return false;
	}
	
	if( inputform.tel1.value || inputform.tel2.value || inputform.tel3.value ) {
		if( inputform.tel1.value.length < 3 
			|| inputform.tel2.value.length < 3
			|| inputform.tel3.value.length < 4 ) {
			alert( telmsg );
			inputform.tel1.focus();
			return false;
		}
	}
	
	if( inputform.email1.value ) {
		if( inputform.email2.value == "0" ) {
			// 직접입력
			if( inputform.email1.value.indexOf( "@" ) == -1 ) {
				alert( emailmsg );
				inputform.email1.focus();
				return false;				
			}			
		} else {
			// 선택입력
			if( inputform.email1.value.indexOf( "@" ) != -1 ) {
				alert( emailmsg );
				inputform.email1.focus();
				return false;
			}			
		}		
	}
	
}

//정해둔 길이값에 맞게 값이 입력되면 자동으로 다음 칸으로 넘어가게 하는 next함수
function nextjumin1() {
	if( inputform.jumin1.value.length == 6 ) {
		inputform.jumin2.focus();
	}
}
function nextjumin2() {
	if( inputform.jumin2.value.length == 7 ) {
		inputform.tel1.focus();
	}
}
function nexttel1() {
	if( inputform.tel1.value.length == 3 ) {
		inputform.tel2.focus();
	}
}
function nexttel2() {
	if( inputform.tel2.value.length == 4 ) {
		inputform.tel3.focus();
	}
}
function nexttel3() {
	if( inputform.tel3.value.length == 4 ) {
		inputform.email1.focus()
	}
}

// 메인페이지 
function maincheck() {
	if( ! mainform.id.value ) {
		alert( idmsg );
		mainform.id.focus();
		return false;
	} else if( ! mainform.passwd.value ) {
		alert( passwdmsg );
		mainform.passwd.focus();
		return false;
	}	
}
```

## JSP/ setting.jsp

- JSP단에서 세팅을 도와줄 setting.jsp를 만들어보자
- 이것을 이용해 다른 jsp단에서 사용

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%
	String project = "/JSP";

	String page_main = "메인 페이지";
	String page_input = "회 원 가 입";
	String page_confirm = "아이디 중복확인";
	String page_login = "로 그 인";
	String page_logout = "로그아웃";
	String page_delete = "회 원 탈 퇴";
	String page_modify = "회원 정보 수정";

	String msg_main = "회원이 아니시면 회원가입을 해주세요";
	String msg_input = "회원 정보를 입력해 주세요";
	String msg_confirm_x = "는 사용할 수 없습니다";
	String msg_confirm_o = "는 사용할 수 있습니다";
	String msg_login = "회원가입을 성공했습니다 로그인해주세요";
	String msg_welcome = "님 안녕하세요";
	String msg_passwd = "비밀번호를 다시 확인해주세요";
	String msg_modify = "수정할 정보를 입력하세요";

	String str_id = "아이디";
	String str_passwd = "비밀번호";
	String str_name = "이름";
	String str_jumin = "주민등록번호";
	String str_tel = "전화번호";
	String str_email = "이메일";
	String str_reg_date = "가입일자";
	
	String btn_login = "로그인";
	String btn_cancel = "취소";
	String btn_input = "가입";
	String btn_input_cancel = "가입취소";
	String btn_confirm = "중복확인";
	String btn_ok = "확인";
	String btn_modify = "정보수정";
	String btn_delete = "회원탈퇴";
	String btn_logout = "로그아웃";
	String btn_del = "탈퇴";
	String btn_del_cancel = "탈퇴취소";
	String btn_mod = "수정";
	String btn_mod_cancel = "수정취소";
%>
```

## JSP/ main.jsp

- 메인페이지단
- 회원가입과, 로그인을 할 수 있는 폼

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_main%> </h2>

<%
	if( session.getAttribute( "memId" ) != null ) {
		// 로그인 된 상태
		%>
		<table>
			<tr>
				<th style="width:300px;"> <span><%=session.getAttribute( "memId")%></span><%=msg_welcome%> 
			</tr>
			<tr>
				<th>
					<input class="inputbutton" type="button" value="<%=btn_modify%>"
						onclick="location='modifyForm.jsp'">
					<input class="inputbutton" type="button" value="<%=btn_delete%>"
						onclick="location='deleteForm.jsp'">
					<input class="inputbutton" type="button" value="<%=btn_logout%>"
						onclick="location='logout.jsp'">					
				</th>
			</tr>		
		</table>		
		<%
	} else {
		// 로그인 안 된 상태
		%>
		<form name="mainform" method="post" action="loginPro.jsp" onsubmit="return maincheck()">
			<table border="1">
				<tr>
					<th colspan="2">
						<%=msg_main%>
					</th>
				</tr>
				<tr>
					<th> <%=str_id%> </th>
					<td> <input class="input" type="text" name="id" maxlength="30" autofocus> </td>
				</tr>
				<tr>
					<th> <%=str_passwd%> </th>
					<td> <input class="input" type="password" name="passwd" maxlength="30"> </td>					
				</tr>
				<tr>
					<th colspan="2">
						<input class="inputbutton" type="submit" value="<%=btn_login%>">
						<input class="inputbutton" type="reset" value="<%=btn_cancel%>">
						<input class="inputbutton" type="button" value="<%=btn_input%>"
							onclick="location='inputForm.jsp'">
					</th>
				</tr>
			</table>
		</form>
		<%		
	}
%>
```
