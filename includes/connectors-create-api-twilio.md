### <a name="prerequisites"></a><span data-ttu-id="73f1e-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="73f1e-101">Prerequisites</span></span>
* <span data-ttu-id="73f1e-102">Twilio 계정</span><span class="sxs-lookup"><span data-stu-id="73f1e-102">A Twilio account</span></span>
* <span data-ttu-id="73f1e-103">SMS를 받을 수 있다고 확인된 Twilio 전화 번호</span><span class="sxs-lookup"><span data-stu-id="73f1e-103">A verified Twilio phone number that can receive SMS</span></span>
* <span data-ttu-id="73f1e-104">SMS를 보낼 수 있다고 확인된 Twilio 전화 번호</span><span class="sxs-lookup"><span data-stu-id="73f1e-104">A verified Twilio phone number that can send SMS</span></span>

> [!NOTE]
> <span data-ttu-id="73f1e-105">Twilio 체험 계정을 사용하는 경우 **확인된** 전화 번호에만 SMS를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-105">If you are using a Twilio trial account, you can only send SMS to **verified** phone numbers.</span></span>  
> 
> 

<span data-ttu-id="73f1e-106">논리 앱에서 Twilio 계정을 사용하려면 먼저 Twilio 계정에 연결하도록 논리 앱에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-106">Before you can use your Twilio account in a Logic app, you must authorize the Logic app to connect to your Twilio account.</span></span> <span data-ttu-id="73f1e-107">다행히 Azure 포털의 논리 앱 내에서 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-107">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="73f1e-108">Twilio 계정에 연결하도록 논리 앱에 권한을 부여하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-108">Here are the steps to authorize your Logic app to connect to your Twilio account:</span></span>

1. <span data-ttu-id="73f1e-109">논리 앱 디자이너에서 Twilio에 대한 연결을 만들려면 드롭다운 목록에서 **Microsoft 관리 API 표시**를 선택한 다음 검색 상자에 *Twilio*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-109">To create a connection to Twilio, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Twilio* in the search box.</span></span> <span data-ttu-id="73f1e-110">사용할 트리거 또는 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-110">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. <span data-ttu-id="73f1e-111">이전에 Twilio에 대한 연결을 만들지 않은 경우 Twilio 자격 증명을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-111">If you haven't created any connections to Twilio before, you'll get prompted to provide your Twilio credentials.</span></span> <span data-ttu-id="73f1e-112">이러한 자격 증명을 사용하여 Twilio 계정의 데이터에 연결하도록 논리 앱에 권한을 부여하고 해당 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-112">These credentials will be used to authorize your Logic app to connect to, and access your Twilio account's data:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. <span data-ttu-id="73f1e-113">Twilio의 대시보드에서 **Twilio 계정 ID** 및 **Twilio 액세스 토큰**이 필요하므로 이제 Twilio 계정에 로그인하여 두 가지 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-113">You'll need the **Twilio account id** and **Twilio access token**  from the dashboard in Twilio, so log in to your Twilio account now to grab these two pieces of information:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. <span data-ttu-id="73f1e-114">Twilio 및 논리 앱에서는 서로 다른 이름을 사용하여 이러한 두 가지 정보를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-114">Twilio and Logic apps use different names to identify these two pieces of infomation.</span></span> <span data-ttu-id="73f1e-115">이러한 정보를 Logic Apps 대화 상자에 매핑하는 방법은 다음과 같습니다. ![](./media/connectors-create-api-twilio/twilio-3.png)</span><span class="sxs-lookup"><span data-stu-id="73f1e-115">Here is how you must map them to the Logic apps dialog: ![](./media/connectors-create-api-twilio/twilio-3.png)</span></span>  
5. <span data-ttu-id="73f1e-116">**연결 만들기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-116">Select the **Create connection** button:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. <span data-ttu-id="73f1e-117">연결이 만들어졌으므로 이제 논리 앱의 다른 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f1e-117">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

