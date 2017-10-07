---
title: "앱 서비스 웹 앱에 Linux FAQ aaaAzure | Microsoft Docs"
description: "Linux의 Azure App Service Web App에 대한 FAQ"
keywords: "Azure App Service, 웹앱, faq, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Linux의 Azure App Service Web App에 대한 FAQ

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Linux에서 웹 응용 프로그램의 hello 릴리스로 기능을 추가 하 고 개선 tooour 플랫폼 작업 중입니다. 다음은 몇 가지 질문과 대답 (FAQ) 고객 것은 무엇입니까 우리 hello를 통해 마지막 하는 달입니다.
Hello 문서에 설명 된 질문이 있는 경우에서는 가능한 한 빨리 대답 해 드리겠습니다.

## <a name="built-in-images"></a>기본 제공 이미지

**Q:** toofork hello 기본 제공 Docker는 컨테이너 hello 플랫폼을 제공 합니다. 이러한 파일은 어디서 찾을 수 있나요?

**A:** [GitHub](https://github.com/azure-app-service)에서 모든 Docker 파일을 찾을 수 있습니다. [Docker Hub](https://hub.docker.com/u/appsvc/)에서 모든 Docker 컨테이너를 찾을 수 있습니다.

**Q:** hello 런타임 스택을 구성 하면 시작 파일 섹션 hello에 대 한 예상 값 hello 무엇 인가요?

**A:** hello 오후 2 구성 파일 또는 스크립트 파일 지정에 대 한 Node.Js 합니다. .Net Core의 경우 컴파일된 DLL 이름을 지정해야 합니다. 에 대 한 Ruby를 hello Ruby 스크립트를 지정할 수 있습니다 되도록 tooinitialize 응용 프로그램을 합니다.

## <a name="management"></a>관리

**Q:** hello Azure 포털에서에서 hello 다시 시작 단추를 누를 때 어떻게 될까요?

**A:** 이 Docker 다시 해당 hello 됩니다.

**Q:** SSH (보안 셸) tooconnect toohello 앱 컨테이너 가상 컴퓨터 (VM) 사용할 수 있습니까?

**A:** 예, 할 수 있는 자세한 정보에 대 한 문서 검사 hello 다음 hello SCM 사이트를 통해 있는지 [Linux에서 웹 앱에 대 한 SSH 지원](./app-service-linux-ssh-support.md)

**Q:** toocreate SDK 또는 ARM 템플릿을 통해 Linux 응용 프로그램 서비스 평면 낮음, 얻을 수이 어떻게?

**A:** tooset hello 필요한 `reserved` hello 앱의 필드 너무 서비스`true`합니다.

## <a name="continuous-integrationdeployment"></a>지속적인 통합/배포

**Q:** hello 이미지 Docker 허브에서 업데이트 후 웹 응용 프로그램 이전 Docker 컨테이너 이미지를 계속 사용 합니다. 사용자 지정 컨테이너의 지속적인 통합/배포를 지원하나요?

**A:** 검사 hello 다음 문서에서 Azure 컨테이너 레지스트리 또는 DockerHub 이미지에 대 한 연속 통합/배포를 tooset [Linux에서 Azure 웹 앱과 함께 연속 배포](./app-service-linux-ci-cd.md)합니다. 사설 레지스트리에 대 한 중지 및 다음 웹 앱을 시작 하 여 hello 컨테이너를 새로 고칠 수 있습니다. 또는 변경 하거나 tooforce 컨테이너의 새로 고침 설정 더미 응용 프로그램을 추가할 수 있습니다.

**Q:** 스테이징 환경이 지원되나요?

**A:** 예.

**Q:** 를 사용할 수 있습니까 **웹 배포** toodeploy 웹 응용 프로그램?

**A:** 예, 앱이 필요한 tooset는 라고 `WEBSITE_WEBDEPLOY_USE_SCM` 너무`false`합니다.

## <a name="language-support"></a>언어 지원

**Q:** 컴파일되지 않은 .NET Core 앱을 지원하나요?

**A:** 예.

**Q:** 작성기를 PHP 앱의 종속성 관리자로 지원하나요?

**A:** 예. Git 배포 하는 동안 Kudu PHP 응용 프로그램 (composer.json 파일의 현재 상태 감사 toohello)를 배포 하는 사용자에 대 한 작성기 설치를 트리거할를 검색 해야 합니다.

## <a name="custom-containers"></a>사용자 지정 컨테이너

**Q:** 나만의 사용자 지정 컨테이너를 사용하고 있습니다. 내 앱 hello에 상주 `\home\` 디렉터리 하는데 hello를 사용 하 여 hello 콘텐츠 찾아보기 때 내 파일을 찾을 수 없는 [SCM 사이트](https://github.com/projectkudu/kudu) 또는 FTP 클라이언트입니다. 내 파일은 어디에 있나요?

**A:** SMB 공유 toohello 탑재 `\home\` 디렉터리입니다. 포함된 모든 콘텐츠를 재정의합니다.

**Q:** 나만의 사용자 지정 컨테이너를 사용하고 있습니다. Hello 플랫폼 toomount SMB 공유 toohello 하지 않으려는 `\home\`합니다.

**A:** hello 설정 하 여 할 수 있습니다 `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 앱 설정 너무`false`합니다.

**Q:** 내 사용자 지정 컨테이너 오랜 시간이 toostart 걸리고 전에 hello 플랫폼 다시 시작 hello 컨테이너가 시작 완료 된 합니다.

**A:** hello 플랫폼은 컨테이너를 다시 시작 하기 전에 대기 하는 hello 시간을 구성할 수 있습니다. Hello 설정 하 여이 작업을 수행할 수 있습니다 `WEBSITES_CONTAINER_START_TIME_LIMIT` 응용 프로그램 설정 toohello 원하는 값 (초)에서입니다. hello 기본값이 230 초 이며 최대 hello 600 초입니다.

**Q:** 개인 레지스트리 서버 url에 대 한 hello 형식 란?

**A:** tooprovide hello 전체 레지스트리 url 포함 하 여 필요한 `http://` 또는 `https://`합니다.

**Q:** hello 이미지 이름 개인 레지스트리 옵션에 대 한 hello 형식 란?

**A:** 않음 (예: hello 개인 등록 url을 포함 하 여 tooadd hello 전체 이미지 이름이 필요 myacr.azurecr.io/dotnet:latest).

**Q:** 내 사용자 지정 컨테이너 이미지에 tooexpose 둘 이상의 포트 합니다. 가능할까요?

**A:** 현재는 지원되지 않습니다.

**Q:** 사용자 고유의 저장소를 가져올 수 있나요?

**A:** 현재는 지원되지 않습니다.

**Q:** hello SCM 사이트에서 내 사용자 지정 컨테이너 파일 시스템이 나 실행 프로세스를 찾아볼 수 없습니다. 그 이유는 무엇입니까?

**A:** 별도 컨테이너에서 hello SCM 사이트를 실행 합니다. Hello 파일 시스템을 확인할 수 없습니다 또는 hello 응용 프로그램 컨테이너의 프로세스를 실행 합니다.

**Q:** 내 사용자 지정 컨테이너 tooa 포트 80 이외의 포트에서 수신 합니다. 내 앱 tooroute hello 요청 toothat 포트를 구성 하려면 어떻게 해야 합니까?

**A:** 자동 포트 검색 했으므로, 또한 라고 하는 응용 프로그램을 지정할 수 **WEBSITES_PORT**, 예상 hello 포트 번호의 hello 값을 지정 합니다. 이전에 hello를 사용 하 여 플랫폼 `PORT` 응용 프로그램 설정, म 계획 toodeprecate hello 사용 하 여가이 앱을 설정 하 고 있으며 toousing 이동 `WEBSITES_PORT` 단독으로 합니다.

**Q:** 필요 합니까 tooimplement HTTPS 사용자 지정 컨테이너 내에 있습니다.

**A:** hello 플랫폼 공유 hello 프런트엔드에서 HTTPS 종단을 처리 하는 아니오, 합니다.

## <a name="pricing-and-sla"></a>가격 및 SLA

**Q:** 무엇는 hello 가격 hello 공개 미리 보기를 사용 하는 동안?

**A:** 절반 hello hello 일반적인 Azure 앱 서비스 가격으로 앱에서 실행 되는 시간 수가 요금이 청구 됩니다. 즉, 이 일반 Azure App Service 가격에서 50% 할인이 적용됩니다.

## <a name="other"></a>기타

**Q:** 응용 프로그램 설정 이름에 지원 되는 hello 문자 무엇 인가요?

**A:** A-Z, a ~ z, 0-9를 사용 하 고 응용 프로그램 설정에 대 한 밑줄 hello 수 있습니다.

**Q:** 어디서 새 기능을 요청할 수 있나요?

**A:** hello에 여러분의 아이디어를 전송 하는 경우 [웹 앱 피드백 포럼](https://aka.ms/webapps-uservoice)합니다. 여러분의 아이디어의 "[Linux]" toohello 제목을 추가 합니다.

## <a name="next-steps"></a>다음 단계
* [Linux에서 Azure Web App이란?](app-service-linux-intro.md)
* [Linux의 Azure Web App에 대한 SSH 지원](./app-service-linux-ssh-support.md)
* [Azure App Service에서 스테이징 환경 설정](./web-sites-staged-publishing.md)
* [Linux에서 Azure 웹앱을 사용한 연속 배포](./app-service-linux-ci-cd.md)
