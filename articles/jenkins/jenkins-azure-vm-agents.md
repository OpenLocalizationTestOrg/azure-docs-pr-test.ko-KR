---
title: "Jenkins와 연속 통합을 위해 Azure VM 에이전트를 사용합니다."
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
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="8eb3e-103">Jenkins와 연속 통합을 위해 Azure VM 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="8eb3e-104">이 빠른 시작에서는 Jenkins Azure VM 에이전트 플러그 인을 사용하여 Azure에서 주문형 Linux(Ubuntu)를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8eb3e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8eb3e-105">Prerequisites</span></span>

<span data-ttu-id="8eb3e-106">이 빠른 시작을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-106">To complete this quickstart:</span></span>

* <span data-ttu-id="8eb3e-107">Jenkins 마스터가 아직 없는 경우 [솔루션 템플릿](install-jenkins-solution-template.md)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="8eb3e-108">Azure 서비스 주체가 아직 없는 경우 [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="8eb3e-109">Azure VM 에이전트 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="8eb3e-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="8eb3e-110">[솔루션 템플릿](install-jenkins-solution-template.md)에서 시작하는 경우 Azure VM 에이전트 플러그 인이 Jenkins 마스터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="8eb3e-111">그렇지 않은 경우 Jenkins 대시보드 내에서 **Azure VM 에이전트** 플러그 인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="8eb3e-112">플러그 인 구성</span><span class="sxs-lookup"><span data-stu-id="8eb3e-112">Configure the plugin</span></span>

* <span data-ttu-id="8eb3e-113">Jenkins 대시보드 내에서 **Manage Jenkins -> Configure System ->**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="8eb3e-114">페이지 아래로 스크롤하고 **새 클라우드 추가** 드롭다운이 있는 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="8eb3e-115">메뉴에서 **Microsoft Azure VM 에이전트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="8eb3e-116">Azure 자격 증명 드롭다운에서 기존 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="8eb3e-117">새 **Microsoft Azure 서비스 주체**를 추가하려면 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure 자격 증명](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="8eb3e-119">**구성 확인**을 클릭하여 프로필 구성이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="8eb3e-120">구성을 저장하고 다음 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="8eb3e-121">템플릿 구성</span><span class="sxs-lookup"><span data-stu-id="8eb3e-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="8eb3e-122">일반 구성</span><span class="sxs-lookup"><span data-stu-id="8eb3e-122">General configuration</span></span>
<span data-ttu-id="8eb3e-123">다음으로, Azure VM 에이전트를 정의하는 데 사용할 템플릿을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="8eb3e-124">**추가**를 클릭하여 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="8eb3e-125">새 템플릿의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="8eb3e-126">레이블에 "ubuntu"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="8eb3e-127">이 레이블은 작업을 구성하는 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="8eb3e-128">콤보 상자에서 원하는 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="8eb3e-129">원하는 VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-129">Select the desired VM size.</span></span>
* <span data-ttu-id="8eb3e-130">Azure Storage 계정 이름을 지정하거나 비워 두어 기본 이름인 "jenkinsarmst"를 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="8eb3e-131">보존 시간을 분 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="8eb3e-132">이 설정은 Jenkins가 유휴 에이전트를 자동으로 삭제할 때까지 대기할 수 있는 시간(분)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="8eb3e-133">유휴 에이전트를 자동으로 삭제하지 않으려는 경우 0을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![일반 구성](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="8eb3e-135">이미지 구성</span><span class="sxs-lookup"><span data-stu-id="8eb3e-135">Image configuration</span></span>

<span data-ttu-id="8eb3e-136">Linux(Ubuntu) 에이전트를 만들려면 **이미지 참조**를 선택하고 예를 들어 다음 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="8eb3e-137">Azure에서 지원하는 최신 이미지는 [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="8eb3e-138">이미지 게시자: Canonical</span><span class="sxs-lookup"><span data-stu-id="8eb3e-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="8eb3e-139">이미지 제품: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="8eb3e-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="8eb3e-140">이미지 SKU: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="8eb3e-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="8eb3e-141">이미지 버전: 최신</span><span class="sxs-lookup"><span data-stu-id="8eb3e-141">Image version: latest</span></span>
* <span data-ttu-id="8eb3e-142">OS 유형: Linux</span><span class="sxs-lookup"><span data-stu-id="8eb3e-142">OS Type: Linux</span></span>
* <span data-ttu-id="8eb3e-143">시작 방법: SSH</span><span class="sxs-lookup"><span data-stu-id="8eb3e-143">Launch method: SSH</span></span>
* <span data-ttu-id="8eb3e-144">관리자 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="8eb3e-144">Provide an admin credentials</span></span>
* <span data-ttu-id="8eb3e-145">VM 초기화 스크립트의 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![이미지 구성](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="8eb3e-147">**템플릿 확인**을 클릭하여 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="8eb3e-148">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="8eb3e-149">Jenkins에서 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="8eb3e-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="8eb3e-150">Jenkins 대시보드 내에서 **New Item**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="8eb3e-151">이름을 입력하고 **프리스타일 프로젝트**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="8eb3e-152">**일반** 탭에서 [Restrict where project can be run(프로젝트를 실행할 수 있는 위치 제한)]을 선택하고 레이블 식에 "ubuntu"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="8eb3e-153">이제 드롭다운에 "ubuntu"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="8eb3e-154">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-154">Click **Save**.</span></span>

![작업 설정](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="8eb3e-156">새 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="8eb3e-156">Build your new project</span></span>

* <span data-ttu-id="8eb3e-157">Jenkins 대시보드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="8eb3e-158">만든 새 작업을 마우스 오른쪽 단추로 클릭하고 **지금 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="8eb3e-159">빌드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-159">A build is kicked off.</span></span> 
* <span data-ttu-id="8eb3e-160">빌드가 완료되면 **콘솔 출력**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="8eb3e-161">해당 빌드가 Azure에서 원격으로 수행된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb3e-161">You see that the build was performed remotely on Azure.</span></span>

![콘솔 출력](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="8eb3e-163">참조</span><span class="sxs-lookup"><span data-stu-id="8eb3e-163">Reference</span></span>

* <span data-ttu-id="8eb3e-164">Azure Friday 비디오: [Azure VM 에이전트를 사용하여 Jenkins와 연속 통합](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)(영문)</span><span class="sxs-lookup"><span data-stu-id="8eb3e-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="8eb3e-165">지원 정보 및 구성 옵션: [Azure VM 에이전트 Jenkins 플러그 인 Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="8eb3e-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

