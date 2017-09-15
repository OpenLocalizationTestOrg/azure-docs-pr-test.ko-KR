<span data-ttu-id="a8e5f-101">Azure는 **다음 조건 모두가 참일 경우**응용 프로그램에서 Python을 사용하도록 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="a8e5f-102">루트 폴더에 있는 requirements.txt 파일</span><span class="sxs-lookup"><span data-stu-id="a8e5f-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="a8e5f-103">루트 폴더에 있는 .py 파일이나 python을 지정하는 runtime.txt</span><span class="sxs-lookup"><span data-stu-id="a8e5f-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="a8e5f-104">이런 경우, Python 특정 배포 스크립트가 사용되어 파일 표준 동기화뿐만 아니라 다음과 같은 추가 Python 작업도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="a8e5f-105">가상 환경 자동 관리</span><span class="sxs-lookup"><span data-stu-id="a8e5f-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="a8e5f-106">pip를 사용하여 requirements.txt에 나열된 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="a8e5f-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="a8e5f-107">선택한 Python 버전에 따라 적절한 web.config 만들기</span><span class="sxs-lookup"><span data-stu-id="a8e5f-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="a8e5f-108">Django 응용 프로그램에 대한 정적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="a8e5f-108">Collect static files for Django applications</span></span>

<span data-ttu-id="a8e5f-109">스크립트를 사용자 지정하지 않고도 기본 배포 단계의 특정 측면을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="a8e5f-110">모든 Python 특정 배포 단계를 건너뛰려는 경우, 다음과 같은 빈 파일을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="a8e5f-111">배포를 더 효율적으로 제어하려면 다음 파일을 만들어 기본 배포 스크립트를 재정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-111">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="a8e5f-112">사용할 수는 [Azure 명령줄 인터페이스] [ Azure command-line interface] 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-112">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="a8e5f-113">프로젝트 폴더에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="a8e5f-114">이러한 파일이 존재하지 않으면 Azure는 임시 배포 스크립트를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="a8e5f-115">위의 명령을 사용하여 만드는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5f-115">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
