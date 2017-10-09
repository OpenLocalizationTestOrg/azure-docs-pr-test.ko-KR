<span data-ttu-id="cfe10-101">도메인 이름에 대 한 hello 레코드를 전파 해야 사용자 지정 도메인 이름을 수 있는 사용자 브라우저 tooverify 수 toouse 수 사용된 tooaccess Azure 앱 서비스의 웹 응용 프로그램 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-101">After hello records for your domain name have propagated, you should be able toouse your browser tooverify that your custom domain name can be used tooaccess your web app in Azure App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="cfe10-102">Hello DNS 시스템을 통해 프로그램 CNAME toopropagate 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-102">It can take some time for your CNAME toopropagate through hello DNS system.</span></span> <span data-ttu-id="cfe10-103">와 같은 서비스를 사용할 수 <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> CNAME hello tooverify를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-103">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify that hello CNAME is available.</span></span>
> 
> 

<span data-ttu-id="cfe10-104">트래픽 관리자 끝점으로 웹 앱을 이미 추가 하지 않은 경우 이렇게 해야 hello 사용자 지정 도메인 이름 경로 tooTraffic 관리자와 이름 확인이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-104">If you have not already added your web app as a Traffic Manager endpoint, you must do this before name resolution will work, as hello custom domain name routes tooTraffic Manager.</span></span> <span data-ttu-id="cfe10-105">트래픽 관리자는 다음 tooyour 웹 응용 프로그램을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-105">Traffic Manager then routes tooyour web app.</span></span> <span data-ttu-id="cfe10-106">Hello 정보에 사용 하 여 [추가 / 삭제 끝점](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd 트래픽 관리자 프로필에서 끝점으로 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-106">Use hello information in [Add or Delete Endpoints](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd your web app as an endpoint in your Traffic Manager profile.</span></span>

> [!NOTE]
> <span data-ttu-id="cfe10-107">끝점을 추가할 때 웹앱이 목록에 나열되지 않는 경우 웹앱이 **표준** 앱 서비스 계획 모드로 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-107">If your web app is not listed when adding an endpoint, verify that it is configured for **Standard** App Service plan mode.</span></span> <span data-ttu-id="cfe10-108">사용 해야 **표준** 순서 toowork 트래픽 관리자에서에서 웹 응용 프로그램에 대 한 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-108">You must use **Standard** mode for your web app in order toowork with Traffic Manager.</span></span>
> 
> 

1. <span data-ttu-id="cfe10-109">브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-109">In your browser, open hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cfe10-110">Hello에 **웹 앱** 탭을 선택 하면 웹 앱의 hello 이름을 클릭 **설정**를 선택한 후 **사용자 지정 도메인이**</span><span class="sxs-lookup"><span data-stu-id="cfe10-110">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="cfe10-111">Hello에 **사용자 지정 도메인** 블레이드에서 클릭 **호스트 이름 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-111">In hello **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="cfe10-112">사용 하 여 hello **Hostname** 텍스트 상자 tooenter hello 트래픽 관리자 도메인 이름 tooassociate이 웹 앱과.</span><span class="sxs-lookup"><span data-stu-id="cfe10-112">Use hello **Hostname** text boxes tooenter hello Traffic Manager domain name tooassociate with this web app.</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. <span data-ttu-id="cfe10-113">클릭 **유효성 검사** toosave hello 도메인 이름 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-113">Click **Validate** toosave hello domain name configuration.</span></span>
6. <span data-ttu-id="cfe10-114">**유효성 검사** 를 클릭하면 Azure에서 도메인 검증 워크플로가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-114">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="cfe10-115">도메인 소유권으로 호스트 이름 가용성과 보고서의 성공 또는 된 규범적인 부모의 toofix 오류 hello 하는 방법에 자세한 오류 체크 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-115">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how toofix hello error.</span></span>    
7. <span data-ttu-id="cfe10-116">유효성을 검사 **호스트 이름 추가** 단추가 활성화 됩니다 고 수 toohello 할당 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-116">Upon successful validation **Add hostname** button will become active and you will be able toohello assign hostname.</span></span> <span data-ttu-id="cfe10-117">브라우저에서 사용자 지정 도메인 이름을 tooyour 이제 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-117">Now navigate tooyour custom domain name in a browser.</span></span> <span data-ttu-id="cfe10-118">이제 사용자 지정 도메인 이름을 사용하여 앱이 실행되고 있음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-118">You should now see your app running using your custom domain name.</span></span> 
   
   <span data-ttu-id="cfe10-119">Hello 사용자 지정 도메인 이름을 hello에 나열 됩니다 구성 완료 되 면 **도메인 이름** 웹 앱의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-119">Once configuration has completed, hello custom domain name will be listed in hello **domain names** section of your web app.</span></span>

<span data-ttu-id="cfe10-120">이 시점에서 브라우저에서 수 tooenter hello 트래픽 관리자 도메인 이름 이름 이어야 하 고는 성공적으로 장에서 tooyour 웹 응용 프로그램을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfe10-120">At this point, you should be able tooenter hello Traffic Manager domain name name in your browser and see that it successfully takes you tooyour web app.</span></span>

