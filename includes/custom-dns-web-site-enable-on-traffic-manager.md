<span data-ttu-id="0e492-101">도메인 이름의 레코드가 전파된 후 브라우저를 사용하여 Azure 앱 서비스의 웹앱에 액세스하는 데 사용자 지정 도메인 이름을 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-101">After the records for your domain name have propagated, you should be able to use your browser to verify that your custom domain name can be used to access your web app in Azure App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="0e492-102">CNAME이 DNS 시스템을 통해 전파되는 데 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-102">It can take some time for your CNAME to propagate through the DNS system.</span></span> <span data-ttu-id="0e492-103"><a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> 등의 서비스를 사용하여 CNAME을 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-103">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the CNAME is available.</span></span>
> 
> 

<span data-ttu-id="0e492-104">웹앱을 트래픽 관리자 끝점으로 아직 추가하지 않은 경우 이름 확인이 적용되기 전에 사용자 지정 도메인 이름이 트래픽 관리자로 라우팅할 때 이를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-104">If you have not already added your web app as a Traffic Manager endpoint, you must do this before name resolution will work, as the custom domain name routes to Traffic Manager.</span></span> <span data-ttu-id="0e492-105">그런 다음 트래픽 관리자가 웹앱으로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-105">Traffic Manager then routes to your web app.</span></span> <span data-ttu-id="0e492-106">[끝점 추가 또는 삭제](../articles/traffic-manager/traffic-manager-endpoints.md) 의 내용을 참조하여 트래픽 관리자 프로필에서 웹앱을 끝점으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-106">Use the information in [Add or Delete Endpoints](../articles/traffic-manager/traffic-manager-endpoints.md) to add your web app as an endpoint in your Traffic Manager profile.</span></span>

> [!NOTE]
> <span data-ttu-id="0e492-107">끝점을 추가할 때 웹앱이 목록에 나열되지 않는 경우 웹앱이 **표준** 앱 서비스 계획 모드로 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-107">If your web app is not listed when adding an endpoint, verify that it is configured for **Standard** App Service plan mode.</span></span> <span data-ttu-id="0e492-108">**표준** 모드로 구성된 웹앱만이 트래픽 관리자에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-108">You must use **Standard** mode for your web app in order to work with Traffic Manager.</span></span>
> 
> 

1. <span data-ttu-id="0e492-109">브라우저에서 [Azure 포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-109">In your browser, open the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0e492-110">**Web Apps** 탭에서 웹앱의 이름을 클릭하고 **설정**을 선택한 다음 **사용자 지정 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-110">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="0e492-111">**사용자 지정 도메인** 블레이드에서 **호스트 이름 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-111">In the **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="0e492-112">**호스트 이름** 텍스트 상자에 이 웹앱과 연결할 트래픽 관리자 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-112">Use the **Hostname** text boxes to enter the Traffic Manager domain name to associate with this web app.</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. <span data-ttu-id="0e492-113">**유효성 검사** 를 클릭하여 도메인 이름 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-113">Click **Validate** to save the domain name configuration.</span></span>
6. <span data-ttu-id="0e492-114">**유효성 검사** 를 클릭하면 Azure에서 도메인 검증 워크플로가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-114">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="0e492-115">여기서는 호스트 이름 가용성 및 보고서 성공 여부 외에 도메인 소유권을 확인하거나 자세한 오류 사항과 그에 대한 해결 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-115">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how to fix the error.</span></span>    
7. <span data-ttu-id="0e492-116">유효성 검사가 성공하면 **호스트 이름 추가** 단추가 활성화되며 호스트 이름을 할당할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-116">Upon successful validation **Add hostname** button will become active and you will be able to the assign hostname.</span></span> <span data-ttu-id="0e492-117">이제 브라우저에서 사용자 지정 도메인 이름으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-117">Now navigate to your custom domain name in a browser.</span></span> <span data-ttu-id="0e492-118">이제 사용자 지정 도메인 이름을 사용하여 앱이 실행되고 있음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-118">You should now see your app running using your custom domain name.</span></span> 
   
   <span data-ttu-id="0e492-119">구성이 완료되면 사용자 지정 도메인 이름이 웹앱의 **도메인 이름** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-119">Once configuration has completed, the custom domain name will be listed in the **domain names** section of your web app.</span></span>

<span data-ttu-id="0e492-120">이때 브라우저에서 트래픽 관리자 도메인 이름을 입력해야 웹앱으로 이동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e492-120">At this point, you should be able to enter the Traffic Manager domain name name in your browser and see that it successfully takes you to your web app.</span></span>

