---
title: "3 노드 Deis aaaDeploy 클러스터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 3 노드 Deis Azure 리소스 관리자 템플릿을 사용 하 여 Azure에서 클러스터"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="d9451-103">Azure에서 3노드 Deis 클러스터 배포 및 구성</span><span class="sxs-lookup"><span data-stu-id="d9451-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="d9451-104">이 문서는 Azure에서 [Deis](http://deis.io/) 클러스터를 프로비전하는 과정을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="d9451-105">필요한 인증서 toodeploying hello를 만들고 샘플 크기 조정에서 모든 hello 단계에서는 **이동** hello 새로 프로 비전 된 클러스터에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="d9451-106">hello 다음 다이어그램 아키텍처를 보여 줍니다 hello 배포 된 hello 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="d9451-107">시스템 관리자를 사용 하 여 hello 클러스터 관리 도구와 같은 Deis **deis** 및 **deisctl**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="d9451-108">연결은은 hello 멤버의 hello 연결 tooone hello 클러스터에서 노드를 전달 하는 Azure 부하 분산 장치를 통해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="d9451-109">hello 클라이언트 액세스를 배포 된 hello 부하 분산 장치를 통해도 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="d9451-110">이 경우 hello 부하 분산 장치 전달 hello 트래픽 tooa Deis hello 클러스터에서 호스트 하는 트래픽을 toocorresponding Docker 컨테이너를 추가로 routs 라우터 메시를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![배포된 Desis 클러스터의 아키텍처 다이어그램](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="d9451-112">단계를 수행 하는 hello 통해 순서 toorun에 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="d9451-113">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d9451-113">An active Azure subscription.</span></span> <span data-ttu-id="d9451-114">없는 경우 [azure.com](https://azure.microsoft.com/)에서 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="d9451-115">회사 또는 학교 id toouse Azure 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="d9451-116">너무 필요한 개인 계정과 Microsoft id 사용 하 여 로그를 있으면[개인 컴퓨터로에서 작업 id를 만들](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d9451-117">-하나-클라이언트 운영 체제에 따라 hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 hello [Mac, Linux 및 Windows에 대 한 Azure CLI](../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="d9451-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="d9451-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="d9451-119">OpenSSL 사용 되는 toogenerate hello 필요한 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="d9451-120">[Git Bash](https://git-scm.com/)와 같은 Git 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d9451-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="d9451-121">tootest hello 샘플 응용 프로그램을도 DNS 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="d9451-122">모든 DNS 서버 또는 와일드 카드 A 레코드를 지원하는 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="d9451-123">컴퓨터 toorun Deis 클라이언트 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="d9451-124">로컬 컴퓨터 또는 가상 컴퓨터 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="d9451-125">거의 모든 Linux 배포판에 이러한 도구를 실행할 수는 있지만 hello 다음 명령을 사용 하 여 Ubuntu 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="d9451-126">프로 비전 hello 클러스터</span><span class="sxs-lookup"><span data-stu-id="d9451-126">Provision hello cluster</span></span>
<span data-ttu-id="d9451-127">이 섹션에서는 [Azure 리소스 관리자](../../azure-resource-manager/resource-group-overview.md) hello 오픈 소스 리포지토리에서 템플릿을 [azure-빠른 시작-템플릿](https://github.com/Azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="d9451-128">첫째, 다운 hello 템플릿을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="d9451-129">그런 다음 인증에 대해 새 SSH 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="d9451-130">그런 다음 클러스터에 대해 새 식별자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="d9451-131">및 마지막으로 hello 셸 스크립트 또는 hello PowerShell 스크립트 tooprovision hello 클러스터 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="d9451-132">복제 hello 리포지토리: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="d9451-133">Toohello 템플릿 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="d9451-134">ssh-keygen를 사용하여 새 SSH 키 쌍 만들기:</span><span class="sxs-lookup"><span data-stu-id="d9451-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="d9451-135">개인 키 위에 hello를 사용 하 여 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="d9451-136">너무 이동[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate 새 클러스터 토큰을 다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="d9451-137">각 CoreOS 클러스터 toohave이 무료 서비스에서 고유한 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="d9451-138">자세한 내용은 [CoreOS 설명서](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9451-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="d9451-139">Hello 수정 **클라우드 config.yaml** tooreplace hello 기존 파일 **검색** hello 새 토큰으로 토큰:</span><span class="sxs-lookup"><span data-stu-id="d9451-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="d9451-140">Hello 수정 **azuredeploy parameters.json** 파일: 텍스트 편집기에서 4 단계에서 만든 열기 hello 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="d9451-141">사이의 모든 텍스트를 복사 `----BEGIN CERTIFICATE-----` 및 `-----END CERTIFICATE-----` hello에 **sshKeyData** 매개 변수 (필요 함 tooremove 모든 줄 바꿈 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="d9451-142">Hello 수정 **newStorageAccountName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="d9451-143">VM OS 디스크에 대 한 hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="d9451-144">이 계정 이름은 전역적으로 고유 toobe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="d9451-145">Hello 수정 **publicDomainName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="d9451-146">이 hello 부하 분산 장치에 대 한 공용 IP와 관련 된 hello DNS 이름의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="d9451-147">hello 최종 FQDN 갖습니다 hello 형식의 *[이 매개 변수 값]*. *[region]* . cloudapp.azure.com 합니다. 예를 들어 hello 리소스 그룹은 배포 된 toohello 미국 서 부 지역 다음 항목은 최종 hello 및 deishbai32, hello 이름을 지정한 경우 FQDN tooyour 부하 분산 장치에 deishbai32.westus.cloudapp.azure.com 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="d9451-148">Hello 매개 변수 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-148">Save hello parameter file.</span></span> <span data-ttu-id="d9451-149">및 다음 Azure PowerShell을 사용 하 여 hello 클러스터를 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="d9451-150">또는 Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="d9451-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="d9451-151">Hello 리소스 그룹은 프로 비전 되 면 hello 그룹의에서 모든 리소스 hello Azure 클래식 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="d9451-152">표시 된 대로 다음 스크린 샷에서 hello hello에 세 개의 Vm이 있는 가상 네트워크를 포함 하는 리소스 그룹 toohello 조인 되는 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="d9451-153">hello 그룹에 연결 된 공용 ip 부하 분산 장치 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![hello Azure 클래식 포털에서 리소스 그룹을 프로 비전](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="d9451-155">Hello 클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="d9451-155">Install hello client</span></span>
<span data-ttu-id="d9451-156">필요한 **deisctl** toocontrol 프로그램 클러스터 Deis 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="d9451-157">Deisctl 모든 hello 클러스터 노드에 자동으로 설치 됩니다, 있지만 별도 관리 컴퓨터는 것이 좋습니다 toouse deisctl 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="d9451-158">또한 개인 IP 주소만 사용 하 여 모든 노드를 구성 하기 때문에 hello 부하 분산 된 공용 IP tooconnect toohello 노드 컴퓨터에 있는 통해 toouse SSH 터널링 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="d9451-159">hello 다음 단계가 hello deisctl를 별도 Ubuntu 물리적 또는 가상 컴퓨터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="d9451-160">deisctl 설치:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="d9451-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="d9451-161">개인 키 toossh 에이전트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="d9451-162">Deisct 구성:</span><span class="sxs-lookup"><span data-stu-id="d9451-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="d9451-163">hello 템플릿은 정의 2223 tooinstance 1, 매핑하는 인바운드 NAT 규칙 2224 tooinstance 2, 및 2225 tooinstance 3입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="d9451-164">이 hello deisctl 도구를 사용 하는 것에 대 한 중복성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="d9451-165">Azure 클래식 포털에서 이러한 규칙을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-165">You can examine these rules on Azure classic portal:</span></span>

![Hello 부하 분산 장치에서 NAT 규칙](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="d9451-167">현재 hello 템플릿 3 개 노드 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="d9451-168">이것은 루프 구문을 지원하지 않는 Azure 리소스 관리자 템플릿 NAT 규칙 정의의 제한 사항 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="d9451-169">설치 하 고 hello 시작 Deis 플랫폼</span><span class="sxs-lookup"><span data-stu-id="d9451-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="d9451-170">이제 deisctl tooinstall를 사용 하 고 hello 시작 플랫폼 Deis:</span><span class="sxs-lookup"><span data-stu-id="d9451-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="d9451-171">약간의 시간이 시작 hello 플랫폼 (으로 10 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="d9451-172">특히, hello 작성기 서비스를 시작 하는 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="d9451-173">몇 번의 시도 toosucceed 걸리는 경우에 따라 및: hello 작업 toohang를 것 같으면 라고 입력 해 보세요 `ctrl+c` toobreak 실행 hello 명령 및 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="d9451-174">사용할 수 있습니다 `deisctl list` tooverify 모든 서비스가 실행 중인 경우:</span><span class="sxs-lookup"><span data-stu-id="d9451-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="d9451-175">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-175">Congratulations!</span></span> <span data-ttu-id="d9451-176">이제 Azure에서 Deis 클러스터를 실행할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="d9451-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="d9451-177">다음으로 샘플 동작에서 Go 응용 프로그램 toosee hello 클러스터를 배포 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="d9451-178">Hello World 응용 프로그램 배포 및 확장</span><span class="sxs-lookup"><span data-stu-id="d9451-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="d9451-179">hello 다음 단계 표시 방법 toodeploy "Hello World"으로 응용 프로그램 toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="d9451-180">hello 단계에 기반 [설명서 Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="d9451-181">라우팅 메시 toowork hello에 대 한 적절 하 게 해야 toohave 와일드 카드 A 레코드 toohello hello 부하 분산 장치의 공용 IP를 가리키는 도메인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="d9451-182">hello 다음 스크린샷은 도메인을 등록 하는 샘플에 대 한 hello A 레코드 GoDaddy에:</span><span class="sxs-lookup"><span data-stu-id="d9451-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy A 레코드](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="d9451-184">deis 설치:</span><span class="sxs-lookup"><span data-stu-id="d9451-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="d9451-185">새 SSH 키를 만들고 공개 키 tooGitHub hello를 추가 (물론, 또한 다시 사용할 수 있습니다 프로그램 기존 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="d9451-186">toocreate 새 SSH 키 쌍을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="d9451-187">Id_rsa.pub, 또는 사용자가 선택한 tooGitHub의 hello 공개 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="d9451-188">SSH 키 구성 화면에서 hello 추가 SSH 키 단추를 사용 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub 키](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="d9451-190">새 사용자 등록:</span><span class="sxs-lookup"><span data-stu-id="d9451-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="d9451-191">Hello SSH 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="d9451-192">응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="d9451-193">
8.hello git 푸시 Docker 이미지 toobe를 빌드 및 배포, 몇 분 정도 걸리며를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="d9451-194">내 경험에서 경우에 따라 10 단계 (Pushing 이미지 tooprivate 리포지토리) 중단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="d9451-195">이런 경우 hello 프로세스를 중지할 수 있습니다 사용 하 여 제거 hello 응용 프로그램 ' 앱 deis: – destroy <application name> ` tooremove hello application and try again. You can use `apps:list deis' toofind 응용 프로그램의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="d9451-196">작동 하는 것, 명령 출력의 hello 끝에서 hello 다음과 같은 내용이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="d9451-197">Hello 응용 프로그램 작동 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="d9451-198">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="d9451-199">Hello 응용 프로그램 too3 인스턴스 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="d9451-200">사용할 수 있습니다 deis 응용 프로그램의 정보 tooexamine 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="d9451-201">hello 다음 출력은 내 응용 프로그램 배포:</span><span class="sxs-lookup"><span data-stu-id="d9451-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="d9451-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9451-202">Next Steps</span></span>
<span data-ttu-id="d9451-203">이 문서는 새 Deis 모든 hello 단계 tooprovision 단계는 Azure 리소스 관리자 템플릿을 사용 하 여 Azure에서 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="d9451-204">hello 템플릿에서 배포 된 응용 프로그램에 부하 분산 뿐 아니라 연결 tooling에 중복성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="d9451-205">hello 서식 파일에는 귀중 한 공용 IP 리소스를 저장 하 고 더욱 안전한 환경 toohost 응용 프로그램을 제공 하는 멤버 노드에 공용 Ip를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9451-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="d9451-206">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="d9451-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="d9451-207">[Azure Resource Manager 개요][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="d9451-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="d9451-208">[Toouse는 Azure CLI hello 하는 방법][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="d9451-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="d9451-209">[Azure Resource Manager로 Azure PowerShell 사용][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="d9451-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
