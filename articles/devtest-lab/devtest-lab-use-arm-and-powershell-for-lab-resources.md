---
title: "aaaCreate 또는 자동으로 Azure 리소스 관리자 템플릿을 사용 하 여 PowerShell과 함께 랩 수정 | Microsoft Docs"
description: "자세한 내용은 방법 PowerShell toocreate 사용 하 여 Azure 리소스 관리자 템플릿을 toouse 또는 랩 DevTest lab에 자동으로 수정"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Azure Resource Manager 템플릿 및 PowerShell을 사용하여 랩 자동 생성 또는 수정

DevTest Labs는 새 랩을 빠르게 자동 생성하거나 기존 랩을 수정한 다음 이러한 리소스를 배포하는 데 유용한 여러 Azure Resource Manager 템플릿 및 PowerShell 스크립트를 제공합니다.

이 문서에서는 이러한 서식 파일 및 스크립트 tooautomate hello 생성, 수정 및 환경에서의 배포를 사용 하 여 hello 과정을 단계별로 안내 합니다. 또한 이렇게 하면 방식과 toouse PowerShell tooperform 몇 가지 일반적인 작업의 DevTest Labs 하는 방법에 대 한 자세한 정보를 찾을 수 있습니다.

## <a name="step-1-gather-your-templates-and-scripts"></a>1단계: 템플릿 및 스크립트 수집
공용 [Github 리포지토리](https://github.com/Azure/azure-devtestlab)에서 미리 만들어진 [Azure Resource Manager 템플릿](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) 및 [PowerShell 스크립트](https://github.com/Azure/azure-devtestlab/tree/master/Scripts)를 찾을 수 있습니다. 그대로 사용하거나 요구 사항에 맞게 사용자 지정하고 [개인 Git 리포지토리](devtest-lab-add-artifact-repo.md)에 저장합니다. 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>2단계: Azure Resource Manager 템플릿 수정
Hello 단계에 따르면 [첫 번째 Azure 리소스 관리자 서식 파일 만들기](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) 하지 이전에 템플릿을 만든 경우.

또한 [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) 많은 지침과 제안 사항 toohelp 제공 신뢰할 수 있는 쉽고 toouse은 Azure 리소스 관리자 템플릿을 만들어야 합니다. 일반적으로 hello 접근 방식 중 하나에의 한 종류로 사용할지, 아니면 예제 제공 및 필요에 따라 서식 파일을 수정 합니다.

## <a name="step-3-deploy-resources-with-powershell"></a>3단계: PowerShell로 리소스 배포
서식 파일 및 스크립트를 지정한 후 같이 hello 필요한 너무[리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)합니다. hello 문서 리소스 tooAzure Azure 리소스 관리자 템플릿 toodeploy Azure PowerShell을 사용 하는 방법에 대 한 일반 정보를 제공 합니다.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>PowerShell을 사용하여 DevTest 랩에서 수행할 수 있는 일반 작업
PowerShell을 사용하여 자동화할 수 있는 다양한 일반 작업이 있습니다. hello hello 설명서의 다음 섹션에서는 hello 단계 필요한 tooperform 이러한 작업 개요입니다.

* [PowerShell을 사용하여 VHD 파일에서 사용자 지정 이미지 만들기](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [PowerShell을 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드](devtest-lab-upload-vhd-using-powershell.md)
* [PowerShell을 사용 하는 외부 사용자 tooa 랩을 추가합니다](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [PowerShell을 사용하여 랩 사용자 지정 역할 만들기](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>다음 단계
* 자세한 방법을 toocreate는 [개인 Git 리포지토리에](devtest-lab-add-artifact-repo.md) 사용자 지정된 서식 파일이 나 스크립트에 저장 됩니다.
* Hello 탐색 [Azure 빠른 시작 템플릿 갤러리에서 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates)합니다.
