1. <span data-ttu-id="3a956-101">보호하려는 서버의 로컬 폴더(예: /tmp)에 설치 관리자를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-101">Copy the installer to a local folder (for example, /tmp) on the server that you want to protect.</span></span> <span data-ttu-id="3a956-102">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-102">In a terminal, run the following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="3a956-103">모바일 서비스를 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-103">To install Mobility Service, run the following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="3a956-104">설치가 완료되면 모바일 서비스를 구성 서버에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-104">Once installation is complete, the Mobility Service needs to get registered to the configuration server.</span></span> <span data-ttu-id="3a956-105">다음 명령을 실행하여 모바일 서비스를 구성 서버에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-105">Run the following command to register the Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="3a956-106">모바일 서비스 설치 관리자 명령줄</span><span class="sxs-lookup"><span data-stu-id="3a956-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="3a956-107">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-107">Parameter</span></span>|<span data-ttu-id="3a956-108">형식</span><span class="sxs-lookup"><span data-stu-id="3a956-108">Type</span></span>|<span data-ttu-id="3a956-109">설명</span><span class="sxs-lookup"><span data-stu-id="3a956-109">Description</span></span>|<span data-ttu-id="3a956-110">가능한 값</span><span class="sxs-lookup"><span data-stu-id="3a956-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="3a956-111">-r</span><span class="sxs-lookup"><span data-stu-id="3a956-111">-r</span></span> |<span data-ttu-id="3a956-112">필수</span><span class="sxs-lookup"><span data-stu-id="3a956-112">Mandatory</span></span>|<span data-ttu-id="3a956-113">MS(모바일 서비스) 설치 여부 또는 MT(마스터 대상) 설치 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="3a956-114">MS</span><span class="sxs-lookup"><span data-stu-id="3a956-114">MS</span></span> </br> <span data-ttu-id="3a956-115">MT</span><span class="sxs-lookup"><span data-stu-id="3a956-115">MT</span></span>|
|<span data-ttu-id="3a956-116">일시 중지되고</span><span class="sxs-lookup"><span data-stu-id="3a956-116">-d</span></span> |<span data-ttu-id="3a956-117">옵션</span><span class="sxs-lookup"><span data-stu-id="3a956-117">Optional</span></span>|<span data-ttu-id="3a956-118">모바일 서비스를 설치하는 위치</span><span class="sxs-lookup"><span data-stu-id="3a956-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="3a956-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="3a956-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="3a956-120">-v</span><span class="sxs-lookup"><span data-stu-id="3a956-120">-v</span></span>|<span data-ttu-id="3a956-121">필수</span><span class="sxs-lookup"><span data-stu-id="3a956-121">Mandatory</span></span>|<span data-ttu-id="3a956-122">모바일 서비스가 설치되는 플랫폼을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-122">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="3a956-123">- **VMware**: *VMware vSphere ESXi 호스트*, *Hyper-V 호스트* 및 *물리적 서버*에서 실행되는 VM에 모바일 서비스를 설치하는 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="3a956-124">- **Azure**: Azure IaaS VM에 에이전트를 설치하는 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="3a956-125">VMware</span><span class="sxs-lookup"><span data-stu-id="3a956-125">VMware</span></span> </br> <span data-ttu-id="3a956-126">Azure</span><span class="sxs-lookup"><span data-stu-id="3a956-126">Azure</span></span>|
|<span data-ttu-id="3a956-127">-q</span><span class="sxs-lookup"><span data-stu-id="3a956-127">-q</span></span>|<span data-ttu-id="3a956-128">옵션</span><span class="sxs-lookup"><span data-stu-id="3a956-128">Optional</span></span>|<span data-ttu-id="3a956-129">설치 관리자를 자동 모드에서 실행하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-129">Specifies to run installer in silent mode</span></span>| <span data-ttu-id="3a956-130">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3a956-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="3a956-131">모바일 서비스 구성 명령줄</span><span class="sxs-lookup"><span data-stu-id="3a956-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="3a956-132">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-132">Parameter</span></span>|<span data-ttu-id="3a956-133">형식</span><span class="sxs-lookup"><span data-stu-id="3a956-133">Type</span></span>|<span data-ttu-id="3a956-134">설명</span><span class="sxs-lookup"><span data-stu-id="3a956-134">Description</span></span>|<span data-ttu-id="3a956-135">가능한 값</span><span class="sxs-lookup"><span data-stu-id="3a956-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="3a956-136">-i</span><span class="sxs-lookup"><span data-stu-id="3a956-136">-i</span></span> |<span data-ttu-id="3a956-137">필수</span><span class="sxs-lookup"><span data-stu-id="3a956-137">Mandatory</span></span>|<span data-ttu-id="3a956-138">구성 서버의 IP</span><span class="sxs-lookup"><span data-stu-id="3a956-138">IP of the Configuration Server</span></span>|<span data-ttu-id="3a956-139">모든 유효한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="3a956-139">Any valid IP Address</span></span>|
|<span data-ttu-id="3a956-140">-P</span><span class="sxs-lookup"><span data-stu-id="3a956-140">-P</span></span> |<span data-ttu-id="3a956-141">필수</span><span class="sxs-lookup"><span data-stu-id="3a956-141">Mandatory</span></span>|<span data-ttu-id="3a956-142">연결 암호가 저장되는 파일의 전체 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3a956-142">Full file path the file where the connection passphrase is saved</span></span>|<span data-ttu-id="3a956-143">모든 유효한 폴더</span><span class="sxs-lookup"><span data-stu-id="3a956-143">Any valid folder</span></span>|
