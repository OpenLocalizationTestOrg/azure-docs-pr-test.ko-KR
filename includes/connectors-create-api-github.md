### <a name="prerequisites"></a><span data-ttu-id="9546b-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9546b-101">Prerequisites</span></span>
* <span data-ttu-id="9546b-102">[GitHub](http://GitHub.com) 계정</span><span class="sxs-lookup"><span data-stu-id="9546b-102">A [GitHub](http://GitHub.com) account</span></span> 

<span data-ttu-id="9546b-103">논리 앱에서 GitHub 계정을 사용하려면 먼저 GitHub 계정에 연결하도록 논리 앱에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-103">Before you can use your GitHub account in a Logic app, you must authorize the Logic app to connect to your GitHub account.</span></span> <span data-ttu-id="9546b-104">다행히 Azure 포털의 논리 앱 내에서 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-104">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="9546b-105">GitHub 계정에 연결하도록 논리 앱에 권한을 부여하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-105">Here are the steps to authorize your Logic app to connect to your GitHub account:</span></span>

1. <span data-ttu-id="9546b-106">논리 앱 디자이너에서 GitHub에 대한 연결을 만들려면 드롭다운 목록에서 **Microsoft 관리 API 표시**를 선택한 다음 검색 상자에 *GitHub*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-106">To create a connection to GitHub, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *GitHub* in the search box.</span></span> <span data-ttu-id="9546b-107">사용할 트리거 또는 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-107">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-github/github-1.png)
2. <span data-ttu-id="9546b-108">이전에 GitHub에 대한 연결을 만들지 않은 경우 GitHub 자격 증명을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-108">If you haven't created any connections to GitHub before, you'll get prompted to provide your GitHub credentials.</span></span> <span data-ttu-id="9546b-109">이러한 자격 증명을 사용하여 GitHub 계정의 데이터에 연결하도록 논리 앱에 권한을 부여하고 해당 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-109">These credentials will be used to authorize your Logic app to connect to, and access your GitHub account's data:</span></span>  
   ![](./media/connectors-create-api-github/github-2.png)
3. <span data-ttu-id="9546b-110">GitHub 사용자 이름 및 암호를 제공하여 논리 앱에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-110">Provide your GitHub user name and password to authorize your Logic app:</span></span>  
   ![](./media/connectors-create-api-github/github-3.png)   
4. <span data-ttu-id="9546b-111">의도를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-111">Confirm your intentions:</span></span>  
   ![](./media/connectors-create-api-github/github-4.png)   
5. <span data-ttu-id="9546b-112">연결이 포털에 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-112">Notice the connection has been created in the portal.</span></span> <span data-ttu-id="9546b-113">이제 논리 앱을 만들고 그 안에서 GitHub를 사용하여 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9546b-113">You can now proceed with creating your Logic app and using GitHub in it:</span></span>   
   ![](./media/connectors-create-api-github/github-5.png)   

