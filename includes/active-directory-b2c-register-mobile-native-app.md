[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

모바일 또는 네이티브 응용 프로그램을 등록하려면 표에 지정된 설정을 사용합니다.

![새 모바일 또는 네이티브 응용 프로그램에 대한 등록 설정 예](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| 설정      | 샘플 값  | 설명                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Name** | Contoso B2C 앱 | 소비자에게 응용 프로그램을 설명하는 응용 프로그램 **이름**을 입력합니다. |
| **네이티브 클라이언트** | 예 | 모바일 또는 네이티브 응용 프로그램에 **예**를 선택합니다. |
| **사용자 지정 리디렉션 URI** | `com.onmicrosoft.contoso.appname://redirect/path` | 사용자 지정 체계로 리디렉션 URI를 입력합니다. [적절한 리디렉션 URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri)를 선택하고 밑줄 등의 특수 문자를 포함하지 마십시오. |

**만들기**를 클릭하여 응용 프로그램을 등록합니다.

새로 등록된 응용 프로그램은 B2C 테넌트에 대한 응용 프로그램 목록에 표시됩니다. 목록에서 모바일 또는 네이티브 앱을 선택합니다. 응용 프로그램의 속성 창이 표시됩니다.

![응용 프로그램 속성](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

전역적으로 고유한 **응용 프로그램 클라이언트 ID**를 기록합니다. 응용 프로그램 코드의 ID를 사용합니다.

네이티브 응용 프로그램이 Azure AD B2C에서 보호하는 웹 API를 호출하는 경우 다음 단계를 수행하세요.
   1. **키** 블레이드로 이동하여 **키 생성** 단추를 클릭하여 응용 프로그램 비밀을 만듭니다. **앱 키** 값을 기록해 둡니다. 이 값을 응용 프로그램의 코드에서 응용 프로그램 비밀로 사용합니다.
   2. **API 액세스**를 클릭하고 **추가**를 클릭한 다음 웹 API와 범위(사용 권한)를 선택합니다.

> [!NOTE]
> **응용 프로그램 비밀**은 중요한 보안 자격 증명이며 적절하게 보호해야 합니다.
> 
