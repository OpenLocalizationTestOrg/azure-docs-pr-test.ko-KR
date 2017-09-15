1. <span data-ttu-id="58849-101">[Azure Portal][Azure portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-101">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="58849-102">포털의 왼쪽 탐색 창에서 **새로 만들기**, **엔터프라이즈 통합** 및 **릴레이**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="58849-103">**네임스페이스 만들기** 대화 상자에서 네임스페이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-103">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="58849-104">시스템에서 사용 가능한 이름인지 즉시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-104">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="58849-105">**구독** 필드에서 네임스페이스를 만들 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
5. <span data-ttu-id="58849-106">**[리소스 그룹](../articles/azure-resource-manager/resource-group-portal.md)** 필드에서 네임스페이스가 있는 기존 리소스 그룹을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58849-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="58849-107">**위치**에서 네임스페이스가 호스트되어야 하는 국가 또는 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-107">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![네임스페이스 만들기][create-namespace]
7. <span data-ttu-id="58849-109">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-109">Click **Create**.</span></span> <span data-ttu-id="58849-110">이제 시스템이 네임스페이스를 만들고 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-110">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="58849-111">몇 분 후 시스템이 계정에 대한 리소스를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-111">After a few minutes, the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="58849-112">관리 자격 증명 얻기</span><span class="sxs-lookup"><span data-stu-id="58849-112">Obtain the management credentials</span></span>
1. <span data-ttu-id="58849-113">네임스페이스 목록에서 새로 만든 네임스페이스 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-113">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="58849-114">네임스페이스 블레이드에서 **공유 액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-114">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="58849-115">**공유 액세스 정책** 블레이드에서 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="58849-117">**정책: RootManageSharedAccessKey** 블레이드에서 **연결 문자열–기본 키** 옆의 복사 단추를 클릭하여 나중에 사용하기 위해 연결 문자열을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="58849-118">메모장이나 기타 다른 위치에 임시로 이 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58849-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="58849-120">이전 단계를 반복하여 나중에 사용할 수 있도록 **기본 키** 값을 임시 위치에 복사 및 붙여넣기합니다.</span><span class="sxs-lookup"><span data-stu-id="58849-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
