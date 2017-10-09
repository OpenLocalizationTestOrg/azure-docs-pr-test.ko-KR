1. <span data-ttu-id="925b1-101">Tooprotect hello 서버 hello installer tooa 로컬 폴더 (예: C:\Temp)를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="925b1-102">Hello 명령을 명령 프롬프트에서 관리자 권한으로 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="925b1-103">tooinstall 모바일 서비스 hello 다음 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="925b1-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="925b1-104">이제 hello 에이전트 toobe hello 구성 서버에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="925b1-105">모바일 서비스 설치 관리자 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="925b1-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="925b1-106">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-106">Parameter</span></span>|<span data-ttu-id="925b1-107">형식</span><span class="sxs-lookup"><span data-stu-id="925b1-107">Type</span></span>|<span data-ttu-id="925b1-108">설명</span><span class="sxs-lookup"><span data-stu-id="925b1-108">Description</span></span>|<span data-ttu-id="925b1-109">가능한 값</span><span class="sxs-lookup"><span data-stu-id="925b1-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="925b1-110">/Role</span><span class="sxs-lookup"><span data-stu-id="925b1-110">/Role</span></span>|<span data-ttu-id="925b1-111">필수</span><span class="sxs-lookup"><span data-stu-id="925b1-111">Mandatory</span></span>|<span data-ttu-id="925b1-112">MS(모바일 서비스) 설치 여부 또는 MT(마스터 대상) 설치 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="925b1-113">MS</span><span class="sxs-lookup"><span data-stu-id="925b1-113">MS</span></span> </br> <span data-ttu-id="925b1-114">MT</span><span class="sxs-lookup"><span data-stu-id="925b1-114">MT</span></span>|
|<span data-ttu-id="925b1-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="925b1-115">/InstallLocation</span></span>|<span data-ttu-id="925b1-116">옵션</span><span class="sxs-lookup"><span data-stu-id="925b1-116">Optional</span></span>|<span data-ttu-id="925b1-117">모바일 서비스를 설치하는 위치</span><span class="sxs-lookup"><span data-stu-id="925b1-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="925b1-118">Hello 컴퓨터의 임의 폴더</span><span class="sxs-lookup"><span data-stu-id="925b1-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="925b1-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="925b1-119">/Platform</span></span>|<span data-ttu-id="925b1-120">필수</span><span class="sxs-lookup"><span data-stu-id="925b1-120">Mandatory</span></span>|<span data-ttu-id="925b1-121">모바일 서비스 설치 가져오기는 hello에 hello 플랫폼 지정</span><span class="sxs-lookup"><span data-stu-id="925b1-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="925b1-122">- **VMware**: *VMware vSphere ESXi 호스트*, *Hyper-V 호스트* 및 *물리적 서버*에서 실행되는 VM에 모바일 서비스를 설치하는 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="925b1-123">- **Azure**: Azure IaaS VM에 에이전트를 설치하는 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="925b1-124">VMware</span><span class="sxs-lookup"><span data-stu-id="925b1-124">VMware</span></span> </br> <span data-ttu-id="925b1-125">Azure</span><span class="sxs-lookup"><span data-stu-id="925b1-125">Azure</span></span>|
|<span data-ttu-id="925b1-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="925b1-126">/Silent</span></span>|<span data-ttu-id="925b1-127">옵션</span><span class="sxs-lookup"><span data-stu-id="925b1-127">Optional</span></span>|<span data-ttu-id="925b1-128">자동 모드에서 toorun hello 설치 관리자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="925b1-129">해당 없음</span><span class="sxs-lookup"><span data-stu-id="925b1-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="925b1-130">%ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log 아래 hello 설치 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="925b1-131">모바일 서비스 등록 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="925b1-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="925b1-132">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="925b1-132">Parameter</span></span>|<span data-ttu-id="925b1-133">형식</span><span class="sxs-lookup"><span data-stu-id="925b1-133">Type</span></span>|<span data-ttu-id="925b1-134">설명</span><span class="sxs-lookup"><span data-stu-id="925b1-134">Description</span></span>|<span data-ttu-id="925b1-135">가능한 값</span><span class="sxs-lookup"><span data-stu-id="925b1-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="925b1-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="925b1-136">/CSEndPoint</span></span> |<span data-ttu-id="925b1-137">필수</span><span class="sxs-lookup"><span data-stu-id="925b1-137">Mandatory</span></span>|<span data-ttu-id="925b1-138">Hello 구성 서버 IP 주소</span><span class="sxs-lookup"><span data-stu-id="925b1-138">IP address of hello configuration server</span></span>| <span data-ttu-id="925b1-139">모든 유효한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="925b1-139">Any valid IP address</span></span>|
  |<span data-ttu-id="925b1-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="925b1-140">/PassphraseFilePath</span></span>|<span data-ttu-id="925b1-141">필수</span><span class="sxs-lookup"><span data-stu-id="925b1-141">Mandatory</span></span>|<span data-ttu-id="925b1-142">Hello 암호의 위치</span><span class="sxs-lookup"><span data-stu-id="925b1-142">Location of hello passphrase</span></span> |<span data-ttu-id="925b1-143">모든 유효한 UNC 또는 로컬 파일 경로</span><span class="sxs-lookup"><span data-stu-id="925b1-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="925b1-144">hello AgentConfiguration 로그 %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log 아래에서 확인할 수 있음</span><span class="sxs-lookup"><span data-stu-id="925b1-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
