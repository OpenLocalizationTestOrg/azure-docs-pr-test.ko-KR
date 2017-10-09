---
title: "Chef와 가상 컴퓨터 배포 aaaAzure | Microsoft Docs"
description: "가상 컴퓨터 배포 및 구성 Microsoft Azure에서 Chef toodo toouse 자동화 하는 방법을 알아봅니다"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Chef를 사용하여 Azure 가상 컴퓨터 배포 자동화
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef는 자동화 및 필요한 상태 구성을 제공하는 유용한 도구입니다.

최신 클라우드 api 릴리스 Azure과의 원활한 통합을 제공 하는 Chef, 기능 tooprovision hello 수 있도록 하며 단일 명령을 통해 구성 상태를 배포 합니다.

이 문서에서는 알려드리겠습니다 방법을 tooset Chef 환경 tooprovision Azure 가상를 설치 하 고 정책 또는 "도움말"을 만들고이 cookbook tooan Azure 가상 컴퓨터를 배포 하는 과정을 안내 합니다.

시작해 보겠습니다.

## <a name="chef-basics"></a>Chef 기본 사항
시작 하기 전에 것이 좋습니다 hello Chef의 기본 개념을 검토 합니다. 훌륭한 자료가 <a href="http://www.chef.io/chef" target="_blank">여기</a> 에 있으니 연습에 앞서 빠르게 읽어 보시기 바랍니다. 그러나 시작 하기 전에 hello 기본 사항을 요약해 보겠습니다는 I.

다음 다이어그램 hello hello 개략적인 Chef 아키텍처를 보여 줍니다.

![][2]

Chef에는 Chef 서버, Chef 클라이언트(노드) 및 Chef 워크스테이션 등의 세 가지 주요 아키텍처 구성 요소가 있습니다.

hello Chef 서버는이 관리 지점 및 Chef 서버 hello에 대 한 두 가지가 있습니다: 호스팅된 솔루션이 나 온-프레미스 솔루션입니다. 여기에서는 호스트 솔루션을 사용합니다.

hello Chef 클라이언트 (노드)는 관리 하는 hello 서버에 있는 hello 에이전트입니다.

hello Chef 워크스테이션은 우리의 관리자 워크스테이션 우리의 정책을 만들 म 및 우리의 관리 명령을 실행 합니다. Hello 실행 **knife** 인프라에서 Chef 워크스테이션 toomanage hello 명령입니다.

"Cookbook" 및 "레시피" hello 개념 이기도합니다. 이들은 효율적으로 정의 하 고 적용 tooour 서버 hello 정책입니다.

## <a name="preparing-hello-workstation"></a>Hello 워크스테이션 준비
첫째, 준비 hello 워크스테이션을 수 있습니다. 여기서는 표준 Windows 워크스테이션을 사용합니다. 이러한 구성 파일과 cookbook toocreate 디렉터리 toostore 필요합니다.

먼저 C:\chef라는 디렉터리를 만듭니다.

그런 다음 c:\chef\cookbooks라는 두 번째 디렉터리를 만듭니다.

이제 필요 toodownload 쿼리하여 Azure 설정 파일 Chef 구독을 사용 하 여 통신할 수 있도록 합니다.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
다운로드 프로그램 hello Azure PowerShell을 사용 하 여 설정을 게시 [Get-azurepublishsettingsfile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) 명령입니다. 

Hello 저장 C:\chef에서 게시 설정 파일입니다.

