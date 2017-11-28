### <a name="prerequisites"></a><span data-ttu-id="95a8d-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95a8d-101">Prerequisites</span></span>
* <span data-ttu-id="95a8d-102">[Yammer](https://www.yammer.com/) 계정</span><span class="sxs-lookup"><span data-stu-id="95a8d-102">A [Yammer](https://www.yammer.com/) account</span></span> 

<span data-ttu-id="95a8d-103">논리 앱에서 Yammer 계정을 사용하려면 먼저 Yammer 계정에 연결하도록 논리 앱에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-103">Before you can use your Yammer account in a Logic app, you must authorize the Logic app to connect to your Yammer account.</span></span> <span data-ttu-id="95a8d-104">다행히 Azure 포털의 논리 앱 내에서 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-104">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="95a8d-105">Yammer 계정에 연결하도록 논리 앱에 권한을 부여하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-105">Here are the steps to authorize your Logic app to connect to your Yammer account:</span></span>

1. <span data-ttu-id="95a8d-106">논리 앱 디자이너에서 Yammer에 대한 연결을 만들려면 드롭다운 목록에서 **Microsoft 관리 API 표시**를 선택한 다음 검색 상자에 *Yammer*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-106">To create a connection to Yammer, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Yammer* in the search box.</span></span> <span data-ttu-id="95a8d-107">사용할 트리거 또는 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-107">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-1.png)
2. <span data-ttu-id="95a8d-108">이전에 Yammer에 대한 연결을 만들지 않은 경우 Yammer 자격 증명을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-108">If you haven't created any connections to Yammer before, you'll get prompted to provide your Yammer credentials.</span></span> <span data-ttu-id="95a8d-109">이러한 자격 증명을 사용하여 Yammer 계정의 데이터에 연결하도록 논리 앱에 권한을 부여하고 해당 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-109">These credentials will be used to authorize your Logic app to connect to, and access your Yammer account's data:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-2.png)
3. <span data-ttu-id="95a8d-110">Yammer 사용자 이름 및 암호를 제공하여 논리 앱에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-110">Provide your Yammer user name and password to authorize your Logic app:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-3.png)   
4. <span data-ttu-id="95a8d-111">연결이 만들어졌으므로 이제 논리 앱의 다른 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95a8d-111">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![](./media/connectors-create-api-yammer/yammer-4.png)   

