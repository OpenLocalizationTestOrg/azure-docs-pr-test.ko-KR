1. [Azure Portal][Azure portal]에 로그인합니다.
2. 포털의 왼쪽 탐색 창에서 **새로 만들기**, **엔터프라이즈 통합** 및 **릴레이**를 차례로 클릭합니다.
3. **네임스페이스 만들기** 대화 상자에서 네임스페이스 이름을 입력합니다. 시스템에서 사용 가능한 이름인지 즉시 확인합니다.
4. **구독** 필드에서 네임스페이스를 만들 Azure 구독을 선택합니다.
5. **[리소스 그룹](../articles/azure-resource-manager/resource-group-portal.md)** 필드에서 네임스페이스가 있는 기존 리소스 그룹을 선택하거나 새로 만듭니다.      
6. **위치**에서 네임스페이스가 호스트되어야 하는 국가 또는 지역을 선택합니다.
   
    ![네임스페이스 만들기][create-namespace]
7. **만들기**를 클릭합니다. 이제 시스템이 네임스페이스를 만들고 사용하도록 설정합니다. 몇 분 후 시스템이 계정에 대한 리소스를 프로비전합니다.

### <a name="obtain-the-management-credentials"></a>관리 자격 증명 얻기
1. 네임스페이스 목록에서 새로 만든 네임스페이스 이름을 클릭합니다.
2. 네임스페이스 블레이드에서 **공유 액세스 정책**을 클릭합니다.
3. **공유 액세스 정책** 블레이드에서 **RootManageSharedAccessKey**를 클릭합니다.
   
    ![connection-info][connection-info]
4. **정책: RootManageSharedAccessKey** 블레이드에서 **연결 문자열–기본 키** 옆의 복사 단추를 클릭하여 나중에 사용하기 위해 연결 문자열을 클립보드에 복사합니다. 메모장이나 기타 다른 위치에 임시로 이 값을 붙여 넣습니다.
   
    ![connection-string][connection-string]

5. 이전 단계를 반복하여 나중에 사용할 수 있도록 **기본 키** 값을 임시 위치에 복사 및 붙여넣기합니다.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
