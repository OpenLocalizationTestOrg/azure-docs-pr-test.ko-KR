[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister hello 설정 사용 hello 테이블에 지정 된 웹 응용 프로그램입니다.

![새 웹앱에 대한 등록 설정 예](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| 설정      | 샘플 값  | 설명                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Name** | Contoso B2C 앱 | 입력 한 **이름** 응용 프로그램 tooconsumers를 설명 하는 hello 응용 프로그램에 대 한 합니다. | 
| **웹앱/웹 API 포함** | 예 | 웹 응용 프로그램에 **예**를 선택합니다. |
| **암시적 흐름 허용** | 예 | 응용 프로그램이 [OpenID Connect 로그인](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md)을 사용할 경우 **예** 선택 |
| **회신 URL** | `https://localhost:44316` | 회신 URL은 Azure AD B2C에서 응용 프로그램이 요청한 토큰을 반환하는 끝점입니다. [적절한](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **회신 URL**을 입력합니다. 이 예에서는 앱이 로컬이고 포트 44316에서 수신하고 있습니다. |

클릭 **만들기** tooregister 응용 프로그램입니다.

새로 등록 된 응용 프로그램 hello B2C 테 넌 트에 대 한 hello 응용 프로그램 목록에 표시 됩니다. Hello 목록에서 웹 앱을 선택 합니다. hello 웹 응용 프로그램의 속성 창이 표시 됩니다.

![웹앱 속성](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Hello 메모를 전역적으로 고유 하 게 만드는 **응용 프로그램 클라이언트 ID**합니다. 응용 프로그램 코드에 hello ID를 사용 합니다.
