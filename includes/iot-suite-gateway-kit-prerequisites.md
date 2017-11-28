## <a name="prerequisites"></a><span data-ttu-id="ff5a0-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ff5a0-101">Prerequisites</span></span>

<span data-ttu-id="ff5a0-102">이 자습서를 완료하려면 활성 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ff5a0-103">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ff5a0-104">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="ff5a0-105">필수 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="ff5a0-105">Required software</span></span>

<span data-ttu-id="ff5a0-106">Intel NUC의 명령줄에 원격으로 액세스할 수 있도록 데스크톱 컴퓨터에 SSH 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Intel NUC.</span></span>

- <span data-ttu-id="ff5a0-107">Windows에서는 SSH 클라이언트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="ff5a0-108">[PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="ff5a0-109">대부분의 Linux 배포판 및 Mac OS는 명령줄 SSH 유틸리티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span>

### <a name="required-hardware"></a><span data-ttu-id="ff5a0-110">필수 하드웨어</span><span class="sxs-lookup"><span data-stu-id="ff5a0-110">Required hardware</span></span>

<span data-ttu-id="ff5a0-111">Intel NUC의 명령줄에 원격으로 연결할 수 있는 데스크톱 컴퓨터이며</span><span class="sxs-lookup"><span data-stu-id="ff5a0-111">A desktop computer to enable you to connect remotely to the command line on the Intel NUC.</span></span>

<span data-ttu-id="ff5a0-112">[IoT Commercial Gateway Kit][lnk-starter-kits].</span><span class="sxs-lookup"><span data-stu-id="ff5a0-112">[IoT Commercial Gateway Kit][lnk-starter-kits].</span></span> <span data-ttu-id="ff5a0-113">이 자습서에서는 키트에서 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5a0-113">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="ff5a0-114">4G 메모리 및 Bluetooth 확장 카드를 포함한 Intel® NUC Kit DE3815TYKE</span><span class="sxs-lookup"><span data-stu-id="ff5a0-114">Intel® NUC Kit DE3815TYKE with 4G Memory and Bluetooth expansion card</span></span>
- <span data-ttu-id="ff5a0-115">전원 어댑터</span><span class="sxs-lookup"><span data-stu-id="ff5a0-115">Power adaptor</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/