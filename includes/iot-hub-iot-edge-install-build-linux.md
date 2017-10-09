## <a name="install-hello-prerequisites"></a><span data-ttu-id="ae27f-101">Hello 필수 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="ae27f-101">Install hello prerequisites</span></span>

<span data-ttu-id="ae27f-102">이 자습서의 단계에서는 hello Ubuntu Linux를 실행 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="ae27f-103">셸을 열고 다음 명령을 tooinstall hello에 대 한 필수 구성 요소 패키지가 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="ae27f-104">Hello 셸에서 hello 명령 tooclone hello Azure IoT 가장자리 GitHub 리포지토리 tooyour 로컬 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="ae27f-105">Toobuild 샘플 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ae27f-105">How toobuild hello sample</span></span>

<span data-ttu-id="ae27f-106">이제 빌드할 수 hello IoT 가장자리 런타임 및 샘플 로컬 컴퓨터에서:</span><span class="sxs-lookup"><span data-stu-id="ae27f-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="ae27f-107">셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-107">Open a shell.</span></span>

1. <span data-ttu-id="ae27f-108">Hello의 로컬 복사본에 toohello 루트 폴더를 이동 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="ae27f-109">빌드 스크립트를 다음과 같이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="ae27f-110">이 스크립트를 사용 하는 **cmake** 폴더 라는 유틸리티 toocreate **빌드** hello 루트 폴더의 로컬 복사본에는 **iot 가장자리** 리포지토리 메이크파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="ae27f-111">hello 스크립트는 다음 단위 테스트 및 최종 tooend 테스트 건너뛰기 hello 솔루션을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="ae27f-112">원하는 toobuild hello 단위 테스트를 실행 하는 경우 추가 hello `--run-unittests` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="ae27f-113">원하는 toobuild hello 끝 tooend 테스트를 실행 하는 경우 추가 hello `--run-e2e-tests`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="ae27f-114">Hello를 실행할 때마다 **build.sh** 스크립트를 삭제 하 고 다음 hello를 다시 만듭니다 **빌드** hello의 로컬 복사본의 hello 루트 폴더에 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="ae27f-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
