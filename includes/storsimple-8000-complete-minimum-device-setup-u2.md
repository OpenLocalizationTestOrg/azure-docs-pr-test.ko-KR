<!--author=alkohli last changed: 01/12/17-->

#### <a name="to-complete-the-minimum-storsimple-device-setup"></a><span data-ttu-id="da3a3-101">최소 StorSimple 장치 설치를 완료하려면</span><span class="sxs-lookup"><span data-stu-id="da3a3-101">To complete the minimum StorSimple device setup</span></span>

   > [!NOTE]
   > <span data-ttu-id="da3a3-102">최소 장치 설정이 완료되면 장치 이름을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-102">You cannot change the device name once the minimum device setup is completed.</span></span>
   
1. <span data-ttu-id="da3a3-103">**장치** 블레이드의 테이블 형식 장치 목록에서 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-103">From the tabular listing of devices in the **Devices** blade, select and click your device.</span></span> <span data-ttu-id="da3a3-104">장치가 **설정 준비 완료** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-104">The device is in a **Ready to set up** state.</span></span> <span data-ttu-id="da3a3-105">**장치 구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-105">The **Configure device** blade opens up.</span></span>

     ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. <span data-ttu-id="da3a3-107">**장치 구성** 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="da3a3-107">In the **Configure device** blade:</span></span>
   
   1. <span data-ttu-id="da3a3-108">장치의 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-108">Supply a **friendly name** for your device.</span></span> <span data-ttu-id="da3a3-109">기본 장치 이름은 장치 모델 및 일련 번호와 같은 정보를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-109">The default device name reflects information such as the device model and serial number.</span></span> <span data-ttu-id="da3a3-110">최대 64자의 친숙한 이름을 할당하여 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-110">You can assign a friendly name of up to 64 characters to manage your device.</span></span>
   2. <span data-ttu-id="da3a3-111">장치가 배포되는 지리적 위치에 기반한 **표준 시간대** 를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-111">Set the **time zone** based on the geographic location in which the device is being deployed.</span></span> <span data-ttu-id="da3a3-112">장치는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-112">Your device uses this time zone for all scheduled operations.</span></span>
   3. <span data-ttu-id="da3a3-113">**DATA 0 설정** 아래에서:</span><span class="sxs-lookup"><span data-stu-id="da3a3-113">Under the **DATA 0 settings**:</span></span>

       1. <span data-ttu-id="da3a3-114">데이터 0 네트워크 인터페이스는 설치 마법사를 통해 구성된 네트워크 설정(IP, 서브넷, 게이트웨이)이 활성화된 대로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-114">Your DATA 0 network interface shows as enabled with the network settings (IP, subnet, gateway) configured via the setup wizard.</span></span> <span data-ttu-id="da3a3-115">또한 데이터 0은 클라우드뿐만 아니라 iSCSI에 대해서도 자동으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-115">DATA 0 is also automatically enabled for cloud as well as iSCSI.</span></span>

       2. <span data-ttu-id="da3a3-116">컨트롤러 0과 컨트롤러 1에 대한 고정 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-116">Provide the fixed IP addresses for Controller 0 and Controller 1.</span></span> <span data-ttu-id="da3a3-117">**컨트롤러 고정 IP 주소는 장치 IP 주소를 통해 접근할 수 있는 서브넷 내의 사용 가능한 IP여야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="da3a3-117">**The controller fixed IP addresses need to be free IPs within the subnet accessible by the device IP address.**</span></span> <span data-ttu-id="da3a3-118">데이터 0 인터페이스가 IPv4에 대해 구성된 경우 고정 IP 주소는 IPv4 형식으로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-118">If the DATA 0 interface was configured for IPv4, the fixed IP addresses need to be provided in the IPv4 format.</span></span> <span data-ttu-id="da3a3-119">IPv6 구성에 대한 접두사를 제공하는 경우 고정 IP 주소는 이러한 필드에 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-119">If you provided a prefix for IPv6 configuration, the fixed IP addresses are populated automatically in these fields.</span></span>

            ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            <span data-ttu-id="da3a3-121">컨트롤러의 고정 IP 주소는 장치에 대한 업데이트를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-121">The fixed IP addresses for the controller are used for servicing the updates to the device.</span></span> <span data-ttu-id="da3a3-122">따라서 고정 IP는 라우팅 가능하고 인터넷에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-122">Therefore, the fixed IPs must be routable and able to connect to the Internet.</span></span> <span data-ttu-id="da3a3-123">[Test-HcsmConnection][Test] cmdlet을 사용하여 고정된 컨트롤러 IP가 라우팅할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-123">You can check that your fixed controller IPs are routable by using the [Test-HcsmConnection][Test] cmdlet.</span></span> <span data-ttu-id="da3a3-124">다음 예제는 고정된 컨트롤러 IP가 인터넷으로 라우팅되고 Microsoft 업데이트 서버에 액세스할 수 있음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-124">The following example shows fixed controller IPs are routed to the Internet and can access the Microsoft Update servers.</span></span>

            ![라우팅 가능한 IP를 표시하는 Test-HcsmConnection](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. <span data-ttu-id="da3a3-126">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-126">Click **OK**.</span></span> <span data-ttu-id="da3a3-127">장치 구성이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-127">The device configuration starts.</span></span> <span data-ttu-id="da3a3-128">장치 구성이 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-128">When the device configuration is complete, you are notified.</span></span> <span data-ttu-id="da3a3-129">장치 상태가 **장치** 블레이드에서 **온라인**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3a3-129">The device status changes to **Online** in the **Devices** blade.</span></span>

    ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
