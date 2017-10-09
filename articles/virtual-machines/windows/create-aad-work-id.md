---
title: "Windows 용 AAD에서에서 회사 또는 학교 id aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Windows 가상 컴퓨터와 Azure Active Directory toouse에 회사 또는 학교 id입니다."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: dd6e2381fd0aa503483aa786b36232e557729c4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a><span data-ttu-id="5e2f4-103">회사 또는 학교 id를 Windows Vm과 Azure Active Directory toouse에서 만들기</span><span class="sxs-lookup"><span data-stu-id="5e2f4-103">Creating a Work or School identity in Azure Active Directory toouse with Windows VMs</span></span>
<span data-ttu-id="5e2f4-104">있고 사용 hello MSDN Azure 크레딧-활용 Azure 계정 tootake hello를 만든 개인 Azure 계정 키를 만들거나 개인 MSDN 구독이 있는 경우는 *Microsoft 계정* identity toocreate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e2f4-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="5e2f4-105">-Azure의 많은 뛰어난 기능 [리소스 그룹 템플릿](../../azure-resource-manager/resource-group-overview.md) -한 가지 예는 회사 또는 학교 계정 (Azure Active Directory에서 관리 하는 id)를 필요한 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2f4-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="5e2f4-106">다행히 새 회사 또는 학교 toocreate를 사용할 수 있는 기본 Azure Active Directory 도메인으로 제공 되 hello 개인 Azure 계정에 대 한 가장 큰 이점 중 하나 때문에, 새 회사 또는 학교 계정 toocreate 아래 hello 지침을 따를 수 있습니다. 필요로 하는 Azure 기능과 함께 사용할 수 있는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5e2f4-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="5e2f4-107">그러나 최근 변경 내용을 쉽게 가능한 toomanage hello를 사용 하 여 Azure 계정 유형으로 구독 `azure login` 설명 하는 대화형 로그인 방법을 [여기](../../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2f4-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="5e2f4-108">해당 메커니즘을 사용할 수 있습니다 또는 hello 설명 하는 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2f4-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="5e2f4-109">수도 있습니다 [Linux vm이 Azure Active Directory toouse에 회사 또는 학교 id를 만들](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2f4-109">You can also [create a work or school identity in Azure Active Directory toouse with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

