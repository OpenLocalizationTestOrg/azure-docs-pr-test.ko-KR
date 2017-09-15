### <a name="prerequisites"></a><span data-ttu-id="17d79-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="17d79-101">Prerequisites</span></span>
* <span data-ttu-id="17d79-102">[Dropbox](https://www.Dropbox.com/) 계정</span><span class="sxs-lookup"><span data-stu-id="17d79-102">A [Dropbox](https://www.Dropbox.com/) account</span></span> 

<span data-ttu-id="17d79-103">논리 앱에서 Dropbox 계정을 사용하려면 먼저 Dropbox 계정에 연결하도록 논리 앱에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-103">Before you can use your Dropbox account in a Logic app, you must authorize the Logic app to connect to your Dropbox account.</span></span> <span data-ttu-id="17d79-104">다행히 Azure 포털의 논리 앱 내에서 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-104">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="17d79-105">Dropbox 계정에 연결하도록 논리 앱에 권한을 부여하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-105">Here are the steps to authorize your Logic app to connect to your Dropbox account:</span></span>

1. <span data-ttu-id="17d79-106">논리 앱 디자이너에서 Dropbox에 대한 연결을 만들려면 드롭다운 목록에서 **Microsoft 관리 API 표시**를 선택한 다음 검색 상자에서 *Dropbox*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-106">To create a connection to Dropbox, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Dropbox* in the search box.</span></span> <span data-ttu-id="17d79-107">사용할 트리거 또는 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-107">Select the trigger or action you'll like to use:</span></span>  
   <span data-ttu-id="17d79-108">![Dropbox 1단계](./media/connectors-create-api-dropbox/dropbox-1.png)</span><span class="sxs-lookup"><span data-stu-id="17d79-108">![Dropbox step 1](./media/connectors-create-api-dropbox/dropbox-1.png)</span></span>
2. <span data-ttu-id="17d79-109">이전에 Dropbox에 대한 연결을 만들지 않은 경우 Dropbox 자격 증명을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-109">If you haven't created any connections to Dropbox before, you'll get prompted to provide your Dropbox credentials.</span></span> <span data-ttu-id="17d79-110">이러한 자격 증명을 사용하여 Dropbox 계정의 데이터에 연결하도록 논리 앱에 권한을 부여하고 해당 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-110">These credentials will be used to authorize your Logic app to connect to, and access your Dropbox account's data:</span></span>  
   ![Dropbox 2단계](./media/connectors-create-api-dropbox/dropbox-2.png)
3. <span data-ttu-id="17d79-112">Dropbox 사용자 이름 및 암호를 제공하여 논리 앱에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-112">Provide your Dropbox user name and password to authorize your Logic app:</span></span>  
   ![Dropbox 3단계](./media/connectors-create-api-dropbox/dropbox-3.png)   
4. <span data-ttu-id="17d79-114">논리 앱에 권한을 부여하여 Dropbox 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-114">Authorize the Logic app to use your Dropbox account:</span></span>  
   ![Dropbox 4단계](./media/connectors-create-api-dropbox/dropbox-4.png)
5. <span data-ttu-id="17d79-116">연결이 만들어졌으므로 이제 논리 앱의 다른 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d79-116">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![Dropbox 5단계](./media/connectors-create-api-dropbox/dropbox-5.png)   

