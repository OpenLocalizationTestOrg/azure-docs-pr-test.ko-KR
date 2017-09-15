## <a name="set-up-the-development-environment"></a><span data-ttu-id="76750-101">개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="76750-101">Set up the development environment</span></span>

<span data-ttu-id="76750-102">이 섹션에서는 ASP.NET MVC 앱 만들기, 연결된 서비스 연결 추가, 컨트롤러 추가 및 필수 네임스페이스 지시문 지정을 포함한 개발 환경 설정에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying the required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="76750-103">ASP.NET MVC 앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="76750-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="76750-104">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76750-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="76750-105">기본 메뉴에서 **파일->새로 만들기->프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-105">Select **File->New->Project** from the main menu</span></span>

1. <span data-ttu-id="76750-106">**새 프로젝트** 대화 상자에서 다음 그림에서 강조 표시한 대로 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-106">On the **New Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![ASP.NET 프로젝트 만들기](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="76750-108">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-108">Select **OK**.</span></span>

1. <span data-ttu-id="76750-109">**새 ASP.NET 프로젝트** 대화 상자에서 다음 그림에서 강조 표시한 대로 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-109">On the **New ASP.NET Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![MVC 지정](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="76750-111">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-111">Select **OK**.</span></span>

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a><span data-ttu-id="76750-112">연결된 서비스를 사용하여 Azure 저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="76750-112">Use Connected Services to connect to an Azure storage account</span></span>

1. <span data-ttu-id="76750-113">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->연결된 서비스**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-113">In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="76750-114">**연결된 서비스 추가** 대화 상자에서 **Azure Storage**를 선택한 다음 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-114">On the **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![연결된 서비스 대화 상자](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="76750-116">**Azure Storage** 대화 상자에서 작업하려는 Azure 저장소 계정을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76750-116">On the **Azure Storage** dialog, select the desired Azure storage account with which you want to work, and select **Add**.</span></span>
