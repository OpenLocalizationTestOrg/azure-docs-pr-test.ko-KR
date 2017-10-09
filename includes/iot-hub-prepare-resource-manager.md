## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Azure 리소스 관리자 요청 tooauthenticate 준비
Hello를 사용 하 여 리소스에서 수행 하는 모든 hello 작업을 인증 해야 [Azure 리소스 관리자] [ lnk-authenticate-arm] 와 Azure AD (Active Directory). 가장 쉬운 방법은 tooconfigure hello toouse PowerShell 또는 Azure CLI입니다.

Hello 설치 [Azure PowerShell cmdlet] [ lnk-powershell-install] 계속 하기 전에.

단계 표시 방법을 따르는 hello tooset PowerShell을 사용 하 여 AD 응용 프로그램에 대 한 암호 인증을 합니다. 표준 PowerShell 세션에서 이러한 명령을 실행할 수 있습니다.

1. 다음 명령을 hello를 사용 하 여 Azure 구독 tooyour에 로그인 합니다.

    ```powershell
    Login-AzureRmAccount
    ```

1. TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 구독. 다음 명령을 toolist hello 있습니다 사용할 수 있는 Azure 구독 toouse hello를 사용 합니다.

    ```powershell
    Get-AzureRMSubscription
    ```

    다음 명령은 tooselect 구독 toouse toorun hello 명령을 toomanage IoT 허브를 지정 하는 hello를 사용 합니다. Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. **TenantId** 및 **SubscriptionId**를 적어둡니다. 나중에 필요합니다.
3. 다음 명령을, hello 자리 표시자를 대체 하는 hello를 사용 하 여 새 Azure Active Directory 응용 프로그램을 만듭니다.
   
   * **{표시 이름}:** **MySampleApp**과 같은 응용 프로그램의 표시 이름입니다.
   * **{홈 페이지 URL}:** 와 같은 응용 프로그램의 hello 홈 페이지의 URL을 hello **http://mysampleapp/home**합니다. 이 URL toopoint tooa 실제 응용 프로그램이 필요는 없습니다.
   * **{응용 프로그램 식별자}:** **http://mysampleapp**과 같은 고유 식별자입니다. 이 URL toopoint tooa 실제 응용 프로그램이 필요는 없습니다.
   * **{Password}:** tooauthenticate 응용 프로그램과 함께 사용 하는 암호입니다.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Hello 메모 **ApplicationId** 만든 hello 응용 프로그램의 합니다. 나중에 필요합니다.
5. 다음 명령을, 대체 hello를 사용 하 여 새 서비스 사용자를 만들 **{MyApplicationId}** hello로 **ApplicationId** hello 이전 단계에서:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. 다음 명령을, 대체 hello를 사용 하 여 역할 할당을 설정 **{MyApplicationId}** 와 프로그램 **ApplicationId**합니다.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

이제 사용자 지정 C# 응용 프로그램에서 tooauthenticate 수 있는 hello Azure AD 응용 프로그램을 만드는 작업이 완료 되었습니다. 다음 값에는이 자습서의 뒷부분에 나오는 hello가 필요 합니다.

* TenantId
* SubscriptionId
* ApplicationId
* 암호

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
