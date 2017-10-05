---
title: "Azure Automation DSC를 사용하여 Site Recovery 모바일 서비스 배포 | Microsoft Docs"
description: "Azure Automation DSC를 사용하여 Azure Site Recovery 모바일 서비스 및 VMware VM과 물리적 서버 복제를 위한 Azure 에이전트를 자동으로 배포하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="b8a5d-103">VM 복제를 위해 Azure Automation DSC를 사용하여 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="b8a5d-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="b8a5d-104">Operations Management Suite에서는 무중단 업무 방식 계획의 일부분으로 사용 가능한 포괄적인 백업 및 재해 복구 솔루션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="b8a5d-105">처음에는 Hyper-V에서 Hyper-V 복제본을 통해 이러한 솔루션이 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="b8a5d-106">하지만 고객의 클라우드에는 여러 하이퍼바이저와 플랫폼이 포함되어 있으므로, 다른 유형의 설정을 지원하도록 솔루션 범위가 확장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="b8a5d-107">현재 VMware 작업 및/또는 실제 서버를 실행 중인 경우 관리 서버가 환경 내의 모든 Azure Site Recovery 구성 요소를 실행하여 Azure와의 통신 및 데이터 복제를 처리합니다(Azure가 대상인 경우).</span><span class="sxs-lookup"><span data-stu-id="b8a5d-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="b8a5d-108">자동화 DSC를 사용하여 Site Recovery 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="b8a5d-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="b8a5d-109">먼저 이 관리 서버가 수행하는 작업을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="b8a5d-110">관리 서버는 다양한 서버 역할을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-110">The management server runs several server roles.</span></span> <span data-ttu-id="b8a5d-111">이러한 역할 중 하나인 *구성*은 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="b8a5d-112">그리고 *프로세스* 역할은 복제 게이트웨이 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="b8a5d-113">이 역할은 보호된 소스 컴퓨터에서 복제 데이터를 수신하여 캐싱, 압축 및 암호화용으로 최적화한 다음 Azure 저장소 계정으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="b8a5d-114">보호된 컴퓨터에 대한 모바일 서비스의 강제 설치를 실행하고 VMware VM의 자동 검색을 수행하는 것도 프로세스 역할의 기능 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="b8a5d-115">Azure에서 장애 복구(failback)가 수행되면 *마스터 대상* 역할이 이 작업의 일부로 복제 데이터를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="b8a5d-116">보호된 컴퓨터의 경우에는 *모바일 서비스*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="b8a5d-117">이 구성 요소는 Azure에 복제하려는 모든 컴퓨터(VMware VM 또는 실제 서버)에 배포되며,</span><span class="sxs-lookup"><span data-stu-id="b8a5d-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="b8a5d-118">컴퓨터에서 데이터 쓰기를 캡처하여 관리 서버(프로세스 역할)로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="b8a5d-119">무중단 업무 방식을 사용해야 하는 경우에는 작업, 인프라 및 관련 구성 요소를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="b8a5d-120">그러면 RTO(복구 시간 목표) 및 RPO(복구 지점 목표) 관련 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="b8a5d-121">이 컨텍스트에서는 작업을 원하는 방식으로 보호하는 데 핵심적인 요소는 모바일 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="b8a5d-122">몇 가지 Operations Management Suite 구성 요소를 활용하면 안정적인 보호 설정이 적용되어 있는지를 최적화된 방식으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="b8a5d-123">이 문서에서는 Azure 자동화 DSC(필요한 상태 구성)를 Site Recovery와 함께 사용하여 다음을 확인하는 방법의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="b8a5d-124">모바일 서비스와 Azure VM 에이전트가 보호하려는 Windows 컴퓨터에 배포되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="b8a5d-125">Azure가 복제 대상일 때 모바일 서비스와 Azure VM 에이전트가 항상 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8a5d-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b8a5d-126">Prerequisites</span></span>
* <span data-ttu-id="b8a5d-127">필수 설치 프로그램을 저장할 저장소</span><span class="sxs-lookup"><span data-stu-id="b8a5d-127">A repository to store the required setup</span></span>
* <span data-ttu-id="b8a5d-128">관리 서버에 등록하기 위해 필요한 암호를 저장할 저장소</span><span class="sxs-lookup"><span data-stu-id="b8a5d-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="b8a5d-129">각 관리 서버에 대해 고유한 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="b8a5d-130">여러 관리 서버를 배포하려는 경우 올바른 암호가 passphrase.txt 파일에 저장되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="b8a5d-131">보호할 수 있도록 설정하려는 컴퓨터에 WMF(Windows Management Framework) 5.0 설치(자동화 DSC의 요구 사항)</span><span class="sxs-lookup"><span data-stu-id="b8a5d-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="b8a5d-132">WMF 4.0이 설치되어 있는 Windows 컴퓨터에 대해 DSC를 사용하려는 경우 [연결이 끊어진 환경에서 DSC 사용](## Use DSC in disconnected environments) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="b8a5d-133">모바일 서비스는 명령줄을 통해 설치할 수 있으며 여러 인수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="b8a5d-134">그러므로 설치에서 이진 파일을 추출한 다음 DSC 구성을 사용하여 검색할 수 있는 위치에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="b8a5d-135">1단계: 이진 파일 추출</span><span class="sxs-lookup"><span data-stu-id="b8a5d-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="b8a5d-136">이 설치에 필요한 파일을 추출하려면 관리 서버에서 다음 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="b8a5d-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="b8a5d-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="b8a5d-138">이 폴더에 다음과 같은 이름의 MSI 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="b8a5d-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="b8a5d-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="b8a5d-140">다음 명령을 사용하여 설치 관리자를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="b8a5d-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="b8a5d-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="b8a5d-142">모든 파일을 선택하여 압축된(zip) 폴더로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="b8a5d-143">이제 자동화 DSC를 사용하여 모바일 서비스의 설치를 자동화하는 데 필요한 이진 파일이 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="b8a5d-144">암호</span><span class="sxs-lookup"><span data-stu-id="b8a5d-144">Passphrase</span></span>
<span data-ttu-id="b8a5d-145">다음으로, 이 압축된 폴더를 배치할 위치를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="b8a5d-146">이 문서의 뒷부분에서 설명하는 대로 Azure 저장소 계정을 사용하여 설치에 필요한 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="b8a5d-147">그러면 프로세스의 일부분으로 에이전트가 관리 서버에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="b8a5d-148">관리 서버를 배포할 때 받은 암호를 텍스트 파일(passphrase.txt)로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="b8a5d-149">zip 폴더와 암호를 모두 Azure 저장소 계정의 전용 컨테이너에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![폴더 위치](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="b8a5d-151">이러한 파일은 네트워크의 공유에 보관해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="b8a5d-152">나중에 사용할 DSC 리소스에 액세스할 수 있으며 설치 프로그램과 암호를 가져올 수 있는지 확인하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="b8a5d-153">2단계: DSC 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="b8a5d-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="b8a5d-154">설치에서는 WMF 5.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="b8a5d-155">컴퓨터가 자동화 DSC를 통해 구성을 올바르게 적용하도록 하려면 WMF 5.0이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="b8a5d-156">이 환경에서는 다음과 같은 예제 DSC 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-156">The environment uses the following example DSC configuration:</span></span>

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
<span data-ttu-id="b8a5d-157">이 구성은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-157">The configuration will do the following:</span></span>

* <span data-ttu-id="b8a5d-158">변수를 통해 모바일 서비스 및 Azure VM 에이전트용 이진 파일 및 암호를 가져올 위치와 출력을 저장할 위치를 구성에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="b8a5d-159">`xRemoteFile` 을 사용하여 리포지토리에서 파일을 다운로드할 수 있도록 xPSDesiredStateConfiguration DSC 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="b8a5d-160">이진 파일을 저장할 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="b8a5d-161">보관 리소스를 통해 zip 폴더에서 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="b8a5d-162">패키지 Install 리소스를 통해 지정된 인수를 사용하여 UNIFIEDAGENT.EXE 설치 관리자에서 모바일 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="b8a5d-163">이때 인수를 생성하는 변수는 실제 환경을 반영하도록 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="b8a5d-164">패키지 AzureAgent 리소스를 통해 Azure VM 에이전트를 설치합니다. Azure에서 실행되는 모든 VM에서는 Azure VM 에이전트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="b8a5d-165">Azure VM 에이전트를 사용하면 장애 조치(failover) 이후 VM에 확장을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="b8a5d-166">하나 이상의 서비스 리소스를 통해 관련 모바일 서비스 및 Azure 서비스가 항상 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="b8a5d-167">구성을 **ASRMobilityService**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="b8a5d-168">에이전트가 정상적으로 연결되고 올바른 암호를 사용하도록 하려면 실제 관리 서버를 반영하도록 구성의 CSIP를 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="b8a5d-169">3단계: 자동화 DSC 업로드</span><span class="sxs-lookup"><span data-stu-id="b8a5d-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="b8a5d-170">이전 단계에서 작성한 DSC 구성은 필수 DSC 리소스 모듈(xPSDesiredStateConfiguration)을 가져오므로 DSC 구성을 업로드하기 전에 자동화에서 해당 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="b8a5d-171">자동화 계정에 로그인하여 **자산** > **모듈**로 이동한 다음 **갤러리 찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="b8a5d-172">여기서 모듈을 검색하고 계정으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-172">Here you can search for the module and import it to your account.</span></span>

![가져오기 모듈](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="b8a5d-174">이 작업이 완료되면 Azure Resource Manager 모듈이 설치된 컴퓨터로 이동하여 새로 만든 DSC 구성 가져오기를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="b8a5d-175">Cmdlet 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8a5d-175">Import cmdlets</span></span>
<span data-ttu-id="b8a5d-176">PowerShell에서 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="b8a5d-177">그런 다음 실제 환경을 반영하도록 cmdlet을 수정하고 변수에서 자동화 계정 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="b8a5d-178">다음 cmdlet을 사용하여 구성을 자동화 DSC에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="b8a5d-179">자동화 DSC의 구성 컴파일</span><span class="sxs-lookup"><span data-stu-id="b8a5d-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="b8a5d-180">다음으로는 노드를 구성에 등록할 수 있도록 자동화 DSC의 구성을 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="b8a5d-181">다음 cmdlet을 실행하여 이 목적을 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="b8a5d-182">기본적으로는 구성을 호스트된 DSC 끌어오기 서비스로 배포하므로 컴파일은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="b8a5d-183">구성을 컴파일한 후에는 PowerShell(Get-AzureRmAutomationDscCompilationJob) 또는 [Azure 포털](https://portal.azure.com/)을 사용하여 작업 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![작업 검색](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="b8a5d-185">이제 DSC 구성을 자동화 DSC에 게시 및 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="b8a5d-186">4단계: 자동화 DSC에 컴퓨터 등록</span><span class="sxs-lookup"><span data-stu-id="b8a5d-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="b8a5d-187">이 시나리오를 완료하기 위한 필수 구성 요소 중 하나는 WMF의 최신 버전을 설치하여 Windows 컴퓨터를 업데이트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="b8a5d-188">[다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50395)에서 사용 중인 플랫폼에 적합한 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="b8a5d-189">이제 노드에 적용할 DSC용 metaconfig를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="b8a5d-190">이 작업에 성공하려면 Azure에서 선택한 자동화 계정에 대한 끝점 URL과 기본 키를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="b8a5d-191">이러한 값은 자동화 계정 **모든 설정** 블레이드의 **키** 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![키 값](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="b8a5d-193">이 예제에서는 Windows Server 2012 R2 실제 서버를 Site Recovery로 보호하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="b8a5d-194">레지스트리에서 보류 중인 파일 이름 바꾸기 작업 확인</span><span class="sxs-lookup"><span data-stu-id="b8a5d-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="b8a5d-195">자동화 DSC 끝점과 서버 연결을 시작하기 전에 레지스트리에서 보류 중인 파일 이름 바꾸기 작업이 있는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="b8a5d-196">이러한 작업이 있으면 보류 중인 다시 부팅으로 인해 설치 프로그램을 완료하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="b8a5d-197">다음 cmdlet을 실행하여 서버에 보류 중인 다시 부팅이 없는지 확인:</span><span class="sxs-lookup"><span data-stu-id="b8a5d-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="b8a5d-198">결과에 아무 항목도 표시되지 않으면 계속 진행해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="b8a5d-199">그렇지 않은 경우 유지 관리 기간 동안 서버를 다시 부팅하여 이 상황을 해소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="b8a5d-200">서버에서 구성을 적용하려면 PowerShell ISE(통합 스크립팅 환경)를 시작하고 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="b8a5d-201">이 스크립트는 기본적으로 로컬 구성 관리자 엔진에 대해 자동화 DSC 서비스에 등록하고 특정 구성(ASRMobilityService.localhost)을 검색하도록 지시하는 DSC 로컬 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="b8a5d-202">이 구성을 사용하는 경우 로컬 구성 관리자 엔진이 자동화 DSC에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="b8a5d-203">이 스크립트는 엔진 작동 방식, 구성 드리프트 발생 시에 수행할 작업(ApplyAndAutoCorrect), 그리고 다시 부팅이 필요한 경우 구성을 진행할 방법도 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="b8a5d-204">이 스크립트를 실행하고 나면 자동화 DSC에 노드가 등록되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![노드 등록 진행 중](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="b8a5d-206">Azure 포털로 돌아가면 새로 등록한 노드가 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![포털에 등록된 노드](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="b8a5d-208">서버에서 다음 PowerShell cmdlet을 실행하여 노드가 올바르게 등록되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="b8a5d-209">구성을 끌어와 서버에 적용한 후에는 다음 cmdlet을 실행하여 수행된 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="b8a5d-210">출력에 서버가 해당 구성을 가져온 것으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-210">The output shows that the server has successfully pulled its configuration:</span></span>

![출력](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="b8a5d-212">또한 모바일 서비스 설정에는 *SystemDrive*\ProgramData\ASRSetupLogs에서 확인할 수 있는 자체의 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="b8a5d-213">지금까지</span><span class="sxs-lookup"><span data-stu-id="b8a5d-213">That’s it.</span></span> <span data-ttu-id="b8a5d-214">Site Recovery를 사용하여 보호하려는 컴퓨터에서 모바일 서비스를 배포하고 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="b8a5d-215">DSC를 사용하면 필요한 서비스가 항상 실행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-215">DSC will make sure that the required services are always running.</span></span>

![배포 정상 완료](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="b8a5d-217">관리 서버가 정상적으로 배포된 서비스를 검색하면 Site Recovery를 사용하여 컴퓨터에서 보호를 구성하고 복제를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="b8a5d-218">연결이 끊어진 환경에서 DSC 사용</span><span class="sxs-lookup"><span data-stu-id="b8a5d-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="b8a5d-219">컴퓨터가 인터넷에 연결되어 있지 않은 경우에도 DSC를 사용하여 보호하려는 작업에 대해 모바일 서비스를 배포하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="b8a5d-220">환경에서 자체 DSC 끌어오기 서버를 인스턴스화하면 궁극적으로는 자동화 DSC에서 제공되는 것과 같은 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="b8a5d-221">즉, 클라이언트가 등록된 구성을 DSC 끝점으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="b8a5d-222">DSC 구성을 로컬로 또는 원격으로 컴퓨터에 수동으로 밀어넣는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="b8a5d-223">이 예제에는 컴퓨터에 이름에 해당하는 매개 변수가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="b8a5d-224">현재 원격 파일은 보호하려는 컴퓨터에서 액세스할 수 있어야 하는 원격 공유에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="b8a5d-225">스크립트가 종료되면 구성이 작동하며, 그러면 대상 컴퓨터에 대한 DSC 구성 적용이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b8a5d-226">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b8a5d-226">Prerequisites</span></span>
<span data-ttu-id="b8a5d-227">XPSDesiredStateConfiguration PowerShell 모듈이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="b8a5d-228">WMF 5.0이 설치된 Windows 컴퓨터의 경우 대상 컴퓨터에서 다음 cmdlet을 실행하여 xPSDesiredStateConfiguration 모듈을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="b8a5d-229">WMF 4.0이 설치되어 있는 Windows 컴퓨터에 배포해야 하는 경우에는 모듈을 다운로드하여 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="b8a5d-230">PowerShellGet(WMF 5.0)이 설치되어 있는 컴퓨터에서는 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="b8a5d-231">WMF 4.0의 경우에는 컴퓨터에 [Windows 8.1 업데이트 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) 이 설치되어 있는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="b8a5d-232">WMF 5.0 및 WMF 4.0이 설치되어 있는 Windows 컴퓨터에 다음 구성을 밀어 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="b8a5d-233">자동화 DSC에서 제공되는 것과 비슷한 기능을 제공하기 위해 회사 네트워크에서 자체 DSC 끌어오기 서버를 인스턴스화하려는 경우 [DSC 웹 끌어오기 서버 설정](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="b8a5d-234">선택 사항: Azure Resource Manager 템플릿을 사용하여 DSC 구성 배포</span><span class="sxs-lookup"><span data-stu-id="b8a5d-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="b8a5d-235">이 문서의 앞부분에서는 고유한 DSC 구성을 만들어 모바일 서비스 및 Azure VM 에이전트를 자동으로 배포하고, 보호하려는 컴퓨터에서 모바일 서비스와 에이전트가 실행되고 있는지를 확인하는 방법을 중점적으로 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="b8a5d-236">이 DSC 구성을 신규 또는 기존 Azure 자동화 계정으로 배포하는 Azure Resource Manager 템플릿도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="b8a5d-237">이 템플릿은 입력 매개 변수를 사용하여 실제 환경에 맞는 변수를 포함하는 자동화 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="b8a5d-238">템플릿을 배포한 후에는 이 가이드의 4단계를 참조해 컴퓨터를 등록하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="b8a5d-239">템플릿은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-239">The template will do the following:</span></span>

1. <span data-ttu-id="b8a5d-240">기존 자동화 계정을 사용하거나 새로운 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="b8a5d-241">다음에 해당하는 입력 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-241">Take input parameters for:</span></span>
   * <span data-ttu-id="b8a5d-242">ASRRemoteFile - 모바일 서비스 설치 프로그램을 저장한 위치</span><span class="sxs-lookup"><span data-stu-id="b8a5d-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="b8a5d-243">ASRPassphrase - passphrase.txt 파일을 저장한 위치</span><span class="sxs-lookup"><span data-stu-id="b8a5d-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="b8a5d-244">ASRCSEndpoint - 관리 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b8a5d-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="b8a5d-245">xPSDesiredStateConfiguration PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="b8a5d-246">DSC 구성을 만들고 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="b8a5d-247">위의 모든 단계는 올바른 순서로 수행되므로 해당 단계가 완료되면 보호할 컴퓨터 등록을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="b8a5d-248">배포 지침이 포함된 템플릿은 [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="b8a5d-249">아래 PowerShell을 사용하여 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-249">Deploy the template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b8a5d-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8a5d-250">Next steps</span></span>
<span data-ttu-id="b8a5d-251">모바일 서비스 에이전트를 배포한 후 가상 컴퓨터에 대해 [복제를 사용하도록 설정](site-recovery-vmware-to-azure.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a5d-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
