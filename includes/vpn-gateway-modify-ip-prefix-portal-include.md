### <span data-ttu-id="a81f2-101"><a name="noconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사 게이트웨이 연결 없음</span><span class="sxs-lookup"><span data-stu-id="a81f2-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="a81f2-102">tooadd 추가 주소 접두사:</span><span class="sxs-lookup"><span data-stu-id="a81f2-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="a81f2-103">로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="a81f2-104">Hello에 hello IP 주소 공간 추가 *추가 주소 범위 추가* 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="a81f2-105">클릭 **저장** toosave 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="a81f2-106">tooremove 주소 접두사:</span><span class="sxs-lookup"><span data-stu-id="a81f2-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="a81f2-107">로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="a81f2-108">Hello 클릭 **'...'** tooremove hello 접두사를 포함 하는 hello 줄에 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="a81f2-109">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-109">Click **Remove**.</span></span>
4. <span data-ttu-id="a81f2-110">클릭 **저장** toosave 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="a81f2-111"><a name="withconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사-기존 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="a81f2-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="a81f2-112">게이트웨이 연결 하 고 원하는 tooadd 또는 로컬 네트워크 게이트웨이에 포함 된 hello IP 주소 접두사를 제거 하는 경우 toodo hello 순서에 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="a81f2-113">이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="a81f2-114">IP 주소 접두사를 수정할 때 toodelete hello VPN 게이트웨이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="a81f2-115">Tooremove hello 연결을 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="a81f2-116">1. Hello 연결을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="a81f2-117">로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="a81f2-118">Hello 클릭 **...**  각 연결에 대 한 hello 선에 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="a81f2-119">클릭 **저장** toosave 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="a81f2-120">2. Hello 주소 접두사를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="a81f2-121">tooadd 추가 주소 접두사:</span><span class="sxs-lookup"><span data-stu-id="a81f2-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="a81f2-122">로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="a81f2-123">Hello IP 주소 공간을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="a81f2-124">클릭 **저장** toosave 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="a81f2-125">tooremove 주소 접두사:</span><span class="sxs-lookup"><span data-stu-id="a81f2-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="a81f2-126">로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="a81f2-127">Hello 클릭 **...**  tooremove hello 접두사를 포함 하는 hello 줄에 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="a81f2-128">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-128">Click **Remove**.</span></span>
4. <span data-ttu-id="a81f2-129">클릭 **저장** toosave 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="a81f2-130">3. Hello 연결을 다시 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="a81f2-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="a81f2-131">VNet에 대 한 가상 네트워크 게이트웨이 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="a81f2-132">(하지 hello 로컬 네트워크 게이트웨이입니다.)</span><span class="sxs-lookup"><span data-stu-id="a81f2-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="a81f2-133">Hello에 가상 네트워크 게이트웨이 hello에 **설정** 섹션에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="a81f2-134">Hello 클릭 **+ 추가** tooopen hello **연결 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="a81f2-135">연결을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-135">Recreate your connection.</span></span>
5. <span data-ttu-id="a81f2-136">클릭 **확인** toocreate hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81f2-136">Click **OK** toocreate hello connection.</span></span>
