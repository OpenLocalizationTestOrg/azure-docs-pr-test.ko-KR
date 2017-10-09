## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="cdebc-101">Raspberry Pi 준비</span><span class="sxs-lookup"><span data-stu-id="cdebc-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="cdebc-102">Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="cdebc-102">Install Raspbian</span></span>

<span data-ttu-id="cdebc-103">인 경우 hello 라스베리 Pi를 사용 하는 처음으로 tooinstall hello Raspbian 운영 체제 NOOBS hello 키트에 포함 된 hello SD 카드에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="cdebc-104">hello [라스베리 Pi 소프트웨어 가이드] [ lnk-install-raspbian] 설명 방법을 tooinstall 라스베리 Pi에 운영 체제.</span><span class="sxs-lookup"><span data-stu-id="cdebc-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="cdebc-105">이 자습서 라스베리 원주율 hello Raspbian 운영 체제를 설치 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="cdebc-106">hello에 포함 된 hello SD 카드 [라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트] [ lnk-starter-kits] NOOBS 설치에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="cdebc-107">이 카드의 hello 라스베리 Pi 부팅 수 있으며 tooinstall hello Raspbian 운영 체제를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

<span data-ttu-id="cdebc-108">toocomplete hello 하드웨어 설치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-108">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="cdebc-109">Hello 키트에 포함 된 라스베리 Pi toohello 전원 공급 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-109">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="cdebc-110">키트에 포함 된 hello 이더넷 케이블을 사용 하 여 라스베리 Pi tooyour 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-110">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="cdebc-111">또는 Raspberry Pi에 대해 [무선 연결][lnk-pi-wireless]을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="cdebc-112">이제 hello 하드웨어를 라스베리 Pi의 설치를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-112">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="cdebc-113">로그인 및 액세스 hello 터미널</span><span class="sxs-lookup"><span data-stu-id="cdebc-113">Sign in and access hello terminal</span></span>

<span data-ttu-id="cdebc-114">환경을 사용 하는 두 가지 옵션 tooaccess 터미널 라스베리 원주율:</span><span class="sxs-lookup"><span data-stu-id="cdebc-114">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="cdebc-115">키보드 연결된 tooyour 라스베리 Pi를 모니터링 하는 경우에 hello Raspbian GUI tooaccess 터미널 윈도우를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-115">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="cdebc-116">액세스 hello 명령줄 데스크톱 컴퓨터의 SSH를 사용 하 여 라스베리 원주율입니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-116">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="cdebc-117">Hello GUI에서에서 터미널 윈도우를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cdebc-117">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="cdebc-118">Raspbian에 대 한 hello 기본 자격 증명이 username **pi** 및 암호 **라스베리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-118">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="cdebc-119">Hello GUI에에서 hello 작업 표시줄에서 hello를 시작할 수 있습니다 **터미널** hello 모양의 아이콘을 모니터를 사용 하 여 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-119">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="cdebc-120">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="cdebc-120">Sign in with SSH</span></span>

<span data-ttu-id="cdebc-121">명령줄 액세스 tooyour 라스베리 Pi에 대 한 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-121">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="cdebc-122">hello 문서 [SSH (보안 셸)] [ lnk-pi-ssh] 설명 방법을 tooconfigure 라스베리 Pi와의 SSH 방법과에서 tooconnect [Windows] [ lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-122">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="cdebc-123">사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="cdebc-124">선택 사항: Raspberry Pi의 폴더 공유</span><span class="sxs-lookup"><span data-stu-id="cdebc-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="cdebc-125">필요에 따라 데스크톱 환경 라스베리 원주율 tooshare 폴더를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-125">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="cdebc-126">공유 폴더를 사용 하면 있습니다 toouse 데스크톱 원하는 텍스트 편집기 (예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime 텍스트](http://www.sublimetext.com/)) tooedit 파일을 사용 하는 대신 프로그램 라스베리 Pi `nano` 또는 `vi`.</span><span class="sxs-lookup"><span data-stu-id="cdebc-126">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="cdebc-127">Windows와 함께 폴더 tooshare hello 라스베리 Pi에서 Samba 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-127">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="cdebc-128">또는 기본 제공 hello를 사용 하 여 [SFTP](https://www.raspberrypi.org/documentation/remote-access/) 바탕 화면에 SFTP 클라이언트와 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="cdebc-128">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/