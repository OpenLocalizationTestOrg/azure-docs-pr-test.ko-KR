<span data-ttu-id="6cfca-101">Azure는 **다음 조건 모두가 참일 경우**응용 프로그램에서 Python을 사용하도록 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="6cfca-102">requirements.txt 파일 hello 루트 폴더</span><span class="sxs-lookup"><span data-stu-id="6cfca-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="6cfca-103">hello 루트 폴더에 모든.py 파일 또는 runtime.txt python을 지정 하는</span><span class="sxs-lookup"><span data-stu-id="6cfca-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="6cfca-104">않은 hello 경우와 같은 추가 Python 작업 뿐만 아니라 파일, hello 표준 동기화를 수행 하는 Python 특정 배포 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="6cfca-105">가상 환경 자동 관리</span><span class="sxs-lookup"><span data-stu-id="6cfca-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="6cfca-106">pip를 사용하여 requirements.txt에 나열된 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="6cfca-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="6cfca-107">Hello에 따라 hello 적절 한 web.config의 생성 Python 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="6cfca-108">Django 응용 프로그램에 대한 정적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="6cfca-108">Collect static files for Django applications</span></span>

<span data-ttu-id="6cfca-109">Toocustomize hello 스크립트 필요 없이 hello 기본 배포 단계의 특정 측면을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="6cfca-110">모든 Python 특정 배포 단계 tooskip 하려는 경우에이 빈 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="6cfca-111">Django 응용 프로그램에 대 한 정적 파일의 tooskip 컬렉션 하려면:</span><span class="sxs-lookup"><span data-stu-id="6cfca-111">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="6cfca-112">배포 보다 자세히 제어는 다음 파일이 hello를 만들어서 hello 기본 배포 스크립트를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-112">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="6cfca-113">Hello를 사용할 수 있습니다 [Azure 명령줄 인터페이스] [ Azure command-line interface] toocreate hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-113">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="6cfca-114">프로젝트 폴더에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="6cfca-115">이러한 파일이 존재하지 않으면 Azure는 임시 배포 스크립트를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="6cfca-116">것이 동일한 toohello 위의 hello 명령으로 만들 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cfca-116">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
