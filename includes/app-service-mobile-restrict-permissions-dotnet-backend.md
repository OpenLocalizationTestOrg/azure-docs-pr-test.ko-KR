
<span data-ttu-id="f15c1-101">기본적으로 Mobile Apps 백 엔드의 API는 익명으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-101">By default, APIs in a Mobile Apps back end can be invoked anonymously.</span></span> <span data-ttu-id="f15c1-102">다음으로, toorestrict 액세스 인증 tooonly 클라이언트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-102">Next, you need toorestrict access tooonly authenticated clients.</span></span>  

* <span data-ttu-id="f15c1-103">**Node.js 다시 (Azure 포털 hello)를 통해 종료** :</span><span class="sxs-lookup"><span data-stu-id="f15c1-103">**Node.js back end (via hello Azure portal)** :</span></span>  

    <span data-ttu-id="f15c1-104">Mobile Apps 설정에서 **간편한 테이블**을 클릭하고 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-104">In your Mobile Apps settings, click **Easy Tables** and select your table.</span></span> <span data-ttu-id="f15c1-105">**사용 권한 변경**을 클릭하고 모든 사용 권한에 대해 **인증된 액세스만**을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-105">Click **Change permissions**, select **Authenticated access only** for all permissions, and then click **Save**.</span></span>
* <span data-ttu-id="f15c1-106">**.NET 백 엔드(C#)**:</span><span class="sxs-lookup"><span data-stu-id="f15c1-106">**.NET back end (C#)**:</span></span>  

    <span data-ttu-id="f15c1-107">Hello 서버 프로젝트에서 이동 너무**컨트롤러** > **TodoItemController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-107">In hello server project, navigate too**Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="f15c1-108">Hello 추가 `[Authorize]` toohello 특성 **TodoItemController** 클래스를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-108">Add hello `[Authorize]` attribute toohello **TodoItemController** class, as follows.</span></span> <span data-ttu-id="f15c1-109">toorestrict 액세스만 toospecific 메서드 hello 클래스 대신이 특성 정당한 toothose 메서드를 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-109">toorestrict access only toospecific methods, you can also apply this attribute just toothose methods instead of hello class.</span></span> <span data-ttu-id="f15c1-110">Hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-110">Republish hello server project.</span></span>

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* <span data-ttu-id="f15c1-111">**(Node.js 코드를 통해) Node.js 백 엔드** :</span><span class="sxs-lookup"><span data-stu-id="f15c1-111">**Node.js backend (via Node.js code)** :</span></span>  

    <span data-ttu-id="f15c1-112">테이블 액세스를 위한 toorequire 인증 hello 다음 줄 toohello Node.js 서버 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-112">toorequire authentication for table access, add hello following line toohello Node.js server script:</span></span>

        table.access = 'authenticated';

    <span data-ttu-id="f15c1-113">자세한 내용은 참조 하십시오. [하는 방법: 액세스 tootables에 인증 필요](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth)합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-113">For more details, see [How to: Require authentication for access tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth).</span></span> <span data-ttu-id="f15c1-114">사이트에서 toodownload hello 퀵 스타트 코드 프로젝트를 확인 하려면 어떻게 toolearn [하는 방법: Git를 사용 하 여 다운로드 hello Node.js 백 엔드 퀵 스타트 코드 프로젝트](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)합니다.</span><span class="sxs-lookup"><span data-stu-id="f15c1-114">toolearn how toodownload hello quickstart code project from your site, see [How to: Download hello Node.js backend quickstart code project using Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).</span></span>
