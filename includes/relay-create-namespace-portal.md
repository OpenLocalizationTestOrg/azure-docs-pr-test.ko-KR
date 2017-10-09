1. <span data-ttu-id="78a04-101">Toohello 로그온 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="78a04-102">Hello hello 포털의 왼쪽된 탐색 창에서 클릭 **새로**, 클릭 **엔터프라이즈 통합**, 클릭 하 고 **릴레이**합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="78a04-103">Hello에 **네임 스페이스 만들기** 대화 상자에서 네임 스페이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="78a04-104">hello 시스템 hello 이름이 사용 가능한 경우 즉시 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="78a04-105">Hello에 **구독** 필드는 toocreate hello 네임 스페이스에는 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="78a04-106">Hello에  **[리소스 그룹](../articles/azure-resource-manager/resource-group-portal.md)**  필드는 hello 네임 스페이스: 라이브, 하거나 새로 만들 기존 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="78a04-107">**위치**, hello 국가 또는 지역에서 네임 스페이스를 호스트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![네임스페이스 만들기][create-namespace]
7. <span data-ttu-id="78a04-109">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-109">Click **Create**.</span></span> <span data-ttu-id="78a04-110">hello 시스템 이제 네임 스페이스 만들고 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="78a04-111">몇 분 후 계정에 대 한 시스템 규정 리소스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="78a04-112">Hello 관리 자격 증명을 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="78a04-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="78a04-113">네임 스페이스의 hello 목록에서 새로 생성 된 네임 스페이스 이름 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="78a04-114">Hello 네임 스페이스 블레이드에서 클릭 **공유 액세스 정책을**합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="78a04-115">Hello에 **공유 액세스 정책을** 블레이드에서 클릭 **RootManageSharedAccessKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="78a04-117">Hello에 **정책: RootManageSharedAccessKey** 블레이드에서 다음 너무 hello 복사 단추를 클릭**연결 문자열-기본 키**, toocopy hello 연결 문자열 tooyour 클립보드 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="78a04-118">메모장이나 기타 다른 위치에 임시로 이 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="78a04-120">반복 hello 이전 단계를 복사 및 붙여넣기의 hello 값 **기본 키** tooa 임시 위치 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78a04-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
