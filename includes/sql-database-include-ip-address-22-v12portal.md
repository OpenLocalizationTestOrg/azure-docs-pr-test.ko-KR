
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="50fec-101">Toohello 로그인 [Azure 포털](https://portal.azure.com/) http://portal.azure.com/에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="50fec-102">Hello 왼쪽된 배너에서 클릭 **모두 찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="50fec-103">hello **찾아보기** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="50fec-104">스크롤하여 **SQL Server**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="50fec-105">hello **SQL server** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Hello 포털에서 Azure SQL 데이터베이스 서버를 찾아][b21-FindServerInPortal]
4. <span data-ttu-id="50fec-107">편의 위해 hello 클릭 hello 이전 버전에서 컨트롤을 최소화 **찾아보기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="50fec-108">Hello 필터 텍스트 상자에 서버 이름을 hello 입력을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="50fec-109">해당 행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-109">Your row is displayed.</span></span>
6. <span data-ttu-id="50fec-110">서버에 대 한 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-110">Click hello row for your server.</span></span> <span data-ttu-id="50fec-111">서버 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="50fec-112">서버 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="50fec-113">hello **설정을** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="50fec-114">**방화벽**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-114">Click **Firewall**.</span></span> <span data-ttu-id="50fec-115">hello **방화벽 설정을** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![설정 > 방화벽을 클릭합니다.][b31-SettingsFirewallNavig]
9. <span data-ttu-id="50fec-117">**클라이언트 IP 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-117">Click **Add Client IP**.</span></span> <span data-ttu-id="50fec-118">Hello 첫 번째 텍스트 상자에 새 규칙에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="50fec-119">낮은 임계값과 높은 hello 입력 IP 주소 원하는 hello 범위에 대 한 값 tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="50fec-120">것이 편리한 toohave hello 낮은 값 끝나야 **.0** 및 안전한 것으로 hello **.255**합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![IP 주소 범위 tooallow 추가][b41-AddRange]
11. <span data-ttu-id="50fec-122">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50fec-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
