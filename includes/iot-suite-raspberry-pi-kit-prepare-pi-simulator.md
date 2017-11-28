## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="5d2c7-101">Raspberry Pi 준비</span><span class="sxs-lookup"><span data-stu-id="5d2c7-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="5d2c7-102">Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="5d2c7-102">Install Raspbian</span></span>

<span data-ttu-id="5d2c7-103">처음으로 Raspberry Pi를 사용하는 경우 키트에 포함된 SD 카드에서 NOOBS를 사용하여 Raspbian 운영 체제를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="5d2c7-104">[Raspberry Pi 소프트웨어 가이드][lnk-install-raspbian]는 Raspberry Pi에 운영 체제를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="5d2c7-105">이 자습서에서는 Raspberry Pi에 Raspbian 운영 체제를 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="5d2c7-106">[Raspberry Pi 3용 Microsoft Azure IoT 시작 키트][lnk-starter-kits]에 포함된 SD 카드에는 이미 NOOBS가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="5d2c7-107">이 카드에서 Raspberry Pi를 부팅할 수 있으며 Raspbian OS를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

<span data-ttu-id="5d2c7-108">하드웨어 설정을 완료하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-108">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="5d2c7-109">Raspberry Pi를 키트에 포함된 전원 공급 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-109">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="5d2c7-110">키트에 포함된 이더넷 케이블을 사용하여 Raspberry Pi를 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-110">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="5d2c7-111">또는 Raspberry Pi에 대해 [무선 연결][lnk-pi-wireless]을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="5d2c7-112">이제 Raspberry Pi의 하드웨어 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-112">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="5d2c7-113">터미널 로그인 및 액세스</span><span class="sxs-lookup"><span data-stu-id="5d2c7-113">Sign in and access the terminal</span></span>

<span data-ttu-id="5d2c7-114">Raspberry Pi의 터미널 환경에 액세스하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-114">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="5d2c7-115">키보드 및 모니터가 Raspberry Pi에 연결된 경우 Raspbian GUI를 사용하여 터미널 창에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-115">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="5d2c7-116">데스크톱 컴퓨터에서 SSH를 사용하여 Raspberry Pi의 명령줄에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-116">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="5d2c7-117">GUI에서 터미널 창 사용</span><span class="sxs-lookup"><span data-stu-id="5d2c7-117">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="5d2c7-118">Raspbian에 대한 기본 자격 증명은 사용자 이름 **pi** 및 암호 **raspberry**입니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-118">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="5d2c7-119">GUI의 작업 표시줄에서 모니터 모양의 아이콘을 사용하여 **터미널** 유틸리티를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-119">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="5d2c7-120">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="5d2c7-120">Sign in with SSH</span></span>

<span data-ttu-id="5d2c7-121">Raspberry Pi에 명령줄 액세스를 위해 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-121">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="5d2c7-122">[SSH(Secure Shell)][lnk-pi-ssh] 문서에서는 Raspberry Pi에서 SSH를 구성하는 방법 및 [Windows][lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]에서 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-122">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="5d2c7-123">사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="5d2c7-124">선택 사항: Raspberry Pi의 폴더 공유</span><span class="sxs-lookup"><span data-stu-id="5d2c7-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="5d2c7-125">필요에 따라 다음 데스크톱 환경을 사용하여 Raspberry Pi의 폴더를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-125">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="5d2c7-126">폴더를 공유하면 `nano` 또는 `vi`을 사용하는 대신 원하는 데스크톱 텍스트 편집기(예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime Text](http://www.sublimetext.com/))를 사용하여 Raspberry Pi의 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-126">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="5d2c7-127">Windows 폴더를 공유하려면 Raspberry Pi Samba 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-127">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="5d2c7-128">데스크톱에서 SFTP 클라이언트를 포함한 기본 제공 [SFTP](https://www.raspberrypi.org/documentation/remote-access/) 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d2c7-128">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/