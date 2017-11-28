### <a name="prerequisites"></a><span data-ttu-id="25079-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="25079-101">Prerequisites</span></span>
* <span data-ttu-id="25079-102">Twitter 계정</span><span class="sxs-lookup"><span data-stu-id="25079-102">A Twitter account</span></span> 

<span data-ttu-id="25079-103">논리 앱에서 Twitter 계정을 사용하려면 먼저 Twitter 계정에 연결하도록 논리 앱에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25079-103">Before you can use your Twitter account in a logic app, you must authorize the logic app to connect to your Twitter account.</span></span> <span data-ttu-id="25079-104">다행히 Azure 포털의 논리 앱 내에서 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25079-104">Fortunately, you can do this easily from within your logic app on the Azure Portal.</span></span> 

<span data-ttu-id="25079-105">Twitter 계정에 연결하도록 논리 앱에 권한을 부여하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25079-105">Here are the steps to authorize your logic app to connect to your Twitter account:</span></span>

1. <span data-ttu-id="25079-106">논리 앱 디자이너에서 Twitter에 대한 연결을 만들려면 드롭다운 목록에서 **Microsoft 관리 API 표시**를 선택한 다음 검색 상자에 *Twitter*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25079-106">To create a connection to Twitter, in the logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Twitter* in the search box.</span></span> <span data-ttu-id="25079-107">사용할 트리거 또는 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25079-107">Select the trigger or action you'll like to use:</span></span>  
   <span data-ttu-id="25079-108">![Twitter 연결 이미지 0](./media/connectors-create-api-twitter/twitter-0.png)</span><span class="sxs-lookup"><span data-stu-id="25079-108">![Twitter connection image 0](./media/connectors-create-api-twitter/twitter-0.png)</span></span>
2. <span data-ttu-id="25079-109">이전에 Twitter에 대한 연결을 만들지 않은 경우 Twitter 자격 증명을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25079-109">If you haven't created any connections to Twitter before, you'll get prompted to provide your Twitter credentials.</span></span> <span data-ttu-id="25079-110">이러한 자격 증명을 사용하여 Twitter 계정의 데이터에 연결하도록 논리 앱에 권한을 부여하고 해당 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25079-110">These credentials will be used to authorize your logic app to connect to, and access your Twitter account's data:</span></span>  
   ![Twitter 연결 이미지 1](./media/connectors-create-api-twitter/twitter-1.png)  
3. <span data-ttu-id="25079-112">Twitter 사용자 이름 및 암호를 제공하여 논리 앱에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="25079-112">Provide your Twitter user name and password to authorize your logic app:</span></span>  
   ![Twitter 연결 이미지 2](./media/connectors-create-api-twitter/twitter-2.png)  
4. <span data-ttu-id="25079-114">권한 부여를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25079-114">Confirm your authorization:</span></span>  
   ![Twitter 연결 이미지 3](./media/connectors-create-api-twitter/twitter-3.png)  
5. <span data-ttu-id="25079-116">연결이 만들어졌으므로 이제 논리 앱의 다른 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25079-116">Notice the connection has been created and you are now free to proceed with the other steps in your logic app:</span></span>  
   ![Twitter 연결 이미지 4](./media/connectors-create-api-twitter/twitter-4.png)

