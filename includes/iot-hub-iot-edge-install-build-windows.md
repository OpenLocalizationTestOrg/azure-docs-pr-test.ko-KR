## <a name="install-hello-prerequisites"></a><span data-ttu-id="57eaf-101">Hello 필수 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="57eaf-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="57eaf-102">[Visual Studio 2015 또는 2017](https://www.visualstudio.com)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="57eaf-103">Hello를 사용할 수 있습니다 hello 라이선스 요구 사항을 충족 하는 경우 Community Edition을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="57eaf-104">있는지 tooinclude Visual c + + 및 NuGet 패키지 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="57eaf-105">설치 [git](http://www.git-scm.com) git.exe hello 명령줄에서 실행할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="57eaf-106">설치 [CMake](https://cmake.org/download/) cmake.exe hello 명령줄에서 실행할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="57eaf-107">CMake 버전 3.7.2 이상을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="57eaf-108">hello **.msi** 설치 관리자가 windows hello 가장 쉬운 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="57eaf-109">CMake toohello 추가 hello 설치 관리자의 메시지에 따라 최소한 현재 사용자를 hello에 대 한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="57eaf-110">[Python 2.7](https://www.python.org/downloads/release/python-27)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="57eaf-111">추가 Python tooyour `PATH` 환경 변수를 **제어판-> 시스템-> 고급 시스템 설정에는 환경 변수->**합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="57eaf-112">명령 프롬프트에서 명령을 tooclone hello Azure IoT 가장자리 GitHub 리포지토리 tooyour 로컬 컴퓨터를 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="57eaf-113">Toobuild 샘플 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="57eaf-113">How toobuild hello sample</span></span>

<span data-ttu-id="57eaf-114">이제 빌드할 수 hello IoT 가장자리 런타임 및 샘플 로컬 컴퓨터에서:</span><span class="sxs-lookup"><span data-stu-id="57eaf-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="57eaf-115">**VS 2015용 개발자 명령 프롬프트** 또는 **VS 2017용 개발자 명령 프롬프트** 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="57eaf-116">Hello의 로컬 복사본에 toohello 루트 폴더를 이동 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="57eaf-117">빌드 스크립트를 다음과 같이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="57eaf-118">이 스크립트는 Visual Studio 솔루션 파일을 만듭니다. 고 hello 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="57eaf-119">Hello에서 hello Visual Studio 솔루션을 찾을 수 있습니다 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="57eaf-120">원하는 toobuild hello 단위 테스트를 실행 하는 경우 추가 hello `--run-unittests` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="57eaf-121">원하는 toobuild hello 끝 tooend 테스트를 실행 하는 경우 추가 hello `--run-e2e-tests`합니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="57eaf-122">Hello를 실행할 때마다 **build.cmd** 스크립트를 삭제 하 고 다음 hello를 다시 만듭니다 **빌드** hello의 로컬 복사본의 hello 루트 폴더에 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="57eaf-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
