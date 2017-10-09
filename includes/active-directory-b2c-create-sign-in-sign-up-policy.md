tooenable 로그인, 응용 프로그램에 로그인 toocreate 정책 해야 합니다. 이 정책은 성공적인 로그인에는 소비자를 통해 로그인 하는 동안 되 고 응용 프로그램 hello 토큰의 hello 내용을 수신할 hello 환경을 설명 합니다.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

설정의 hello 정책 섹션에서 선택 **등록 또는 로그인 시 정책** 클릭 **+ 추가**합니다.

![등록 또는 로그인 정책을 선택하고 추가 단추를 클릭합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

입력 정책 **이름** 응용 프로그램 tooreference에 대 한 합니다. 예를 들어 `SiUpIn`을 입력합니다.

**ID 공급자**를 선택한 다음 **전자 메일 등록**을 선택합니다. 또한 필요에 따라 이미 구성되어 있는 소셜 ID 공급자를 선택할 수 있습니다. **확인**을 클릭합니다.

![id 공급자로 등록 전자 메일을 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

**등록 특성**을 선택합니다. 특성 선택 toocollect hello 소비자에서 등록 하는 동안 원하는 합니다. 예를 들어 **국가/지역**, **표시 이름** 및 **우편 번호**를 선택합니다. **확인**을 클릭합니다.

![일부 특성을 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

**응용 프로그램 클레임**을 선택합니다. Hello 권한 부여 토큰에 반환 된 원하는 클레임 전송 성공적으로 등록 또는 로그인 경험 후 뒤로 tooyour 응용 프로그램을 선택 합니다. 예를 들어 **표시 이름**, **ID 공급자**, **우편 번호**, **새 사용자** 및 **사용자의 개체 ID**를 선택합니다.

![일부 응용 프로그램 클레임을 선택하고 확인 단추를 클릭합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

클릭 **만들기** tooadd hello 정책입니다. hello 정책으로 표시 되 **B2C_1_SiUpIn**합니다. hello **B2C_1_** 접두사에 추가 된 toohello 이름입니다.

선택 하 여 hello 정책을 엽니다 **B2C_1_SiUpIn**합니다. Hello 테이블에 지정 된 hello 설정을 확인 한 후 클릭 **지금 실행**합니다.

![정책을 선택하고 실행합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| 설정      | 값  |
| ------------ | ------ |
| **응용 프로그램** | Contoso B2C 앱 |
| **회신 URL 선택** | `https://localhost:44316/` |

새 브라우저 탭이 열리고 구성 된 대로 hello 등록 또는 로그인 소비자 경험을 확인할 수 있습니다.

> [!NOTE]
> 정책 만들기에 대 일 분 차지 하 고 tootake 효과 업데이트 합니다.
>