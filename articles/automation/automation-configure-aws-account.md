---
title: "Amazon 웹 서비스와 인증 aaaConfigure | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate AWS 리소스를 관리 하는 Azure 자동화에서 runbook에 대 한는 AWS 자격 증명의 유효성을 검사 합니다."
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
ms.date: 11/11/2016
ms.author: magoedte
ms.openlocfilehash: 6edaa000c1b206d80fe64b18c729dac124849070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a><span data-ttu-id="fe478-104">Amazon 웹 서비스로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="fe478-104">Authenticate Runbooks with Amazon Web Services</span></span>
<span data-ttu-id="fe478-105">AWS(Amazon 웹 서비스)의 리소스를 사용하여 일반 작업을 자동화하는 일은 Azure의 자동화 Runbook으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-105">Automating common tasks with resources in Amazon Web Services (AWS) can be accomplished with Automation runbooks in Azure.</span></span>  <span data-ttu-id="fe478-106">Azure의 리소스와 마찬가지로 자동화 Runbook을 사용하여 AWS에서 많은 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-106">You can automate many tasks in AWS using Automation runbooks just like you can with resources in Azure.</span></span>  <span data-ttu-id="fe478-107">다음 두 가지만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-107">All that is required are two things:</span></span>

* <span data-ttu-id="fe478-108">AWS 구독 및 일련의 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="fe478-108">An AWS subscription and a set of credentials.</span></span>  <span data-ttu-id="fe478-109">특히 AWS 액세스 키 및 비밀 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-109">Specifically your AWS Access Key and Secret Key.</span></span>  <span data-ttu-id="fe478-110">자세한 내용은 hello 문서를 검토 하십시오 [AWS 자격 증명을 사용 하 여](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-110">For more information, please review hello article [Using AWS Credentials](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).</span></span>
* <span data-ttu-id="fe478-111">Azure 구독 및 자동화 계정.</span><span class="sxs-lookup"><span data-stu-id="fe478-111">An Azure subscription and Automation account.</span></span>  <span data-ttu-id="fe478-112">Azure 자동화 계정 설정에 대 한 자세한 내용은 hello 문서를 검토 하십시오 [구성할 Azure 실행 계정](automation-sec-configure-azure-runas-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-112">For more information on setting up an Azure Automation account, please review hello article [Configure Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>  

<span data-ttu-id="fe478-113">AWS와 tooauthenticate를 지정 해야 AWS 자격 증명 tooauthenticate 집합이 Azure 자동화에서 실행 하는 runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-113">tooauthenticate with AWS, you must specify a set of AWS credentials tooauthenticate your runbooks running from Azure Automation.</span></span> <span data-ttu-id="fe478-114">생성 된 자동화 계정에 이미 있는 toouse AWS와 해당 tooauthenticate를 하려는 경우 다음 단원을 hello에 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-114">If you already have an Automation account created and you want toouse that tooauthenticate with AWS, you can follow hello steps in hello following section.</span></span>  <span data-ttu-id="fe478-115">Runbook 대상으로 하는 AWS 리소스에 대 한 계정을 toodedicated 하려는 경우 먼저 만들어야 새 [자동화 계정으로 실행 계정](automation-sec-configure-azure-runas-account.md) (건너뛸 hello 옵션 toocreate 서비스 사용자) 한 다음 아래 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-115">If you want toodedicated an account for runbooks targetting AWS resources, you should first create a new [Automation Run As account](automation-sec-configure-azure-runas-account.md) (skip hello option toocreate a service principal) and then follow hello steps below.</span></span>

## <a name="configure-automation-account"></a><span data-ttu-id="fe478-116">자동화 계정 구성</span><span class="sxs-lookup"><span data-stu-id="fe478-116">Configure Automation account</span></span>
<span data-ttu-id="fe478-117">Azure 자동화 toocommunicate AWS와,에 대 한 tooretrieve AWS 자격 증명이 필요 하 고 Azure 자동화에서 자산으로 보관해 먼저 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-117">For Azure Automation toocommunicate with AWS, you will first need tooretrieve your AWS credentials and store them as assets in Azure Automation.</span></span>  <span data-ttu-id="fe478-118">Hello AWS 문서에서 설명 하는 단계를 수행 하는 hello 수행 [AWS 계정에 대 한 액세스 키 관리](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate 액세스 키 및 복사 hello **액세스 키 ID** 및 **암호선택키** (선택적으로 키 파일 toostore 다운로드 안전한 곳 것).</span><span class="sxs-lookup"><span data-stu-id="fe478-118">Perform hello following steps documented in hello AWS document [Managing Access Keys for your AWS Account](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate an Access Key and copy hello **Access Key ID** and **Secret Access Key** (optionally download your key file toostore it somewhere safe).</span></span>

<span data-ttu-id="fe478-119">Azure 자동화 계정 toosecurely와 자격 증명 자산 toocreate 해야는 만들어 있습니다 AWS 보안 키를 복사한 후 저장 하 고 runbook으로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-119">After you have created and copied your AWS security keys, you will need toocreate a Credential asset with an Azure Automation account toosecurely store them and reference them with your runbooks.</span></span>  <span data-ttu-id="fe478-120">Hello 섹션의 hello 단계에 따라 **새 자격 증명 자산을 만드는** hello에 [자산에 Azure 자동화 자격 증명](automation-credentials.md) hello 다음 정보를 입력 하 고 문서:</span><span class="sxs-lookup"><span data-stu-id="fe478-120">Follow hello steps in hello section **Creating a new credential asset** in hello [Credential assets in Azure Automation](automation-credentials.md) article and enter hello following information:</span></span>

1. <span data-ttu-id="fe478-121">Hello에 **이름** 상자에 입력 **AWScred** 또는 명명 표준에 따라 적절 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-121">In hello **Name** box, enter **AWScred** or an appropriate value following your naming standards.</span></span>  
2. <span data-ttu-id="fe478-122">Hello에 **사용자 이름** 상자에 입력 하면 **액세스 ID** 하였고 **암호 액세스 키** hello에 **암호** 및 **확인 암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-122">In hello **User name** box type your **Access ID** and your **Secret Access Key** in hello **Password** and **Confirm password** box.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="fe478-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe478-123">Next steps</span></span>
* <span data-ttu-id="fe478-124">Reivew hello 솔루션 문서 [Amazon 웹 서비스에서 VM의 배포를 자동화](automation-scenario-aws-deployment.md) toolearn toocreate runbook tooautomate AWS에서 작업 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fe478-124">Reivew hello solution article [Automating deployment of a VM in Amazon Web Services](automation-scenario-aws-deployment.md) toolearn how toocreate runbooks tooautomate tasks in AWS.</span></span>

