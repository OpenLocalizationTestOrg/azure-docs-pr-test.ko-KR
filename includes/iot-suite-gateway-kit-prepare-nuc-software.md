## <a name="build-iot-edge"></a><span data-ttu-id="56074-101">IoT Edge 빌드</span><span class="sxs-lookup"><span data-stu-id="56074-101">Build IoT Edge</span></span>

<span data-ttu-id="56074-102">이 자습서에서는 미리 구성 된 솔루션 모니터링 원격 hello로 IoT 가장자리 모듈 toocommunicate 사용자 지정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="56074-103">따라서 사용자 지정 소스 코드에서 toobuild hello IoT 가장자리 모듈을 검색 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="56074-104">다음 섹션 hello tooinstall IoT Edge 및 빌드 사용자 지정 IoT 지 모듈 hello 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="56074-105">IoT Edge 설치</span><span class="sxs-lookup"><span data-stu-id="56074-105">Install IoT Edge</span></span>

<span data-ttu-id="56074-106">hello 다음 단계로 진행 tooinstall hello Intel NUC hello에 대 한 IoT 가장자리 소프트웨어를 미리 컴파일 방식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56074-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="56074-107">Hello 나오는 Intel NUC hello에 명령을 실행 하 여 필요한 hello 스마트 패키지 저장소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="56074-108">입력 `y` 때 hello 명령은 묻는 너무**이 채널을 포함?**합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="56074-109">Hello 다음 명령을 실행 하 여 hello 스마트 패키지 관리자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="56074-110">Hello 다음 명령을 실행 하 여 hello Azure IoT 가장자리 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="56074-111">Hello "Hello world" 예제를 실행 하 여 hello 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="56074-112">이 샘플 5 초 마다 hello world 메시지 toohello log.txT 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="56074-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="56074-113">hello 다음 명령이 실행 hello "Hello world" 예제 추가 정보:</span><span class="sxs-lookup"><span data-stu-id="56074-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="56074-114">무시 **잘못 된 인수** hello 예제를 중지 하면 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="56074-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="56074-115">Hello 로그 파일의 명령을 tooview hello 내용을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="56074-116">문제 해결</span><span class="sxs-lookup"><span data-stu-id="56074-116">Troubleshooting</span></span>

<span data-ttu-id="56074-117">Hello 오류가 나타나면 "패키지가 util-linux-dev", 제공 Intel NUC hello를 다시 부팅을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="56074-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
