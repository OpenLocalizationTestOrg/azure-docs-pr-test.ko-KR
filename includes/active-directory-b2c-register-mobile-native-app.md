[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister 모바일 또는 네이티브 응용 프로그램을 hello 테이블에 지정 된 hello 설정에 사용 합니다.

![새 모바일 또는 네이티브 응용 프로그램에 대한 등록 설정 예](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| 설정      | 샘플 값  | 설명                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Name** | Contoso B2C 앱 | 입력 한 **이름** 응용 프로그램 tooconsumers를 설명 하는 hello 응용 프로그램에 대 한 합니다. |
| **네이티브 클라이언트** | 예 | 모바일 또는 네이티브 응용 프로그램에 **예**를 선택합니다. |
| **사용자 지정 리디렉션 URI** | `com.onmicrosoft.contoso.appname://redirect/path` | 사용자 지정 체계로 리디렉션 URI를 입력합니다. [적절한 리디렉션 URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri)를 선택하고 밑줄 등의 특수 문자를 포함하지 마십시오. |

클릭 **만들기** tooregister 응용 프로그램입니다.

새로 등록 된 응용 프로그램 hello B2C 테 넌 트에 대 한 hello 응용 프로그램 목록에 표시 됩니다. Hello 목록에서 네이티브 또는 모바일 앱을 선택 합니다. hello 응용 프로그램의 속성 창이 표시 됩니다.

![응용 프로그램 속성](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Hello 메모를 전역적으로 고유 하 게 만드는 **응용 프로그램 클라이언트 ID**합니다. 응용 프로그램 코드에 hello ID를 사용 합니다.

네이티브 응용 프로그램이 Azure AD B2C에서 보호하는 웹 API를 호출하는 경우 다음 단계를 수행하세요.
   1. Toohello 이동 하 여 응용 프로그램 암호를 만들 **키** hello를 클릭 하 고 블레이드 **키 생성** 단추입니다. Hello 기록 **응용 프로그램 키는** 값입니다. 응용 프로그램의 코드에서 hello 응용 프로그램으로 hello 값을 사용합니다.
   2. **API 액세스**를 클릭하고 **추가**를 클릭한 다음 웹 API와 범위(사용 권한)를 선택합니다.

> [!NOTE]
> **응용 프로그램 비밀**은 중요한 보안 자격 증명이며 적절하게 보호해야 합니다.
> 
