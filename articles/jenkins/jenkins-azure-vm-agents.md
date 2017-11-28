---
title: "Jenkins 연속 통합 하기 위해 Azure VM 에이전트를 aaaUse 합니다."
description: "Jenkins 슬레이브로 Azure VM 에이전트입니다."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="c3041-103">Jenkins와 연속 통합을 위해 Azure VM 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="c3041-104">이 퀵 스타트의 방법을 toouse hello Jenkins Azure VM 에이전트 플러그 인 toocreate Azure에서 요청 시 (Ubuntu) Linux 에이전트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3041-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3041-105">Prerequisites</span></span>

<span data-ttu-id="c3041-106">toocomplete이 빠른이 시작:</span><span class="sxs-lookup"><span data-stu-id="c3041-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="c3041-107">Jenkins 마스터 아직 없는 경우 hello로 시작할 수 있습니다 [솔루션 템플릿](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="c3041-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="c3041-108">너무 참조[Azure CLI 2.0과 함께 Azure 서비스 사용자를 만들](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) Azure 서비스 사용자를 아직 없는 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="c3041-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="c3041-109">Azure VM 에이전트 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="c3041-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="c3041-110">Hello에서 시작 하는 경우 [솔루션 템플릿을](install-jenkins-solution-template.md), hello Jenkins 마스터에 hello Azure VM 에이전트 플러그 인이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="c3041-111">그렇지 않으면 hello 설치 **Azure VM 에이전트** hello Jenkins 대시보드 내에서 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="c3041-112">Hello 플러그 인 구성</span><span class="sxs-lookup"><span data-stu-id="c3041-112">Configure hello plugin</span></span>

* <span data-ttu-id="c3041-113">Hello Jenkins 대시보드 내에서 클릭 **Jenkins 관리-> 시스템 구성->**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="c3041-114">Hello 페이지의 맨 아래 toohello 스크롤하여 hello 드롭다운이 있는 hello 섹션을 찾아 **새로운 클라우드 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="c3041-115">Hello 메뉴에서 선택 **Microsoft Azure VM 에이전트**</span><span class="sxs-lookup"><span data-stu-id="c3041-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="c3041-116">Hello Azure 자격 증명 드롭다운에서 기존 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="c3041-117">새 tooadd **Microsoft Azure 서비스 사용자** hello 다음 값을 입력: 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure 자격 증명](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="c3041-119">클릭 **확인 구성** toomake 해당 hello 프로필 구성이 올바른지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="c3041-120">Hello 구성을 저장 하 고 toohello 다음 단계를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="c3041-121">템플릿 구성</span><span class="sxs-lookup"><span data-stu-id="c3041-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="c3041-122">일반 구성</span><span class="sxs-lookup"><span data-stu-id="c3041-122">General configuration</span></span>
<span data-ttu-id="c3041-123">다음을 사용 하 여 toodefine Azure VM 에이전트에 대 한 템플릿을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="c3041-124">클릭 **추가** tooadd 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="c3041-125">새 템플릿의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="c3041-126">Hello 레이블에 대 한 "ubuntu"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="c3041-127">이 레이블은 hello 작업 구성 하는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="c3041-128">Hello 콤보 상자에서 원하는 지역을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="c3041-129">Select hello v M 크기를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="c3041-130">Hello Azure 저장소 계정 이름을 지정 하거나 빈 toouse hello 기본 이름이 "jenkinsarmst" 둡니다</span><span class="sxs-lookup"><span data-stu-id="c3041-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="c3041-131">Hello 보존 시간을 분 단위로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="c3041-132">이 설정은 Jenkins 유휴 에이전트를 자동으로 삭제 하기 전에 대기할 수 있는 시간 (분) hello 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="c3041-133">유휴 에이전트 toobe 자동으로 삭제 하지 않을 경우 0을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![일반 구성](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="c3041-135">이미지 구성</span><span class="sxs-lookup"><span data-stu-id="c3041-135">Image configuration</span></span>

<span data-ttu-id="c3041-136">Linux (Ubuntu) 에이전트 toocreate 선택 **참조 이미지** 및 사용 하 여 hello 구성을 한 예로 다음과 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="c3041-137">너무 참조[Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello에 대 한 최신 Azure 이미지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="c3041-138">이미지 게시자: Canonical</span><span class="sxs-lookup"><span data-stu-id="c3041-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="c3041-139">이미지 제품: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c3041-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="c3041-140">이미지 SKU: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="c3041-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="c3041-141">이미지 버전: 최신</span><span class="sxs-lookup"><span data-stu-id="c3041-141">Image version: latest</span></span>
* <span data-ttu-id="c3041-142">OS 유형: Linux</span><span class="sxs-lookup"><span data-stu-id="c3041-142">OS Type: Linux</span></span>
* <span data-ttu-id="c3041-143">시작 방법: SSH</span><span class="sxs-lookup"><span data-stu-id="c3041-143">Launch method: SSH</span></span>
* <span data-ttu-id="c3041-144">관리자 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="c3041-144">Provide an admin credentials</span></span>
* <span data-ttu-id="c3041-145">VM 초기화 스크립트의 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![이미지 구성](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="c3041-147">클릭 **확인 템플릿** tooverify hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="c3041-148">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="c3041-149">Jenkins에서 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c3041-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="c3041-150">Hello Jenkins 대시보드 내에서 클릭 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="c3041-151">이름을 입력하고 **프리스타일 프로젝트**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="c3041-152">Hello에 **일반** 탭, 선택 "프로젝트를 실행할 수 있는 제한" 및 "ubuntu" 레이블 식의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="c3041-153">이제 "ubuntu" hello 드롭다운에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="c3041-154">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-154">Click **Save**.</span></span>

![작업 설정](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="c3041-156">새 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="c3041-156">Build your new project</span></span>

* <span data-ttu-id="c3041-157">Toohello Jenkins 대시보드를 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="c3041-158">만든 마우스 오른쪽 단추로 클릭 hello 새 작업을 클릭 한 다음 **이제 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="c3041-159">빌드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-159">A build is kicked off.</span></span> 
* <span data-ttu-id="c3041-160">Hello 빌드가 완료 되 면 너무 이동**콘솔 출력이**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="c3041-161">Hello 빌드가 Azure에서 원격으로 수행 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3041-161">You see that hello build was performed remotely on Azure.</span></span>

![콘솔 출력](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="c3041-163">참조</span><span class="sxs-lookup"><span data-stu-id="c3041-163">Reference</span></span>

* <span data-ttu-id="c3041-164">Azure Friday 비디오: [Azure VM 에이전트를 사용하여 Jenkins와 연속 통합](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)(영문)</span><span class="sxs-lookup"><span data-stu-id="c3041-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="c3041-165">지원 정보 및 구성 옵션: [Azure VM 에이전트 Jenkins 플러그 인 Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="c3041-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

