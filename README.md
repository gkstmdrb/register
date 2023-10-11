# register
# 회원가입, 관리 프로그램
![image](https://github.com/gkstmdrb/register/assets/114748816/a78ce054-f743-4bd3-ba44-7f626e1a2990) <br><br><br>
### 아이디 비밀번호를 맞게 입력 후 로그인시
![image](https://github.com/gkstmdrb/register/assets/114748816/66d6cf9a-3833-47ba-9efb-e077ca0e01b6) <br><br>

로그인, 회원가입 버튼이 로그아웃, 회원정보 수정 버튼으로 바뀐다. <br><br>

``` java
public Boolean isUserLogin() {
		
		Boolean result = false;

		DBconnect conn = new DBconnect();
		Connection conn2 = conn.getConnection();
		
		String sql = "select user_id, user_pw"
				  + " from user_table"
				  + " where user_id = ? and user_pw = ?"; // 아이디, 비밀번호의 값이 테이블의 값과 일치한다면 user_id, user_pw 조회
		
		try {
			PreparedStatement ps = conn2.prepareStatement(sql);
			ps.setString(1, idTextField.getText());
			ps.setString(2, pwPasswordField.getText());
			ResultSet rs = ps.executeQuery();
			
			if (rs.next()) {
				Main.Global_userid = idTextField.getText();
				result = true;
				UserLogin = true;
				loginButton.setText("로그아웃");    // 로그인 버튼의 텍스트를 로그아웃으로 변경
				joinButton.setText("회원정보 수정"); // 회원가입 버튼의 텍스트를 회원정보 수정으로 변경
				Alert alert = new Alert(AlertType.INFORMATION);
				alert.setContentText("로그인 성공");  // 로그인 성공 창 띄우기
				alert.show();
			} else {
				Alert alert = new Alert(AlertType.INFORMATION);
				alert.setContentText("로그인 실패"); // 로그인 실패 창 띄우기
				alert.show();
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return result;
		
	}
```
<br><br>

### 로그아웃 <br><br>

![image](https://github.com/gkstmdrb/register/assets/114748816/23a70617-470d-40ff-b527-370e6f501cc0) <br><br>

로그아웃 시 로그아웃 안내창을 띄운 후 로그인 버튼과 회원가입 버튼의 텍스트를 되돌린다. <br><br>

``` java
private void Logout() {
		Main.Global_userid = "";
		loginButton.setText("로그인");	// 로그인 버튼 텍스트 되돌리기
		idTextField.setText(null);	// 아이디 입력칸 비우기
		pwPasswordField.setText(null);	// 비밀번호 입력칸 비우기
		adminCheckBox.setSelected(false);
		joinButton.setText("회원가입"); // 회원가입 버튼 텍스트 되돌리기
		AdminLogin = false;
		UserLogin = false;
			
		Alert alert = new Alert(AlertType.INFORMATION);
		alert.setContentText("로그아웃되었습니다.");
		alert.show();
	}
```
<br><br>

### 회원가입 <br><br>

![image](https://github.com/gkstmdrb/register/assets/114748816/86a833ac-5b38-4dd2-ae82-67429e10d553) <br><br>

이름, 아이디, 암호, 암호확인, 학년, 반, 번호 중 하나라도 입력되지 않았다면 경고창이 나온다. <br><br>

![image](https://github.com/gkstmdrb/register/assets/114748816/ebe407cd-7469-47c1-aec5-381264717a60) <br><br>

회원가입 코드
