---
title: "aaaDeploy hello Azure 자동화 dsc 사이트 복구 모바일 서비스 | Microsoft Docs"
description: "Toouse Azure 자동화 DSC tooautomatically 복제 tooAzure 물리적 서버와 VMware VM에 대 한 hello Azure 사이트 복구 모바일 서비스 및 Azure 에이전트를 배포 방법에 대해 설명"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="a64eb-103">VM 복제 하기 위해 Azure 자동화 dsc hello 모바일 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="a64eb-104">Operations Management Suite에서는 무중단 업무 방식 계획의 일부분으로 사용 가능한 포괄적인 백업 및 재해 복구 솔루션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="a64eb-105">처음에는 Hyper-V에서 Hyper-V 복제본을 통해 이러한 솔루션이 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="a64eb-106">했지만 확장 된 toosupport 다른 유형의 설치 프로그램 및 때문에 고객 여러 하이퍼바이저 플랫폼의 클라우드.</span><span class="sxs-lookup"><span data-stu-id="a64eb-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="a64eb-107">실행 하는 경우 VMware 작업 부하 및/또는 실제 서버 오늘, 관리 서버 hello의 모든 Azure Site Recovery 구성 요소 사용자 환경 toohandle hello 통신 및 데이터 복제에 Azure 통해가 있을 때 실행 Azure 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="a64eb-108">자동화 DSC를 사용 하 여 hello 사이트 복구 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="a64eb-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="a64eb-109">먼저 이 관리 서버가 수행하는 작업을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="a64eb-110">hello 관리 서버는 여러 서버 역할을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-110">hello management server runs several server roles.</span></span> <span data-ttu-id="a64eb-111">이러한 역할 중 하나인 *구성*은 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="a64eb-112">또한 hello *프로세스* 역할은 게이트웨이 역할을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="a64eb-113">이 역할 보호 된 원본 컴퓨터에서 복제 데이터를 수신, 캐싱, 압축 및 암호화를 사용 하 여이 최적화 하 고 tooan Azure 저장소 계정 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="a64eb-114">Hello 프로세스 역할에 대 한 hello 함수 중 하나는 또한 hello 이동성 서비스 tooprotected 컴퓨터의 toopush 설치 및 VMware Vm의 자동 검색을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="a64eb-115">Azure에서 장애 복구 이면 hello *마스터 대상* 역할이이 작업의 일부로 hello 복제 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="a64eb-116">Hello 보호 된 컴퓨터에 대 한 hello에 의존 *모바일 서비스*합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="a64eb-117">이 구성 요소는 원하는 tooreplicate tooAzure tooevery 배포 된 컴퓨터 (VMware VM 또는 실제 서버).</span><span class="sxs-lookup"><span data-stu-id="a64eb-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="a64eb-118">Hello 컴퓨터에 데이터 쓰기 캡처하고 toohello 관리 서버 (프로세스 역할)에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="a64eb-119">비즈니스 연속성을 다룰 때 중요 한 toounderstand 작업, 인프라 및 hello 구성 요소와 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="a64eb-120">그런 다음 복구 시간 목표 (RTO) 및 복구 지점 목표 (RPO)에 대 한 hello 요구 사항을 충족 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="a64eb-121">이 컨텍스트에서 hello 모바일 서비스는 키 tooensuring 예상 작업 보호 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="a64eb-122">몇 가지 Operations Management Suite 구성 요소를 활용하면 안정적인 보호 설정이 적용되어 있는지를 최적화된 방식으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="a64eb-123">이 문서에서는 Azure 자동화 DSC 필요한 상태 구성 (), tooensure 사이트 복구와 함께 사용 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="a64eb-124">hello 모바일 서비스와 Azure VM 에이전트는 원하는 tooprotect 배포 toohello Windows 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="a64eb-125">hello 모바일 서비스와 Azure VM 에이전트는 항상 때 실행 중 Azure hello 복제 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a64eb-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a64eb-126">Prerequisites</span></span>
* <span data-ttu-id="a64eb-127">리포지토리 toostore hello 필수 설정</span><span class="sxs-lookup"><span data-stu-id="a64eb-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="a64eb-128">리포지토리 toostore hello hello 관리 서버와 공유 암호 tooregister 필요</span><span class="sxs-lookup"><span data-stu-id="a64eb-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="a64eb-129">각 관리 서버에 대해 고유한 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="a64eb-130">보아야 toodeploy 여러 관리 서버, 해야 tooensure 해당 hello 올바른 암호 hello passphrase.txt 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="a64eb-131">Windows Management Framework (WMF) 5.0 (자동화 DSC에 대 한 요구 사항) 보호를 위해 tooenable 되도록 hello 컴퓨터에 설치 되어</span><span class="sxs-lookup"><span data-stu-id="a64eb-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="a64eb-132">WMF 4.0이 설치 되어 있는 toouse DSC에 대 한 Windows 컴퓨터를 원하는 경우 hello 섹션을 참조 하세요. [연결이 끊어진된 환경에서 사용 하 여 DSC](## Use DSC in disconnected environments)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="a64eb-133">hello 모바일 서비스 hello 명령줄을 통해 설치할 수 있으며 여러 인수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="a64eb-134">바로 이러한 이유로 toohave hello 이진 파일 (설치에서 압축을 풀어) 이후 필요 하 고 DSC 구성을 사용 하 여 검색할 수 있습니다 장소에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="a64eb-135">1단계: 이진 파일 추출</span><span class="sxs-lookup"><span data-stu-id="a64eb-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="a64eb-136">tooextract hello 필요한 파일을이 설치 프로그램에 대 한 관리 서버에 디렉터리를 다음 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="a64eb-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="a64eb-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="a64eb-138">이 폴더에 다음과 같은 이름의 MSI 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="a64eb-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="a64eb-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="a64eb-140">사용 하 여 hello 다음 명령은 tooextract hello 설치 관리자:</span><span class="sxs-lookup"><span data-stu-id="a64eb-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="a64eb-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="a64eb-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="a64eb-142">모든 파일을 선택 하 고 tooa 압축된 (zip) 폴더를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="a64eb-143">자동화 DSC를 사용 하 여 hello 모바일 서비스의 tooautomate hello 설치 해야 하는 hello 바이너리 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="a64eb-144">암호</span><span class="sxs-lookup"><span data-stu-id="a64eb-144">Passphrase</span></span>
<span data-ttu-id="a64eb-145">다음으로, 저장할 tooplace이 zip 폴더 toodetermine를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="a64eb-146">표시 된 나중에 toostore hello 암호 hello 설치에 필요한 Azure 저장소 계정에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="a64eb-147">hello 에이전트는 hello 프로세스의 일부로 hello 관리 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="a64eb-148">hello 관리 서버를 배포할 때 가져온 hello 암호 passphrase.txt로 tooa 텍스트 파일로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="a64eb-149">Hello Azure 저장소 계정에서에서 전용된 컨테이너에서 hello 압축 된 폴더와 hello 암호를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![폴더 위치](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="a64eb-151">원하는 경우 tookeep 이러한 파일 공유에 네트워크에서이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="a64eb-152">나중에 사용할 계획 hello DSC 리소스 액세스 개이고 hello 설정 및 암호를 가져올 수 tooensure를 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="a64eb-153">2 단계: hello DSC 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="a64eb-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="a64eb-154">hello 설치 WMF 5.0에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="a64eb-155">WMF 5.0 필요 없는 toobe, 컴퓨터 toosuccessfully hello에 대 한 자동화 DSC를 통해 hello 구성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="a64eb-156">hello 환경에서는 다음 예제에서는 DSC 구성을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="a64eb-157">hello 구성 작업을 수행 합니다 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="a64eb-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="a64eb-158">hello 변수 tooget hello 암호와 toostore hello 출력 tooget가 그 hello 모바일 서비스와 hello Azure VM 에이전트에 대 한 이진을 hello hello 구성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="a64eb-159">hello 구성 가져옵니다 hello xPSDesiredStateConfiguration DSC 리소스를 사용할 수 있도록 `xRemoteFile` hello 리포지토리에서 toodownload hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="a64eb-160">hello 구성 toostore hello 이진 파일의 압축을 풀려면는 디렉터리로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="a64eb-161">hello 보관 리소스는 hello zip 폴더에서 hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="a64eb-162">hello 패키지 설치 리소스 hello UNIFIEDAGENT에서에서 hello 모바일 서비스를 설치 합니다. EXE installer hello 특정 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="a64eb-163">(hello 인수를 생성 하는 hello 변수 할 변경 toobe tooreflect 환경.)</span><span class="sxs-lookup"><span data-stu-id="a64eb-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="a64eb-164">hello 패키지 AzureAgent 리소스에서는 Azure에서 실행 되는 모든 VM에 권장 hello Azure VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="a64eb-165">hello Azure VM 에이전트를 사용 가능한 tooadd 확장 toohello VM 장애 조치 후.</span><span class="sxs-lookup"><span data-stu-id="a64eb-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="a64eb-166">hello 서비스 리소스 또는 리소스는 확인 hello 관련 모바일 서비스 및 hello Azure 서비스는 항상 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="a64eb-167">으로 hello 구성을 저장 **ASRMobilityService**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="a64eb-168">Tooreplace hello CSIP 구성 tooreflect hello 실제 관리 서버에서를 기억 hello 에이전트 올바르게 연결 하 고 있도록 hello 올바른 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="a64eb-169">3 단계: 업로드 tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="a64eb-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="a64eb-170">때문에 변경한 hello DSC 구성에서 필요한 DSC 리소스 모듈 (xPSDesiredStateConfiguration)을 가져옵니다, 해야 tooimport 자동화에서 해당 모듈 hello DSC 구성에 업로드 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="a64eb-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="a64eb-171">자동화 계정 tooyour 로그인 너무 찾아보기**자산** > **모듈**를 클릭 하 고 **찾아보기 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="a64eb-172">Hello 모듈에 대 한 검색할 수는 여기 tooyour 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-172">Here you can search for hello module and import it tooyour account.</span></span>

![가져오기 모듈](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="a64eb-174">이 완료 하면 tooyour 컴퓨터 hello Azure 리소스 관리자 모듈 설치 되어 있는 이동한 다음 tooimport 새로 만든 hello DSC 구성을 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="a64eb-175">Cmdlet 가져오기</span><span class="sxs-lookup"><span data-stu-id="a64eb-175">Import cmdlets</span></span>
<span data-ttu-id="a64eb-176">PowerShell에서 tooyour Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="a64eb-177">수정 hello cmdlet tooreflect 사용자 환경 및 변수에 자동화 계정 정보를 캡처:</span><span class="sxs-lookup"><span data-stu-id="a64eb-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="a64eb-178">Hello 다음 cmdlet을 사용 하 여 tooAutomation DSC를 구성 하는 hello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="a64eb-179">자동화 DSC에서 hello 구성 컴파일</span><span class="sxs-lookup"><span data-stu-id="a64eb-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="a64eb-180">다음으로, 해야 자동화 DSC에서 toocompile hello 구성 tooregister 노드 tooit를 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="a64eb-181">Hello 다음 cmdlet을 실행 하 여를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="a64eb-182">이 작업에 hello 구성 호스팅된 toohello DSC 끌어오기 서비스를 기본적으로 배포 하는 때문에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="a64eb-183">PowerShell (Get AzureRmAutomationDscCompilationJob)를 사용 하 여 또는 hello를 사용 하 여 hello 작업 정보를 검색할 수 hello 구성을 컴파일한 후 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![작업 검색](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="a64eb-185">이제 성공적으로 게시 및 있는 DSC 구성 tooAutomation DSC를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="a64eb-186">4 단계: 컴퓨터 등록 tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="a64eb-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="a64eb-187">이 시나리오를 완료 하기 위한 hello 필수 구성 요소 중 하나는 Windows 컴퓨터의 WMF hello 최신 버전으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="a64eb-188">다운로드 하 여 hello에서 플랫폼에 대 한 hello 올바른 버전을 설치 [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50395)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="a64eb-189">이제 만들게 됩니다는 metaconfig dsc tooyour 노드를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="a64eb-190">이 toosucceed, tooretrieve hello 끝점 URL과 hello 기본 키가 필요 Azure에서 선택한 자동화 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="a64eb-191">이러한 값을 찾을 수 **키** hello에 **모든 설정을** 블레이드 hello 자동화 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![키 값](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="a64eb-193">이 예제에서는 Windows Server 2012 R2 실제 서버 Site Recovery를 사용 하 여 tooprotect 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="a64eb-194">보류 된 파일 이름 바꾸기 작업이 hello 레지스트리에 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="a64eb-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="a64eb-195">Hello 자동화 DSC 끝점과 tooassociate hello 서버를 시작 하기 전에 hello 레지스트리에 파일 이름 바꾸기 작업이 보류 중인를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="a64eb-196">Hello 설치 기한 마무리에서 인해은 tooa 다시 부팅 보류 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="a64eb-197">Hello cmdlet tooverify hello 서버에서 보류 중인 재부팅 하지 않아도 있는지 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="a64eb-198">이 빈 표시 되 면 확인 tooproceed 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="a64eb-199">파일이 없으면 hello 서버 유지 관리 기간 동안 다시 부팅 하 여 해결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="a64eb-200">hello PowerShell 스크립팅 환경을 ISE (통합)를 시작 하 고 hello 다음 스크립트를 실행 하는 hello 서버의 tooapply hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="a64eb-201">이 기본적으로 DSC 로컬 구성을 자동화 DSC 서비스 hello로 hello 로컬 구성 관리자 엔진 tooregister 지시 및 hello 특정 구성 (ASRMobilityService.localhost)를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="a64eb-202">이 구성을 자동화 dsc 로컬 구성 관리자 hello 엔진 tooregister 자체를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="a64eb-203">또한 hello 엔진 작동 방식, 수행할 경우 구성 드리프트 (ApplyAndAutoCorrect) 및 어떻게 진행 되는 것 hello 구성으로 다시 부팅 해야 하는 경우를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="a64eb-204">이 스크립트를 실행 한 후 hello 노드 자동화 dsc tooregister를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![노드 등록 진행 중](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="a64eb-206">Azure 포털 toohello 돌아가서 hello 새로 등록 된 노드에 hello 포털에서 이제 나타난 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Hello 포털에서 등록 된 노드](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="a64eb-208">Hello 서버에서 다음 PowerShell 노드 hello cmdlet tooverify 제대로 등록 되었는지 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="a64eb-209">Hello 구성에 대 한 가져온 및 적용 된 toohello 서버를 수행한 후 hello 다음 cmdlet을 실행 하 여이 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="a64eb-210">hello 출력이 해당 hello 서버에 해당 구성을 끌어온 성공적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![출력](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="a64eb-212">또한 hello Mobility service 설치에는 자체 로그에서 찾을 수 있는 *SystemDrive*\ProgramData\ASRSetupLogs 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="a64eb-213">지금까지</span><span class="sxs-lookup"><span data-stu-id="a64eb-213">That’s it.</span></span> <span data-ttu-id="a64eb-214">이제 성공적으로 배포 및 등록 한 hello 컴퓨터에서 모바일 서비스 hello Site Recovery를 사용 하 여 tooprotect 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="a64eb-215">DSC는 hello 필요한 서비스가 항상 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-215">DSC will make sure that hello required services are always running.</span></span>

![배포 정상 완료](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="a64eb-217">Hello 관리 서버에서 배포 된 hello를 발견 하면 후 보호를 구성할 수 있으며 사이트 복구를 사용 하 여 hello 컴퓨터에서 복제를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="a64eb-218">연결이 끊어진 환경에서 DSC 사용</span><span class="sxs-lookup"><span data-stu-id="a64eb-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="a64eb-219">컴퓨터에 연결 된 toohello 인터넷 하지 않으면 DSC toodeploy에 의존 하 고 수 있습니다 tooprotect hello 작업에서 hello 이동성 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="a64eb-220">사용자 환경에서 직접 DSC 끌어오기 서버를 인스턴스화할 수 tooessentially hello 자동화 DSC에서 얻을 수 있는 동일한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="a64eb-221">즉, 클라이언트 hello 끌어오고 hello 구성 (등록) 한 후 toohello DSC 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="a64eb-222">그러나 또 다른 옵션은 로컬 또는 원격으로 toomanually 푸시 hello DSC 구성 tooyour 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="a64eb-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="a64eb-223">이 예에서 hello 컴퓨터 이름에는 추가 된 매개 변수는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="a64eb-224">이제 원하는 tooprotect hello 컴퓨터별 hello 원격 파일에 액세스할 수 있어야 하는 원격 공유에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="a64eb-225">hello 스크립트 끝에 hello hello 구성 시행 하 고 tooapply hello DSC 구성 toohello 대상 컴퓨터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a64eb-226">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a64eb-226">Prerequisites</span></span>
<span data-ttu-id="a64eb-227">해당 hello xPSDesiredStateConfiguration PowerShell 모듈이 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="a64eb-228">WMF 5.0이 설치 되어 있는 Windows 컴퓨터에 대 한 hello cmdlet hello 대상 컴퓨터에서 다음을 실행 하 여 hello xPSDesiredStateConfiguration 모듈을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="a64eb-229">또한 다운로드 하 고 toodistribute이 필요할 경우 hello 모듈을 저장할 수 것 WMF 4.0이 있는 tooWindows 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="a64eb-230">PowerShellGet(WMF 5.0)이 설치되어 있는 컴퓨터에서는 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="a64eb-231">또한 WMF 4.0에 대 한 해당 hello 확인 [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) hello 컴퓨터에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="a64eb-232">hello 다음 구성을 처리할 수 있는 WMF 4.0 및 WMF 5.0 되어 tooWindows 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="a64eb-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="a64eb-233">자동화 DSC에서 얻을 수 있는 여 회사 네트워크 toomimic hello 기능에서 직접 DSC 끌어오기 서버 tooinstantiate 경우 참조 [DSC 웹 끌어오기 서버 설정](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="a64eb-234">선택 사항: Azure Resource Manager 템플릿을 사용하여 DSC 구성 배포</span><span class="sxs-lookup"><span data-stu-id="a64eb-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="a64eb-235">이 문서 DSC 구성 tooautomatically 직접 만드는 방법을 중점적 hello 모바일 서비스와 Azure VM 에이전트-hello를 배포 하 고 tooprotect 원하는 hello 컴퓨터에서 실행 중인 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="a64eb-236">이 DSC 구성 tooa 새로운 또는 기존 Azure 자동화 계정을 배포 하는 Azure 리소스 관리자 템플릿을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="a64eb-237">hello 템플릿을 환경에 대 한 hello 변수를 포함 하는 입력된 매개 변수 toocreate 자동화 자산을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="a64eb-238">Hello 서식 파일을 배포한 후에이 가이드 tooonboard toostep 4를 컴퓨터에 단순히 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="a64eb-239">hello 템플릿을 처리 해 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="a64eb-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="a64eb-240">기존 자동화 계정을 사용하거나 새로운 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="a64eb-241">다음에 해당하는 입력 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-241">Take input parameters for:</span></span>
   * <span data-ttu-id="a64eb-242">ASRRemoteFile-hello Mobility service 설치 프로그램을 저장 한 hello 위치</span><span class="sxs-lookup"><span data-stu-id="a64eb-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="a64eb-243">ASRPassphrase-hello passphrase.txt 파일을 저장 한 hello 위치</span><span class="sxs-lookup"><span data-stu-id="a64eb-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="a64eb-244">ASRCSEndpoint-관리 서버 hello IP 주소</span><span class="sxs-lookup"><span data-stu-id="a64eb-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="a64eb-245">Hello xPSDesiredStateConfiguration PowerShell 모듈을 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="a64eb-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="a64eb-246">만들고 hello DSC 구성을 컴파일하합니다</span><span class="sxs-lookup"><span data-stu-id="a64eb-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="a64eb-247">이전 단계는 모든 hello 컴퓨터 보호를 위해 온 보 딩을 시작할 수 있도록 hello 올바른 순서로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="a64eb-248">배포에 대 한 지침이 포함 된 hello 서식 파일에 있는 [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="a64eb-249">PowerShell을 사용 하 여 hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="a64eb-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a64eb-250">Next steps</span></span>
<span data-ttu-id="a64eb-251">Hello 이동성 서비스 에이전트를 배포한 후 다음을 할 수 있습니다 [복제 사용](site-recovery-vmware-to-azure.md) hello 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64eb-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
