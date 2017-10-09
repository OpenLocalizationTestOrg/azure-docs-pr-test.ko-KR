1. <span data-ttu-id="66251-101">Hello installer tooa 로컬 폴더 (예를 들어 /tmp) tooprotect hello 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="66251-102">종료, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="66251-103">tooinstall 모바일 서비스 hello 다음 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="66251-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="66251-104">설치가 완료 되 면 tooget 등록된 toohello 구성 서버 hello 모바일 서비스에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="66251-105">구성 서버와 명령 tooregister hello 모바일 서비스를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="66251-106">모바일 서비스 설치 관리자 명령줄</span><span class="sxs-lookup"><span data-stu-id="66251-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="66251-107">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-107">Parameter</span></span>|<span data-ttu-id="66251-108">형식</span><span class="sxs-lookup"><span data-stu-id="66251-108">Type</span></span>|<span data-ttu-id="66251-109">설명</span><span class="sxs-lookup"><span data-stu-id="66251-109">Description</span></span>|<span data-ttu-id="66251-110">가능한 값</span><span class="sxs-lookup"><span data-stu-id="66251-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="66251-111">-r</span><span class="sxs-lookup"><span data-stu-id="66251-111">-r</span></span> |<span data-ttu-id="66251-112">필수</span><span class="sxs-lookup"><span data-stu-id="66251-112">Mandatory</span></span>|<span data-ttu-id="66251-113">MS(모바일 서비스) 설치 여부 또는 MT(마스터 대상) 설치 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="66251-114">MS</span><span class="sxs-lookup"><span data-stu-id="66251-114">MS</span></span> </br> <span data-ttu-id="66251-115">MT</span><span class="sxs-lookup"><span data-stu-id="66251-115">MT</span></span>|
|<span data-ttu-id="66251-116">일시 중지되고</span><span class="sxs-lookup"><span data-stu-id="66251-116">-d</span></span> |<span data-ttu-id="66251-117">옵션</span><span class="sxs-lookup"><span data-stu-id="66251-117">Optional</span></span>|<span data-ttu-id="66251-118">모바일 서비스를 설치하는 위치</span><span class="sxs-lookup"><span data-stu-id="66251-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="66251-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="66251-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="66251-120">-v</span><span class="sxs-lookup"><span data-stu-id="66251-120">-v</span></span>|<span data-ttu-id="66251-121">필수</span><span class="sxs-lookup"><span data-stu-id="66251-121">Mandatory</span></span>|<span data-ttu-id="66251-122">모바일 서비스 설치 가져오기는 hello에 hello 플랫폼 지정</span><span class="sxs-lookup"><span data-stu-id="66251-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="66251-123">- **VMware**: *VMware vSphere ESXi 호스트*, *Hyper-V 호스트* 및 *물리적 서버*에서 실행되는 VM에 모바일 서비스를 설치하는 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="66251-124">- **Azure**: Azure IaaS VM에 에이전트를 설치하는 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="66251-125">VMware</span><span class="sxs-lookup"><span data-stu-id="66251-125">VMware</span></span> </br> <span data-ttu-id="66251-126">Azure</span><span class="sxs-lookup"><span data-stu-id="66251-126">Azure</span></span>|
|<span data-ttu-id="66251-127">-q</span><span class="sxs-lookup"><span data-stu-id="66251-127">-q</span></span>|<span data-ttu-id="66251-128">옵션</span><span class="sxs-lookup"><span data-stu-id="66251-128">Optional</span></span>|<span data-ttu-id="66251-129">자동 모드에서 toorun 설치 관리자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="66251-130">해당 없음</span><span class="sxs-lookup"><span data-stu-id="66251-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="66251-131">모바일 서비스 구성 명령줄</span><span class="sxs-lookup"><span data-stu-id="66251-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="66251-132">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66251-132">Parameter</span></span>|<span data-ttu-id="66251-133">형식</span><span class="sxs-lookup"><span data-stu-id="66251-133">Type</span></span>|<span data-ttu-id="66251-134">설명</span><span class="sxs-lookup"><span data-stu-id="66251-134">Description</span></span>|<span data-ttu-id="66251-135">가능한 값</span><span class="sxs-lookup"><span data-stu-id="66251-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="66251-136">-i</span><span class="sxs-lookup"><span data-stu-id="66251-136">-i</span></span> |<span data-ttu-id="66251-137">필수</span><span class="sxs-lookup"><span data-stu-id="66251-137">Mandatory</span></span>|<span data-ttu-id="66251-138">hello 구성 서버 IP</span><span class="sxs-lookup"><span data-stu-id="66251-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="66251-139">모든 유효한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="66251-139">Any valid IP Address</span></span>|
|<span data-ttu-id="66251-140">-P</span><span class="sxs-lookup"><span data-stu-id="66251-140">-P</span></span> |<span data-ttu-id="66251-141">필수</span><span class="sxs-lookup"><span data-stu-id="66251-141">Mandatory</span></span>|<span data-ttu-id="66251-142">Hello 연결 암호 저장 되는 전체 파일 경로 hello 파일</span><span class="sxs-lookup"><span data-stu-id="66251-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="66251-143">모든 유효한 폴더</span><span class="sxs-lookup"><span data-stu-id="66251-143">Any valid folder</span></span>|
