---
title: "Linux 기반 HDInsight-Azure의 Hadoop MapReduce.NET aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 toouse.NET 응용 프로그램에서 Linux 기반 HDInsight는 MapReduce 스트리밍에 대 한 합니다."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Windows 기반 HDInsight에 대 한.NET 솔루션을 마이그레이션하려면 HDInsight tooLinux 기반

Linux 기반 HDInsight 클러스터 사용 [모노 (https://mono-project.com)](https://mono-project.com) toorun.NET 응용 프로그램입니다. 모노는 toouse.NET 구성 요소를와 Linux 기반 HDInsight MapReduce 응용 프로그램과 같은 있습니다. 이 문서에서는 Linux 기반 HDInsight의 모노와 Windows 기반 HDInsight 클러스터 toowork에 대 한 toomigrate.NET 솔루션을 생성 하는 방법에 대해 설명 합니다.

## <a name="mono-compatibility-with-net"></a>Mono와 .NET의 호환성

Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다. HDInsight에 포함 된 모노 길이의 hello에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다. tooinstall 모노의 특정 버전 참조 hello [설치 또는 업데이트 모노](hdinsight-hadoop-install-mono.md) 문서.

모노 및.NET 간의 호환성에 대 한 자세한 내용은 참조 hello [모노 호환성 (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) 문서.

> [!IMPORTANT]
> hello SCP.NET 프레임 워크는 모노 호환 됩니다. 모노 SCP.NET 사용에 대 한 자세한 내용은 참조 하십시오. [HDInsight의 Apache Storm의 Visual Studio를 사용 하 여 toodevelop C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.

## <a name="automated-portability-analysis"></a>자동 이식성 분석

hello [.NET 이식성 분석기](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) toogenerate 사용 되는 응용 프로그램 및 모노 간의 비 호환성 보고서를 수 있습니다. 모노 이식성에 대 한 hello 단계 tooconfigure hello 분석기 toocheck 다음 응용 프로그램을 사용 합니다.

1. Hello 설치 [.NET 이식성 분석기](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)합니다. 설치 하는 동안 Visual Studio toouse의 hello 버전을 선택 합니다.

2. Visual Studio 2015에서 선택 __분석__ > __Portability Analyzer 설정__, 있는지 확인 하 고 __4.5__ 체크 인 hello __모노__  섹션.

    ![4.5는 hello 분석기 설정에 대 한 모노 섹션에서 선택](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    선택 __확인__ toosave hello 구성 합니다.

3. __Analyze__ > __Analyze Assembly Portability__를 선택합니다. 솔루션에 포함 된 hello 어셈블리를 선택한 다음 선택 __열려__ toobegin 분석 합니다.

4. 분석이 완료되면 __Analyze__ > __View analysis reports__를 선택합니다. __이식성 분석 결과__선택, __보고서를 열고__ tooopen 보고서입니다.

    ![이식성 분석기 결과 대화 상자](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> hello 분석기 솔루션과 모든 문제를 catch 할 수 없습니다. 예를 들어의 파일 경로 `c:\temp\file.txt` 모노 Windows에서 실행 되 고 hello 경로가 해당 컨텍스트에서 유효 하기 때문에 정상으로 간주 됩니다. 그러나 hello 경로 Linux 플랫폼에 올바르지 않습니다.

## <a name="manual-portability-analysis"></a>수동 이식성 분석

Hello에 hello 정보를 사용 하 여 코드의 수동 감사 수행 [응용 프로그램 이식성 (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) 문서.

## <a name="modify-and-build"></a>수정 및 빌드

HDInsight에 대 한 Visual Studio toobuild toouse.NET 솔루션을 계속할 수 있습니다. 그러나 해당 hello 프로젝트는 구성 된 toouse.NET Framework 4.5 확인 해야 합니다.

## <a name="deploy-and-test"></a>배포 및 테스트

Hello 권장 사항을 hello.NET 이식성 분석기 또는 수동 분석에서 사용 하 여 솔루션을 수정 하면 HDInsight와 테스트 해야 합니다. Linux 기반 HDInsight 클러스터에서 hello 솔루션 테스트 toobe 수정 해야 하는 미묘한 문제를 나타낼 수 있습니다. 테스트하는 동안 응용 프로그램에서 추가 기록을 활성화하는 것이 좋습니다.

로그 액세스에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [Linux 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>다음 단계

* [HDInsight에서 MapReduce와 함께 C# 사용](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Hive 및 Pig과 함께 C# 사용자 정의 함수 사용](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [HDInsight에서 Storm용 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)