## <a name="creating-a-managed-chef-account"></a>관리되는 Chef 계정 만들기
[여기](https://manage.chef.io/signup)에 호스트되는 Chef 계정에 등록합니다.

Hello 등록 프로세스 동안 됩니다 toocreate 새 조직을 라는 메시지가 표시 됩니다.

![][3]

조직 만들어지면 hello 시작 키트를 다운로드 합니다.

![][4]

> [!NOTE]
> 키 재설정 될 것 이라는 것을 경고 하는 메시지가 표시 되 면 아직 구성 된 기존 인프라가 없는 있으므로 확인 tooproceed 됩니다.
> 
> 

이 시작 키트 zip 파일에는 조직 구성 파일 및 키가 포함되어 있습니다.

## <a name="configuring-hello-chef-workstation"></a>Hello Chef 워크스테이션 구성
Hello chef starter.zip tooC:\chef의 hello 콘텐츠를 추출 합니다.

Chef starter\chef repo 아래에 있는 모든 파일을 복사\.chef tooyour c:\chef 디렉터리입니다.

디렉터리는 이제 비슷합니다 다음 예제는 hello 합니다.

![][5]

Hello Azure 게시 파일을 포함 하 여 c:\chef의 hello 루트에서 4 개의 파일을 만들었습니다.

hello PEM 파일 hello knife.rb 파일 knife 구성을 포함 하는 동안 사용자의 조직 및 관리자 통신에 대 한 개인 키를 포함 합니다. Tooedit hello knife.rb 파일이 필요 합니다.

Hello 파일에서 원하는 편집기를 열고 cookbook_path"hello" hello를 제거 하 여 수정 /... / hello 경로 같이 다음에 표시 되도록 합니다.

    cookbook_path  ["#{current_dir}/cookbooks"]

추가적으로 hello 다음 줄에서는 Azure의 반사 hello 이름 게시 설정 파일입니다.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

이제 knife.rb 파일에 다음 예제와 비슷한 toohello 표시 합니다.

![][6]

이 줄은 Knife hello cookbook 디렉터리 c:\chef\cookbooks, 아래에서 참조 하 고 또한 쿼리하여 Azure 게시 설정 파일을 사용 하 여 Azure 작업 중에 확인 합니다.

## <a name="installing-hello-chef-development-kit"></a>Hello Chef 개발 키트를 설치합니다.
다음 [다운로드 및 설치](http://downloads.getchef.com/chef-dk/windows) Chef 워크스테이션을 ChefDK (Chef Development Kit) tooset hello 합니다.

![][7]

C:\opscode hello 기본 위치에 설치 합니다. 설치하는 데 10분 정도 걸립니다.

PATH 변수에 C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin에 대한 항목이 포함되어 있어야 합니다.

그렇지 않으면 이러한 경로를 추가해야 합니다.

*참고 hello 순서의 hello 경로 중요!* Opscode 경로 hello 올바른 순서에 없는 경우에 문제를 해야 합니다.

계속하기 전에 워크스테이션을 다시 부팅하세요.

다음으로 hello Knife Azure 확장을 설치 하겠습니다. "Azure 플러그 인" Knife hello로 제공합니다.

Hello 다음 명령을 실행 합니다.

    chef gem install knife-azure ––pre

> [!NOTE]
> hello – pre 인수 hello 최신 RC 버전의 hello 액세스 toohello 최신 Api 집합을 제공 하는 Knife Azure 플러그 인을 받는지 확인 합니다.
> 
> 

한 많은 종속성도 hello에 설치 될 가능성이 동시 합니다.

![][8]

tooensure 모든 항목은 다음 명령이 실행된 hello 올바르게 구성 합니다.

    knife azure image list

모든 것이 올바르게 구성되었으면 사용 가능한 Azure 이미지 목록이 표시됩니다.

축하합니다. hello 워크스테이션 설정 되었습니다!

## <a name="creating-a-cookbook"></a>Cookbook 만들기
Cookbook Chef toodefine에서 사용 하는 관리 되는 클라이언트에서 tooexecute 한다고 명령 집합이 있습니다. Cookbook을 만드는 것은 간단 하 고 사용 하 여 hello **cookbook을 생성 하는 chef** toogenerate 우리의 Cookbook 서식 파일을 명령입니다. 저는 IIS를 자동으로 배포하는 정책을 좋아하므로 저의 Cookbook 웹 서버를 호출해 보겠습니다.

C:\Chef 디렉터리 hello 다음 명령을 실행 합니다.

    chef generate cookbook webserver

이 hello 디렉터리 C:\Chef\cookbooks\webserver 파일 집합이 생성 됩니다. 이제 우리 Chef 클라이언트 tooexecute 관리 되는 가상 컴퓨터에 같은 명령의 toodefine hello 집합이 필요 합니다.

hello 명령은 hello 파일 default.rb에 저장 됩니다. 이 파일에 I 합니다 정의할 명령 집합을 시작 하 여 IIS를 설치, IIS 템플릿 파일 toohello wwwroot 폴더를 복사 합니다.

Hello C:\chef\cookbooks\webserver\recipes\default.rb 파일을 수정 하 고 hello 다음 줄을 추가 합니다.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

완료 되 면 hello 파일을 저장 합니다.

## <a name="creating-a-template"></a>템플릿 만들기
이전에 설명한 것 처럼 toogenerate 가격 default.html 페이지도 사용 되는 템플릿 파일 필요 합니다.

다음 명령 toogenerate hello 템플릿이 hello를 실행 합니다.

    chef generate template webserver Default.htm

이제 toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb 파일을 이동 합니다. 몇 가지 간단한 "Hello World" HTML 코드를 추가 하 여 hello 파일을 편집 하 고 hello 파일을 저장 합니다.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Chef 서버 hello Cookbook toohello 업로드
이 단계에서는 로컬 컴퓨터에 만든 Cookbook hello의 복사본을 사용 하 고 toohello Chef 호스팅 서버를 업로드 합니다. Hello Cookbook hello 아래에 표시 됩니다, 업로드 한 후 **정책** 탭 합니다.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Knife Azure를 사용하여 가상 컴퓨터 배포
이제 Azure 가상 컴퓨터를 배포 하 고 hello 품질 IIS 웹 서비스와 기본 웹 페이지를 설치 하는 "웹 서버" Cookbook을 적용 합니다.

이 toodo 주문 하 hello를 사용 하 여 **knife azure 서버 만들기** 명령입니다.

독자 hello 명령의 한 예로 다음 나타납니다.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

hello 매개 변수는 자체 설명 합니다. 특정 변수를 대체하고 실행합니다.

> [!NOTE]
> Hello hello 명령줄을 통해 hello – tcp 끝점 매개 변수를 사용 하 여 끝점 네트워크 필터 규칙을 자동화 I. 포트 80 및 3389 tooprovide 액세스 toomy 웹 페이지 및 RDP 세션을 연 했습니다.
> 
> 

Hello 명령을 실행 하면 되 면 이동 toohello Azure 포털을 시작 tooprovision 컴퓨터에 표시 됩니다.

![][13]

다음 hello 명령 프롬프트가 표시 됩니다.

![][10]

Hello 배포 완료 되 면 우리 있어야 수 tooconnect toohello 웹 서비스 포트 80 통해 म म hello hello Knife Azure 명령 사용 하는 가상 컴퓨터를 프로비저닝할 때 hello 포트 연 합니다. 이 가상 컴퓨터 클라우드 서비스 내에 가상 컴퓨터 hello 그대로 hello 클라우드 서비스 url과 연결 하겠습니다.

![][11]

보시는 바와 같이 HTML 코드를 독창적으로 수정했습니다.

반드시 hello 포트 3389 통해 Azure 포털에서에서 RDP 세션을 통해 연결할 수 있습니다.

유익한 정보가 되셨기 바랍니다. 이제 Azure의 Infrastructure as Code 과정을 시작해 보세요.

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
