---
title: "Azure에서 Linux VM에 응용 프로그램 프레임워크 배포 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 Linux VM에 널리 사용되는 응용 프로그램 프레임워크를 만들어 Active Directory, Docker 등을 설치합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 90e95919-4611-40d7-8fa8-e38facbde9a7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rasquill
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5d0d064c0afc4a9a5cb802fce66e219d23dc1ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-popular-application-frameworks-on-linux-using-azure-resource-manager-templates"></a><span data-ttu-id="5950c-103">Azure Resource Manager 템플릿을 사용하여 Linux에서 널리 사용되는 응용 프로그램 프레임워크 배포</span><span class="sxs-lookup"><span data-stu-id="5950c-103">Deploy popular application frameworks on Linux using Azure Resource Manager templates</span></span>

<span data-ttu-id="5950c-104">워크로드를 수행하려면 일반적으로 여러 리소스가 설계에 따라 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5950c-104">Workloads usually require many resources to function according to design.</span></span> <span data-ttu-id="5950c-105">Azure 리소스 관리자 템플릿을 통해 응용 프로그램이 구성되는 방식뿐만 아니라 구성된 응용 프로그램을 지원하기 위해 리소스를 배포하는 방식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5950c-105">Azure Resource Manager templates make it possible for you to not only define how applications are configured, but also how the resources are deployed to support configured applications.</span></span> <span data-ttu-id="5950c-106">이 문서는 갤러리에서 가장 널리 사용되는 템플릿을 소개하고 Azure 포털, Azure CLI, 또는 PowerShell을 사용하여 배포하는 것에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5950c-106">This article introduces you to the most popular templates in the gallery and gives you information for using the Azure portal, Azure CLI, or PowerShell to deploy them.</span></span>

[!INCLUDE [virtual-machines-common-app-frameworks](../../../includes/virtual-machines-common-app-frameworks.md)]

