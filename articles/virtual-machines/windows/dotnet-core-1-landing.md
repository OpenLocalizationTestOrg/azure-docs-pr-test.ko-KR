---
title: "Windows 가상 컴퓨터 DotNet 코어 자습서 1 aaaAzure | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 14d5f250-1f76-49d4-898f-07b58fd39e7c
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8df69c496f44acb02d8afc45695349ec1f558f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toowindows-virtual-machines"></a>응용 프로그램 배포 tooWindows 가상 컴퓨터를 자동화합니다.

네 부분으로 구성된 이 시리즈에서는 Azure Resource Manager 템플릿을 사용하여 Azure 리소스 및 응용 프로그램을 배포 및 구성하는 과정을 자세히 설명합니다. 이 시리즈의 샘플 템플릿은 배포 되 고 hello 배포 템플릿을 검사. 이 시리즈의 hello 목표는 Azure 리소스 간의 hello 관계에 tooeducate 및 tooprovide 직접 경험 완전히 통합 된 Azure 리소스 관리자 템플릿을 배포 합니다. 이 문서에서는 Azure Resource Manager에 대한 기본적인 지식이 있다고 가정하므로 이 자습서를 시작하기 전에 기본적인 Azure Resource Manager 개념을 숙지하시기 바랍니다.

## <a name="music-store-application"></a>Music Store 응용 프로그램
hello이 시리즈에 사용 된 샘플은.Net Core 응용 프로그램 쇼핑 음악 스토어를 시뮬레이션 합니다. 이 응용 프로그램에 배포 된 tooeither Linux 또는 Windows 가상 시스템에서 배포 둘 다에 대해 생성 된 샘플 수 있습니다. hello 응용 프로그램에 웹 응용 프로그램과 SQL 데이터베이스에 포함 됩니다. 이 시리즈의 hello 기사를 읽기 전에이 페이지에 있는 hello 배포 단추를 사용 하 여 hello 응용 프로그램을 배포 합니다. 완전히 배포 되 면 hello 응용 프로그램 / Azure 아키텍처 유사 다이어그램을 다음 hello 합니다. 

hello 음악 스토어 리소스 관리자 템플릿을 찾을 수 있습니다, [음악 스토어 Windows 템플릿](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)

![Music Store 응용 프로그램](./media/dotnet-core-1-landing/music-store.png)

Hello를 포함 하 여 이러한 구성 요소 각각 hello 다음 4 개의 문서에서에서 JSON를 검사 하는 서식 파일을 연결 합니다.

* [**응용 프로그램 아키텍처** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – 웹 사이트와 같은 응용 프로그램 구성 요소 및 데이터베이스 가상 컴퓨터 및 Azure SQL 데이터베이스와 같은 Azure 컴퓨터 리소스에서 호스팅되는 toobe 필요 합니다. 이 문서 매핑 계산 필요, tooAzure 리소스 및 Azure 리소스 관리자 템플릿 사용 하 여 이러한 리소스 배포를 안내 합니다. 
* [**액세스 및 보안** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – Azure에서 응용 프로그램 호스팅, 경우에 필요한 tooconsider hello 응용 프로그램에 액세스 하는 방법 및 다른 응용 프로그램 구성 요소는 서로 액세스 하는 방법입니다. 이 문서를 제공 하 고 인터넷 액세스 tooan 응용 프로그램 및 응용 프로그램 구성 요소 간의 액세스 보안을 자세히 설명 합니다.
* [**가용성과 규모** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – 가용성과 규모 참조 toohello 응용 프로그램 기능 toostay 인프라 가동 중지 시간 중에 실행 하 고 hello 기능 tooscale 리소스 toomeet 응용 프로그램의 요구를 계산 합니다. 이 문서 정보 hello 구성 요소는 부하 분산 된 toodeploy 및 항상 사용 가능한 응용 프로그램에 필요 합니다.
* [**응용 프로그램 배포** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) -이 응용 프로그램에 Azure 가상 컴퓨터, hello 메서드는 hello 하 여 응용 프로그램 이진 파일 hello 가상 컴퓨터에 설치 된 배포를 고려해 야 합니다. 이 문서에서는 Azure 가상 컴퓨터 사용자 지정 스크립트 확장을 사용하여 응용 프로그램 설치를 자동화하는 방법을 자세히 설명합니다.

hello 목표 Azure 리소스 관리자 템플릿을 개발 하는 경우에 Azure 인프라 및 hello 설치의 tooautomate hello 배포 하 고이 Azure 인프라에서 호스트 되는 모든 응용 프로그램의 구성입니다. 이러한 문서를 따라 작업하면서 이러한 작업의 예제를 볼 수 있습니다.

## <a name="deploy-hello-music-store-application"></a>Hello 음악 스토어 응용 프로그램 배포
이 단추를 사용 하 여 hello 음악 스토어 응용 프로그램을 배포할 수 있습니다.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

hello Azure Resource Manager 템플릿에 다음 매개 변수 값에는 hello가 필요 합니다.

| 매개 변수 이름 | 설명 |
| --- | --- |
| ADMINUSERNAME |Hello 가상 컴퓨터와 hello Azure SQL 데이터베이스에 사용 되는 관리 사용자 이름입니다. |
| ADMINPASSWORD |Hello Azure 가상 컴퓨터와 SQL 데이터베이스에 사용 되는 암호입니다. |
| NUMBEROFINSTANCES |만든 가상 컴퓨터 toobe hello 수입니다. 이러한 가상 컴퓨터 호스트 hello 음악 스토어 웹 응용 프로그램의 각 및 모든 트래픽의 부하 균형을입니다. |
| PUBLICIPADDRESSDNSNAME |Hello 공용 IP 주소와 연결 된 전역 고유 DNS 이름입니다. |

Hello 템플릿 배포 완료 되 면 toohello 인터넷 브라우저를 사용 하 여 공용 IP 주소를 찾습니다. hello.Net Core 음악 사이트 나타납니다.

## <a name="next-steps"></a>다음 단계
<hr>

[1단계 - Azure Resource Manager 템플릿을 사용하는 응용 프로그램 아키텍처](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[2단계 - Azure Resource Manager 템플릿의 액세스 및 보안](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[3단계 - Azure Resource Manager 템플릿의 가용성 및 크기 조정](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[4단계 - Azure Resource Manager 템플릿을 사용한 응용 프로그램 배포](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

