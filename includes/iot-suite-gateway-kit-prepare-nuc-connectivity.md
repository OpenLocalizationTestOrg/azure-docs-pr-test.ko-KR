## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="bdcf0-101">Intel NUC 준비</span><span class="sxs-lookup"><span data-stu-id="bdcf0-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="bdcf0-102">toocomplete hello 하드웨어 설치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-102">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="bdcf0-103">Hello 키트에 포함 된 Intel NUC toohello 전원 공급 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-103">Connect your Intel NUC toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="bdcf0-104">이더넷 케이블을 사용 하 여 Intel NUC tooyour 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-104">Connect your Intel NUC tooyour network using an Ethernet cable.</span></span>

<span data-ttu-id="bdcf0-105">이제 Intel NUC 게이트웨이 장치 hello 하드웨어 설치를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-105">You have now completed hello hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="bdcf0-106">로그인 및 액세스 hello 터미널</span><span class="sxs-lookup"><span data-stu-id="bdcf0-106">Sign in and access hello terminal</span></span>

<span data-ttu-id="bdcf0-107">환경을 사용 하는 두 가지 옵션 tooaccess 터미널 Intel NUC에:</span><span class="sxs-lookup"><span data-stu-id="bdcf0-107">You have two options tooaccess a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="bdcf0-108">키보드 연결 된 tooyour Intel NUC를 모니터링 하는 경우에 hello 셸 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-108">If you have a keyboard and monitor connected tooyour Intel NUC, you can access hello shell directly.</span></span> <span data-ttu-id="bdcf0-109">hello 기본 자격 증명이 username **루트** 및 암호 **루트**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-109">hello default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="bdcf0-110">Hello 셸 데스크톱 컴퓨터의 SSH를 사용 하 여 Intel NUC에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-110">Access hello shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="bdcf0-111">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="bdcf0-111">Sign in with SSH</span></span>

<span data-ttu-id="bdcf0-112">SSH 사용 하 여 toosign, Intel NUC의 hello IP 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-112">toosign in with SSH, you need hello IP address of your Intel NUC.</span></span> <span data-ttu-id="bdcf0-113">키보드 연결 된 tooyour Intel NUC 모니터링을 사용 하 여 hello `ifconfig` toofind hello IP 주소가 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-113">If you have a keyboard and monitor connected tooyour Intel NUC, use hello `ifconfig` command toofind hello IP address.</span></span> <span data-ttu-id="bdcf0-114">또는 tooyour 라우터 toolist hello 주소의 네트워크 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-114">Alternatively, connect tooyour router toolist hello addresses of devices on your network.</span></span>

<span data-ttu-id="bdcf0-115">사용자 이름 **root** 및 암호 **root**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="bdcf0-116">선택 사항: Intel NUC에서 폴더 공유</span><span class="sxs-lookup"><span data-stu-id="bdcf0-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="bdcf0-117">필요에 따라 데스크톱 환경에 Intel NUC tooshare 폴더를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-117">Optionally, you may want tooshare a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="bdcf0-118">공유 폴더를 사용 하면 있습니다 toouse 데스크톱 원하는 텍스트 편집기 (예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime 텍스트](http://www.sublimetext.com/)) tooedit 파일을 사용 하는 대신 Intel NUC 프로그램 `nano` 또는 `vi`.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-118">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="bdcf0-119">Intel NUC hello에 Samba 서버를 구성 하는 Windows와 함께 폴더 tooshare 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-119">tooshare a folder with Windows, configure a Samba server on hello Intel NUC.</span></span> <span data-ttu-id="bdcf0-120">또는 hello Intel NUC 데스크톱 컴퓨터에서 SFTP 클라이언트를에 hello SFTP 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdcf0-120">Alternatively, use hello SFTP server on hello Intel NUC with an SFTP client on your desktop machine.</span></span>
