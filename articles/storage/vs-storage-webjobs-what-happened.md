---
title: "aaaWhat 발생 toomy WebJob 프로젝트 (Visual Studio Azure 저장소 서비스를 연결 하는 데 사용)? | Microsoft Docs"
description: "연결 된 서비스를 Visual Studio를 사용 하 여 tooa 저장소 계정을 연결 후 Azure WebJob 프로젝트의 내용에 대해 설명"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 7735f49b1e7ec8dda30d1262d7ce65454604b610
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webjob-project-visual-studio-azure-storage-connected-service"></a>어떤 발생 했습니다 toomy WebJob 프로젝트 (Visual Studio Azure 저장소 서비스를 연결 하는 데 사용)?
## <a name="references-added"></a>참조 추가됨
hello Azure 저장소 NuGet 패키지에는 Visual Studio 프로젝트에서 업데이트 tooor를 추가 되었습니다.  
이 패키지는 hello 다음.NET 참조를 추가 합니다.

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.ConfigurationManager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>추가된 Azure 저장소에 대한 연결 문자열
Hello 프로젝트의 App.config 파일에서 hello **AzureWebJobsStorage** 및 **AzureWebJobsDashboard** hello 선택한 저장소 계정 연결 문자열 및 키와 함께 항목이 업데이트 되었습니다.

자세한 내용은 [Azure WebJob 설명서 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.

