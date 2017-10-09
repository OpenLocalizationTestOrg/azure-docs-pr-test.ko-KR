#### <a name="prerequisites"></a><span data-ttu-id="5ffdd-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5ffdd-101">Prerequisites</span></span>
* <span data-ttu-id="5ffdd-102">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5ffdd-102">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5ffdd-103">[OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) 계정</span><span class="sxs-lookup"><span data-stu-id="5ffdd-103">A [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) account</span></span> 

<span data-ttu-id="5ffdd-104">OneDrive 계정에 논리 앱을 사용 하려면 먼저 hello 논리 앱 tooconnect tooyour OneDrive 계정에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-104">Before you can use your OneDrive account in a logic app, authorize hello logic app tooconnect tooyour OneDrive account.</span></span>  <span data-ttu-id="5ffdd-105">Hello Azure 포털에서 논리 앱 내에서이 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-105">You can do this easily within your logic app on hello Azure portal.</span></span> 

<span data-ttu-id="5ffdd-106">단계를 수행 하는 hello를 사용 하 여 논리 앱 tooconnect tooyour OneDrive 계정에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-106">Authorize your logic app tooconnect tooyour OneDrive account using hello following steps:</span></span>

1. <span data-ttu-id="5ffdd-107">논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-107">Create a logic app.</span></span> <span data-ttu-id="5ffdd-108">Hello 논리 앱 디자이너에서 선택 **표시 Microsoft 관리 되는 Api** hello에 드롭다운 목록에서 선택한 다음 hello 검색 상자에 "onedrive"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-108">In hello Logic Apps designer, select **Show Microsoft managed APIs** in hello drop down list, and then enter "onedrive" in hello search box.</span></span> <span data-ttu-id="5ffdd-109">Hello 트리거 또는 동작 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-109">Select one of hello triggers or actions:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="5ffdd-110">모든 연결 tooOneDrive 이전에 만든 하지 않은 경우 사용자는 OneDrive 자격 증명을 사용 하 여 증명된 toosign:</span><span class="sxs-lookup"><span data-stu-id="5ffdd-110">If you haven't previously created any connections tooOneDrive, you are prompted toosign in using your OneDrive credentials:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-2.png)
3. <span data-ttu-id="5ffdd-111">**로그인**을 선택하고 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-111">Select **Sign in**, and enter your user name and password.</span></span> <span data-ttu-id="5ffdd-112">**로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-112">Select **Sign in**:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-3.png)   
   
    <span data-ttu-id="5ffdd-113">이러한 자격 증명 사용 되는 tooauthorize 하 여 논리 앱 tooconnect 되며 hello 데이터 OneDrive 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-113">These credentials are used tooauthorize your logic app tooconnect to, and access hello data in your OneDrive account.</span></span> 
4. <span data-ttu-id="5ffdd-114">선택 **예** tooauthorize hello 논리 앱 toouse OneDrive 계정:</span><span class="sxs-lookup"><span data-stu-id="5ffdd-114">Select **Yes** tooauthorize hello logic app toouse your OneDrive account:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-4.png)   
5. <span data-ttu-id="5ffdd-115">공지 hello 연결이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffdd-115">Notice hello connection has been created.</span></span> <span data-ttu-id="5ffdd-116">이제 진행할 논리 앱의 단계를 다른 hello:</span><span class="sxs-lookup"><span data-stu-id="5ffdd-116">Now, proceed with hello other steps in your logic app:</span></span>  
   ![](./media/connectors-create-api-onedrive/onedrive-5.png)

