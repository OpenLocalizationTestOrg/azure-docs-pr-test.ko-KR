## <a name="prerequisites"></a>필수 조건
CDN 관리 코드를 작성할 수 있습니다, 전에 필요 toodo 일부 준비 tooenable hello Azure 리소스 관리자가 있는 코드 toointeract 취급 합니다.  toodo이를 해야 합니다.

* 리소스 그룹 toocontain hello에서는이 자습서에서 만드는 CDN 프로필 만들기
* 응용 프로그램에 대 한 Azure Active Directory tooprovide 인증 구성
* 사용 권한을 toohello 리소스 그룹 권한 있는 사용자는 Azure AD 테 넌 트에서 있도록와 상호 작용할 수 우리의 CDN 프로필 적용

### <a name="creating-hello-resource-group"></a>Hello 리소스 그룹 만들기
1. Hello에 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 클릭 **새로** hello 상단 왼쪽에 단추 및 **관리**, 및 **리소스 그룹**합니다.

    ![새 리소스 그룹 만들기](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. *CdnConsoleTutorial*리소스 그룹을 호출합니다.  구독을 선택하고 가까운 위치를 선택합니다.  Hello를 클릭할 수를 **Pin toodashboard** hello 포털 확인란 toopin hello 리소스 그룹 toohello 대시보드 합니다.  이렇게 하면 더욱 쉽게 toofind 나중입니다.  항목을 선택한 후에 **만들기**를 클릭합니다.

    ![Hello 리소스 그룹 이름 지정](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Hello 리소스 그룹을 만든 tooyour 대시보드에 고정 하지 않은 경우 후를 클릭 하 여 찾을 수 있습니다 **찾아보기**, 다음 **리소스 그룹**합니다.  리소스 그룹 tooopen hello 클릭 것입니다.  **구독 ID**를 적어둡니다.  나중에 필요합니다.

    ![Hello 리소스 그룹 이름 지정](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Hello Azure AD 응용 프로그램 만들기 및 사용 권한을 적용
두 가지 방법은 Azure Active Directory와 tooapp 인증: 개별 사용자 또는 서비스 사용자입니다. 서비스 사용자가 Windows에서 비슷한 tooa 서비스 계정입니다.  Hello CDN 프로필을 통해 특정 사용자 권한이 toointeract를 부여 하는 대신에서는 대신 사용 권한을 부여 hello toohello 서비스 사용자.  일반적으로, 서비스 주체는 자동화된 비대화형 프로세스에 사용됩니다.  이 자습서는 대화형 콘솔 응용 프로그램을 작성 하는 경우에 hello 서비스 보안 주체 방식에 살펴볼 것입니다.

Azure Active Directory 응용 프로그램 만들기를 비롯하여 여러 반계로 구성된 서비스 주체를 만듭니다.  toodo이 너무 여기[이 자습서에 따라](../articles/resource-group-create-service-principal-portal.md)합니다.

> [!IMPORTANT]
> 수 있는지 toofollow hello에서 모든 hello 단계 [연결된 자습서](../articles/resource-group-create-service-principal-portal.md)합니다.  설명한 대로 완료하는 것이 *매우 중요합니다*.  있는지 toonote 확인 프로그램 **테 넌 트 ID**, **테 넌 트 도메인 이름** (일반적으로 *. onmicrosoft.com* 도메인 사용자 지정 도메인을 지정 하지 않으면), **클라이언트 ID** , 및 **클라이언트 인증 키**와 마찬가지로 나중에 이러한 필요 합니다.  매우 신중 하 게 tooguard 될 프로그램 **클라이언트 ID** 및 **클라이언트 인증 키**이러한 자격 증명 수, hello 서비스 보안 주체로 tooexecute 작업을 누구나 사용할 합니다.
>
> Toohello 단계 이름은 구성 다중 테 넌 트 응용 프로그램을 가져오면 선택 **아니요**합니다.
>
> Toohello 단계를 가져올 때 [응용 프로그램 toorole 할당](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role)를 사용 하 여 hello 리소스 그룹 앞에서 만든 *CdnConsoleTutorial*, hello 하지 않고 **판독기** 역할 할당 hello **CDN 프로필 참가자** 역할입니다.  Hello 응용 프로그램 hello를 할당 하 고 나면 **CDN 프로필 참가자** 반환 toothis 자습서, 리소스 그룹에 대해 역할입니다. 
>
>

서비스 보안 주체 및 할당 된 hello를 만든 후 **CDN 프로필 참가자** 역할, hello **사용자** 블레이드 리소스 그룹에 대 한 유사한 toothis 같아야 합니다.

![사용자 블레이드](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>대화형 사용자 인증
서비스 사용자 대신 구하려는 경우 대화형 개별 사용자 인증을 하는 경우 hello 프로세스는 서비스 사용자에 대 한 매우 유사한 toothat 합니다.  사실, 해야 toofollow 동일한 절차 hello 하지만 몇 가지 사소한 변경 합니다.

> [!IMPORTANT]
> 서비스 사용자 대신 toouse 개별 사용자 인증을 선택 하는 경우에 다음 단계를 수행 합니다.
>
>

1. 응용 프로그램을 만들 때 **웹 응용 프로그램** 대신 **네이티브 응용 프로그램**을 선택합니다.

    ![네이티브 응용 프로그램](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Hello 다음 페이지에 메시지가 표시 됩니다에 대 한는 **리디렉션 URI**합니다.  hello URI 유효성을 검사할 수 없습니다, 하지만 입력 한 내용을 기억 합니다.  나중에 필요합니다.
3. 필요 toocreate 없습니다는 **클라이언트 인증 키**합니다.
4. 서비스 보안 주체 toohello 할당 하는 대신 **CDN 프로필 참가자** 역할 tooassign 개별 사용자 또는 그룹 하겠습니다.  이 예에서 확인할 수 있습니다 I 할당 한 *CDN 데모 사용자* toohello **CDN 프로필 참가자** 역할입니다.  

    ![개별 사용자 액세스](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
