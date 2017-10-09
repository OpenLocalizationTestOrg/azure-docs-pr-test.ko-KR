### <a name="prerequisites"></a><span data-ttu-id="45172-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="45172-101">Prerequisites</span></span>
* <span data-ttu-id="45172-102">Twilio 계정</span><span class="sxs-lookup"><span data-stu-id="45172-102">A Twilio account</span></span>
* <span data-ttu-id="45172-103">SMS를 받을 수 있다고 확인된 Twilio 전화 번호</span><span class="sxs-lookup"><span data-stu-id="45172-103">A verified Twilio phone number that can receive SMS</span></span>
* <span data-ttu-id="45172-104">SMS를 보낼 수 있다고 확인된 Twilio 전화 번호</span><span class="sxs-lookup"><span data-stu-id="45172-104">A verified Twilio phone number that can send SMS</span></span>

> [!NOTE]
> <span data-ttu-id="45172-105">Twilio 평가판 계정을 사용 하 고, 보낼 수 있습니다만 SMS 너무**확인** 전화 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="45172-105">If you are using a Twilio trial account, you can only send SMS too**verified** phone numbers.</span></span>  
> 
> 

<span data-ttu-id="45172-106">Twilio 계정에서 논리 앱을 사용 하려면 먼저 hello 논리 앱 tooconnect tooyour Twilio 계정에 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45172-106">Before you can use your Twilio account in a Logic app, you must authorize hello Logic app tooconnect tooyour Twilio account.</span></span> <span data-ttu-id="45172-107">다행히 hello Azure 포털에서 논리 앱 내에서이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45172-107">Fortunately, you can do this easily from within your Logic app on hello Azure Portal.</span></span> 

<span data-ttu-id="45172-108">논리 앱 tooconnect tooyour Twilio 계정 hello 단계 tooauthorize 키를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45172-108">Here are hello steps tooauthorize your Logic app tooconnect tooyour Twilio account:</span></span>

1. <span data-ttu-id="45172-109">toocreate hello 논리가 응용 프로그램 디자이너에는 연결 tooTwilio 선택 **표시 Microsoft 관리 되는 Api** hello 드롭 다운 목록 다음 입력 *Twilio* hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45172-109">toocreate a connection tooTwilio, in hello Logic app designer, select **Show Microsoft managed APIs** in hello drop down list then enter *Twilio* in hello search box.</span></span> <span data-ttu-id="45172-110">Hello 트리거나 toouse 만드는 것이 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45172-110">Select hello trigger or action you'll like toouse:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. <span data-ttu-id="45172-111">하기 전에 모든 연결 tooTwilio을 만들지 않은 경우 Twilio 자격 증명된 tooprovide를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45172-111">If you haven't created any connections tooTwilio before, you'll get prompted tooprovide your Twilio credentials.</span></span> <span data-ttu-id="45172-112">이러한 자격 증명 사용된 tooauthorize 하 여 논리 앱 tooconnect 되며 Twilio 계정의 데이터에 액세스:</span><span class="sxs-lookup"><span data-stu-id="45172-112">These credentials will be used tooauthorize your Logic app tooconnect to, and access your Twilio account's data:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. <span data-ttu-id="45172-113">Hello 해야 **Twilio 계정 id** 및 **Twilio 액세스 토큰** Twilio에서 hello 대시보드에서 있으므로 로그인 tooyour Twilio 계정 지금 toograb이 두 가지 정보:</span><span class="sxs-lookup"><span data-stu-id="45172-113">You'll need hello **Twilio account id** and **Twilio access token**  from hello dashboard in Twilio, so log in tooyour Twilio account now toograb these two pieces of information:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. <span data-ttu-id="45172-114">Twilio 및 논리 앱 서로 다른 이름을 tooidentify이 두 가지 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45172-114">Twilio and Logic apps use different names tooidentify these two pieces of infomation.</span></span> <span data-ttu-id="45172-115">어떻게 해야 매핑하십시오 toohello 논리 앱 대화 다음과 같습니다.![](./media/connectors-create-api-twilio/twilio-3.png)</span><span class="sxs-lookup"><span data-stu-id="45172-115">Here is how you must map them toohello Logic apps dialog: ![](./media/connectors-create-api-twilio/twilio-3.png)</span></span>  
5. <span data-ttu-id="45172-116">선택 hello **연결을 만들** 단추:</span><span class="sxs-lookup"><span data-stu-id="45172-116">Select hello **Create connection** button:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. <span data-ttu-id="45172-117">Hello 연결 만들었으며 했으면 이제 다른 hello로 무료 tooproceed 논리 앱에서 단계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45172-117">Notice hello connection has been created and you are now free tooproceed with hello other steps in your Logic app:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

