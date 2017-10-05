---
title: "Amazon 웹 서비스로 인증 구성 | Microsoft Docs"
description: "이 문서에서는 Azure 자동화에서 AWS 리소스를 관리하는 Runbook에 대한 AWS 자격 증명을 만들고 유효성을 검사하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "aws 인증, aws 구성"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 81e5e5d56a7e6149409e11aca2e5fdf28d6a7134
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a><span data-ttu-id="04b35-104">Amazon 웹 서비스로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="04b35-104">Authenticate Runbooks with Amazon Web Services</span></span>
<span data-ttu-id="04b35-105">AWS(Amazon 웹 서비스)의 리소스를 사용하여 일반 작업을 자동화하는 일은 Azure의 자동화 Runbook으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-105">Automating common tasks with resources in Amazon Web Services (AWS) can be accomplished with Automation runbooks in Azure.</span></span>  <span data-ttu-id="04b35-106">Azure의 리소스와 마찬가지로 자동화 Runbook을 사용하여 AWS에서 많은 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-106">You can automate many tasks in AWS using Automation runbooks just like you can with resources in Azure.</span></span>  <span data-ttu-id="04b35-107">다음 두 가지만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-107">All that is required are two things:</span></span>

* <span data-ttu-id="04b35-108">AWS 구독 및 일련의 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="04b35-108">An AWS subscription and a set of credentials.</span></span>  <span data-ttu-id="04b35-109">특히 AWS 액세스 키 및 비밀 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-109">Specifically your AWS Access Key and Secret Key.</span></span>  <span data-ttu-id="04b35-110">자세한 내용은 [AWS 자격 증명 사용](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04b35-110">For more information, please review the article [Using AWS Credentials](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).</span></span>
* <span data-ttu-id="04b35-111">Azure 구독 및 자동화 계정.</span><span class="sxs-lookup"><span data-stu-id="04b35-111">An Azure subscription and Automation account.</span></span>  <span data-ttu-id="04b35-112">Azure Automation 계정 설정에 대한 자세한 내용은 [Azure 실행 계정 구성](automation-sec-configure-azure-runas-account.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04b35-112">For more information on setting up an Azure Automation account, please review the article [Configure Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>  

<span data-ttu-id="04b35-113">AWS에 인증하려면 Azure 자동화에서 실행 중인 Runbook을 인증하도록 AWS 자격 증명을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-113">To authenticate with AWS, you must specify a set of AWS credentials to authenticate your runbooks running from Azure Automation.</span></span> <span data-ttu-id="04b35-114">이미 자동화 계정을 만들었고 해당 계정을 사용하여 AWS에 인증하려면 다음 섹션의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="04b35-114">If you already have an Automation account created and you want to use that to authenticate with AWS, you can follow the steps in the following section.</span></span>  <span data-ttu-id="04b35-115">AWS 리소스를 대상으로 하는 Runbook 전용 계정을 지정하려면 먼저 새 [Automation 계정](automation-offering-get-started.md) 을 만든 다음 아래 단계를 따라야 합니다(서비스 주체를 만드는 옵션은 건너뜀).</span><span class="sxs-lookup"><span data-stu-id="04b35-115">If you want to dedicated an account for runbooks targetting AWS resources, you should first create a new [Automation account](automation-offering-get-started.md) (skip the option to create a service principal) and then follow the steps below.</span></span>

## <a name="configure-automation-account"></a><span data-ttu-id="04b35-116">자동화 계정 구성</span><span class="sxs-lookup"><span data-stu-id="04b35-116">Configure Automation account</span></span>
<span data-ttu-id="04b35-117">Azure Automation가 AWS와 통신하려면 먼저 AWS 자격 증명을 검색하여 Azure Automation에 자산으로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-117">For Azure Automation to communicate with AWS, you first need to retrieve your AWS credentials and store them as assets in Azure Automation.</span></span>  <span data-ttu-id="04b35-118">AWS 문서 [AWS 계정에 대한 선택키 관리](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)에 설명된 다음 단계를 수행하여 선택키를 만들고 **액세스 키 ID** 및 **암호 선택키**를 복사합니다(필요에 따라 키 파일을 다운로드하여 안전한 곳에 저장).</span><span class="sxs-lookup"><span data-stu-id="04b35-118">Perform the following steps documented in the AWS document [Managing Access Keys for your AWS Account](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) to create an Access Key and copy the **Access Key ID** and **Secret Access Key** (optionally download your key file to store it somewhere safe).</span></span>

<span data-ttu-id="04b35-119">AWS 보안 키를 만들어서 복사한 후에는 보안 키를 안전하게 보관하고 Runbook에서 참조할 수 있도록 Azure Automation 계정으로 자격 증명 자산을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-119">After you have created and copied your AWS security keys, you need to create a Credential asset with an Azure Automation account to securely store them and reference them with your runbooks.</span></span>  <span data-ttu-id="04b35-120">[Azure Automation의 자격 증명 자산](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) 문서에 있는 **새 자격 증명을 만들려면** 섹션의 단계에 따라 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-120">Follow the steps in the section **To create a new credential** in the [Credential assets in Azure Automation](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) article and enter the following information:</span></span>

1. <span data-ttu-id="04b35-121">**이름** 상자에 **AWScred**를 입력하거나 본인의 명명 기준에 따라 적합한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-121">In the **Name** box, enter **AWScred** or an appropriate value following your naming standards.</span></span>  
2. <span data-ttu-id="04b35-122">**사용자 이름** 상자에 **액세스 ID**를 입력하고 **암호** 및 **암호 확인** 상자에 **암호 선택키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-122">In the **User name** box type your **Access ID** and your **Secret Access Key** in the **Password** and **Confirm password** box.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="04b35-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04b35-123">Next steps</span></span>
* <span data-ttu-id="04b35-124">솔루션 문서 [Amazon 웹 서비스에서 VM 배포 자동화](automation-scenario-aws-deployment.md)를 검토하여 AWS에서 작업을 자동화하는 Runbook을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04b35-124">Reivew the solution article [Automating deployment of a VM in Amazon Web Services](automation-scenario-aws-deployment.md) to learn how to create runbooks to automate tasks in AWS.</span></span>

