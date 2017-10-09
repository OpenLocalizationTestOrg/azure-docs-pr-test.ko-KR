<span data-ttu-id="cad8e-101">도메인 이름에 대 한 hello 레코드를 전파 웹 앱과 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-101">After hello records for your domain name have propagated, you must associate them with your Web App.</span></span> <span data-ttu-id="cad8e-102">다음 웹 브라우저를 사용 하 여 단계 tooenable hello 도메인 이름을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-102">Use hello following steps tooenable hello domain names using your web browser.</span></span>

> [!NOTE]
> <span data-ttu-id="cad8e-103">TXT 레코드 hello DNS 시스템을 통해 이전 단계 toopropagate hello에서에서 만든 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-103">It can take some time for TXT records created in hello previous steps toopropagate through hello DNS system.</span></span> <span data-ttu-id="cad8e-104">Hello TXT 레코드에 전파 될 때까지 tooyour 웹 응용 프로그램의 hello 도메인 이름을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-104">You cannot add hello domain name of tooyour web app until hello TXT record has propagated.</span></span> <span data-ttu-id="cad8e-105">A 레코드를 사용 하는 hello 이전 단계에서 만든 hello TXT 레코드에 전파 될 때까지 hello 레코드 도메인 이름 tooyour 웹 응용 프로그램을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-105">If you are using an A record, you cannot add hello A record domain name tooyour web app until hello TXT record created in hello previous step has propagated.</span></span>
> 
> <span data-ttu-id="cad8e-106">와 같은 서비스를 사용할 수 <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> TXT 레코드 hello tooverify를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-106">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify that hello TXT record is available.</span></span>
> 
> 

1. <span data-ttu-id="cad8e-107">브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-107">In your browser, open hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cad8e-108">Hello에 **웹 앱** 탭, 웹 앱의 hello 이름을 클릭 한 다음 선택 **사용자 지정 도메인이**</span><span class="sxs-lookup"><span data-stu-id="cad8e-108">In hello **Web Apps** tab, click hello name of your web app, and then select **Custom domains**</span></span>
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="cad8e-109">Hello에 **사용자 지정 도메인** 블레이드에서 클릭 **호스트 이름 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-109">In hello **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="cad8e-110">사용 하 여 hello **Hostname** 텍스트 상자 tooenter hello 도메인 이름 tooassociate이 웹 앱과.</span><span class="sxs-lookup"><span data-stu-id="cad8e-110">Use hello **Hostname** text boxes tooenter hello domain names tooassociate with this web app.</span></span>
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. <span data-ttu-id="cad8e-111">**유효성 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-111">Click **Validate**.</span></span>
6. <span data-ttu-id="cad8e-112">**유효성 검사** 를 클릭하면 Azure에서 도메인 검증 워크플로가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-112">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="cad8e-113">도메인 소유권으로 호스트 이름 가용성과 보고서의 성공 또는 된 규범적인 부모의 toofix 오류 hello 하는 방법에 자세한 오류 체크 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-113">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how toofix hello error.</span></span>    

<span data-ttu-id="cad8e-114">이 시점에서 브라우저에서 수 tooenter hello 사용자 지정 도메인 이름 이어야 하 고는 성공적으로 장에서 tooyour 웹 응용 프로그램을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cad8e-114">At this point, you should be able tooenter hello custom domain name in your browser and see that it successfully takes you tooyour web app.</span></span>

