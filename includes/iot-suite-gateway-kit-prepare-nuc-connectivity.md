## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="acc6f-101">Intel NUC 준비</span><span class="sxs-lookup"><span data-stu-id="acc6f-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="acc6f-102">하드웨어 설정을 완료하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-102">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="acc6f-103">Intel NUC를 키트에 포함된 전원 공급 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-103">Connect your Intel NUC to the power supply included in the kit.</span></span>
- <span data-ttu-id="acc6f-104">이더넷 케이블을 사용하여 Intel NUC를 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-104">Connect your Intel NUC to your network using an Ethernet cable.</span></span>

<span data-ttu-id="acc6f-105">이제 Intel NUC 게이트웨이 장치의 하드웨어 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-105">You have now completed the hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="acc6f-106">터미널 로그인 및 액세스</span><span class="sxs-lookup"><span data-stu-id="acc6f-106">Sign in and access the terminal</span></span>

<span data-ttu-id="acc6f-107">Intel NUC의 터미널 환경에 액세스하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-107">You have two options to access a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="acc6f-108">Intel NUC에 연결된 키보드 및 모니터가 있는 경우 셸에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-108">If you have a keyboard and monitor connected to your Intel NUC, you can access the shell directly.</span></span> <span data-ttu-id="acc6f-109">기본 자격 증명은 사용자 이름 **root** 및 암호 **root**입니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-109">The default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="acc6f-110">데스크톱 컴퓨터에서 SSH를 사용하여 Intel NUC의 셸에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-110">Access the shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="acc6f-111">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="acc6f-111">Sign in with SSH</span></span>

<span data-ttu-id="acc6f-112">SSH를 사용하여 로그인하려면 Intel NUC의 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-112">To sign in with SSH, you need the IP address of your Intel NUC.</span></span> <span data-ttu-id="acc6f-113">Intel NUC에 연결된 키보드 및 모니터가 있는 경우 `ifconfig` 명령을 사용하여 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-113">If you have a keyboard and monitor connected to your Intel NUC, use the `ifconfig` command to find the IP address.</span></span> <span data-ttu-id="acc6f-114">또는 라우터에 연결하여 네트워크에서 장치의 주소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-114">Alternatively, connect to your router to list the addresses of devices on your network.</span></span>

<span data-ttu-id="acc6f-115">사용자 이름 **root** 및 암호 **root**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="acc6f-116">선택 사항: Intel NUC에서 폴더 공유</span><span class="sxs-lookup"><span data-stu-id="acc6f-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="acc6f-117">필요에 따라 다음 데스크톱 환경을 사용하여 Intel NUC의 폴더를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-117">Optionally, you may want to share a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="acc6f-118">폴더를 공유하면 `nano` 또는 `vi`를 사용하는 대신 원하는 데스크톱 텍스트 편집기(예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime Text](http://www.sublimetext.com/))를 사용하여 Intel NUC의 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-118">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="acc6f-119">Windows 폴더를 공유하려면 Intel NUC에서 Samba 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-119">To share a folder with Windows, configure a Samba server on the Intel NUC.</span></span> <span data-ttu-id="acc6f-120">또는 데스크톱 컴퓨터에서 SFTP 클라이언트를 통해 Intel NUC의 SFTP 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acc6f-120">Alternatively, use the SFTP server on the Intel NUC with an SFTP client on your desktop machine.</span></span>
