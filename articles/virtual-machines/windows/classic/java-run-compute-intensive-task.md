---
title: "VM에서 Java 응용 프로그램 aaaCompute를 많이 사용 | Microsoft Docs"
description: "다른 Java 응용 프로그램에서 계산 집약적인 Java 응용 프로그램을 실행 하는 Azure 가상 컴퓨터 toocreate 수 모니터링 하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Toorun 계산 집약적인 java에서 가상 컴퓨터에서 작업 하는 방법
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

Azure 가상 컴퓨터 toohandle 계산 집약적인 작업을 사용할 수 있습니다. 예를 들어 가상 컴퓨터 작업을 처리 하 고 결과 tooclient 컴퓨터 또는 모바일 응용 프로그램 배달 수입니다. 이 문서를 읽은 후 다른 Java 응용 프로그램에서 계산 집약적인 Java 응용 프로그램을 실행 하는 가상 컴퓨터 toocreate 수 모니터링 하는 방법을 이해를 해야 합니다.

이 자습서에서는 toocreate Java 콘솔 응용 프로그램 라이브러리 tooyour Java 응용 프로그램을 가져올 수 및 Java 보관 파일 (JAR)를 생성할 수 있습니다 어떻게 알고 가정 합니다. Microsoft Azure에 대한 지식은 없는 것으로 가정합니다.

다음 내용을 배웁니다.

* 어떻게 toocreate Java 개발 키트 (JDK)와 가상 컴퓨터를 이미 설치 되었습니다.
* 어떻게 tooremotely tooyour 가상 컴퓨터에 로그인 합니다.
* 어떻게 toocreate 서비스 버스 네임 스페이스입니다.
* 어떻게 toocreate 계산 집약적인 작업을 수행 하는 Java 응용 프로그램입니다.
* 어떻게 toocreate 모니터링 하는 Java 응용 프로그램 hello hello 계산 집약적인 작업의 진행 상황입니다.
* 어떻게 toorun hello Java 응용 프로그램입니다.
* 어떻게 toostop hello Java 응용 프로그램입니다.

이 자습서는 hello 계산 집약적인 작업에 대 한 hello 외판원 문제를 사용 합니다. hello 다음은 hello Java 응용 프로그램 실행 중인 hello 계산 집약적인 작업의 예입니다.

![순회 외판원 문제 해 찾기][solver_output]

hello 다음은 hello Java 응용 프로그램 모니터링 hello 계산 집약적인 작업의 예입니다.

![순회 외판원 문제 클라이언트][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate 가상 컴퓨터
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. **새로 만들기**를 클릭하고 **계산**, **가상 컴퓨터**, **갤러리에서**를 차례로 클릭합니다.
3. Hello에 **가상 컴퓨터 이미지 선택** 대화 상자에서 **JDK 7 Windows Server 2012**합니다.
   **JDK 6 Windows Server 2012** 는 아직 JDK 7에서 준비 toorun 없는 레거시 응용 프로그램이 있는 경우.
4. **다음**을 누릅니다.
5. Hello에 **가상 컴퓨터 구성** 대화 상자:
   1. Hello 가상 컴퓨터에 대 한 이름을 지정 합니다.
   2. Hello 크기 toouse hello 가상 컴퓨터를 지정 합니다.
   3. Hello에 hello 관리자에 대 한 이름을 입력 **사용자 이름** 필드입니다. 이 암호 이름 및 hello 옆에 입력 하면, toohello 가상 컴퓨터에 원격으로 로그인 할 때 사용 합니다.
   4. Hello에 암호를 입력 **새 암호** 필드를 다시 hello에 입력 **확인** 필드입니다. 이것이 hello 관리자 계정 암호입니다.
   5. **다음**을 누릅니다.
6. Hello에 다음 **가상 컴퓨터 구성** 대화 상자:
   1. 에 대 한 **클라우드 서비스**, hello 기본값을 사용 하 여 **새 클라우드 서비스를 만들**합니다.
   2. 값에 대 한 hello **클라우드 서비스 DNS 이름** cloudapp.net에서 고유 해야 합니다. 필요한 경우 Azure에서 고유한 이름이 되도록 수정합니다.
   3. 지역, 선호도 그룹 또는 가상 네트워크를 지정합니다. 이 자습서에서는 지역(예: **미국 서부**)을 지정합니다.
   4. **저장소 계정** 상자에서 **자동으로 생성된 저장소 계정 사용**을 선택합니다.
   5. **가용성 집합**에서 **(없음)**을 선택합니다.
   6. **다음**을 누릅니다.
7. 최종 hello에 **가상 컴퓨터 구성** 대화 상자:
   1. Hello 기본 끝점 항목을 수락 합니다.
   2. 페이지 맨 아래에 있는 **완료**을 참조하세요.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>tooremotely 로그인 tooyour 가상 컴퓨터
1. Toohello 로그온 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. **가상 컴퓨터**를 클릭합니다.
3. Hello 하려는 toolog에 hello 가상 컴퓨터 이름을 클릭 합니다.
4. **Connect**를 클릭합니다.
5. 필요한 tooconnect toohello 가상 컴퓨터로 toohello 표시 되는 메시지에 응답 합니다. Hello 관리자 이름 및 암호에 대 한 메시지가 표시 되 면 hello 가상 컴퓨터를 만들 때 제공한 hello 값을 사용 합니다.

해당 hello Azure 서비스 버스 기능 hello Baltimore CyberTrust 루트 인증서 toobe JRE의의 일부로 설치 해야 **cacerts** 저장 합니다. 이 인증서가 자동으로 환경 JRE (Java Runtime)이이 자습서에서 사용 하는 hello에 포함 됩니다. 경우 않아도이 인증서에 프로그램 JRE **cacerts** 저장소를 참조 하십시오 [Java CA 인증서 저장소 인증서 toohello 추가] [ add_ca_cert] 추가에 대 한 내용은 (으로 에 대 한 정보, cacerts 저장소에 hello 인증서 보기)

## <a name="how-toocreate-a-service-bus-namespace"></a>어떻게 toocreate 서비스 버스 네임 스페이스
Azure에서 서비스 버스를 사용 하 여 toobegin 큐, 서비스 네임 스페이스를 먼저 만들어야 합니다. 서비스 네임스페이스는 응용 프로그램 내에서 서비스 버스 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.

서비스 네임 스페이스 toocreate:

1. Toohello 로그온 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello hello Azure 클래식 포털의 왼쪽 아래 탐색 창에서 **서비스 버스, 액세스 제어 및 Caching**합니다.
3. Hello hello Azure 클래식 포털의 왼쪽 창에서 클릭 hello **서비스 버스** 노드를 hello를 클릭 한 다음 **새로** 단추입니다.  
   ![서비스 버스 노드 스크린샷][svc_bus_node]
4. Hello에 **새 서비스 Namespace를 만들** 대화 상자에 입력 한 **Namespace**, toomake를 고유한 지 클릭 하 고는 **가용성 확인** 단추 합니다.  
   ![새 네임스페이스 만들기 스크린샷][create_namespace]
5. 된 hello 네임 스페이스 이름을 사용할 수 있는지 확인 한 후, 국가 또는 지역 하면 네임 스페이스를 호스팅해야 및 hello를 클릭 한 다음 선택 **만들 Namespace** 단추입니다.  
   
   hello 네임 스페이스를 만든 후 hello Azure 클래식 포털에에서 나타납니다 걸리고 순간 tooactivate 합니다. Hello 상태가 될 때까지 기다립니다 **활성** hello 다음 단계를 계속 합니다.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Hello 기본 관리 자격 증명을 가져올 hello 네임 스페이스에 대 한
Hello 새 네임 스페이스에 큐를 만들 때 처럼 순서 tooperform 관리 작업에는 네임 스페이스에 대 한 tooobtain hello 관리 자격 증명이 필요 합니다.

1. Hello 왼쪽된 탐색 창에서 클릭 hello **서비스 버스** 노드를 사용 가능한 네임 스페이스는 hello 목록을 표시 합니다.
   ![사용 가능한 네임스페이스 스크린샷][avail_namespaces]
2. 표시 된 hello 목록에서 방금 만든 hello 네임 스페이스를 선택 합니다.
   ![네임스페이스 목록 스크린샷][namespace_list]
3. 오른쪽 hello **속성** 창 새 네임 스페이스에 대 한 hello 속성을 나열 합니다.
   ![속성 창 스크린샷][properties_pane]
4. hello **기본 키** 숨겨집니다. Hello 클릭 **보기** toodisplay hello에 대 한 보안 자격 증명을 단추입니다.
   ![기본 키 스크린샷][default_key]
5. Hello 메모 **기본 발급자** 및 hello **기본 키** tooperform 작업 아래에이 정보를 사용 하 여 네임 스페이스와 됩니다.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>어떻게 toocreate 계산 집약적인 작업을 수행 하는 Java 응용 프로그램
1. 개발 컴퓨터에서 (없는 만든 toobe hello 가상 컴퓨터)을 다운로드 hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/)합니다.
2. 이 섹션의 hello 끝에 hello 예제 코드를 사용 하 여 Java 콘솔 응용 프로그램을 만듭니다. 이 자습서에서는 **TSPSolver.java** hello Java 파일 이름입니다. Hello 수정 **프로그램\_서비스\_버스\_네임 스페이스**, **프로그램\_서비스\_버스\_소유자**, 및 **프로그램\_서비스\_버스\_키** 자리 표시자 toouse 서비스 버스 **네임 스페이스**, **기본 발급자** 및  **기본 키** 값을 각각.
3. 후 코딩, 내보내기 hello 응용 프로그램 tooa runnable Java 보관 파일 (JAR) 및 패키지 hello 필요 hello에 라이브러리 JAR을 생성 합니다. 이 자습서에서는 **TSPSolver.jar** 생성 hello JAR 이름으로 합니다.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>어떻게 toocreate 모니터링 하는 Java 응용 프로그램 hello hello 계산 집약적인 작업의 진행 상황
1. 개발 컴퓨터에서이 섹션의 hello 끝에 hello 예제 코드를 사용 하 여 Java 콘솔 응용 프로그램을 만듭니다. 이 자습서에서는 **TSPClient.java** hello Java 파일 이름입니다. 에서 설명한 것 처럼 수정 hello **프로그램\_서비스\_버스\_네임 스페이스**, **프로그램\_서비스\_버스\_소유자**, 및 **프로그램\_서비스\_버스\_키** 자리 표시자 toouse 서비스 버스 **네임 스페이스**, **기본 발급자**및 **기본 키** 값을 각각.
2. Hello 응용 프로그램 tooa 내보내기 실행 가능한 JAR 및 패키지 hello hello에 라이브러리 생성 JAR 필요 합니다. 이 자습서에서는 **TSPClient.jar** 생성 hello JAR 이름으로 합니다.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>어떻게 toorun hello Java 응용 프로그램
첫 번째 toocreate hello 큐 다음 toosolve hello 현재 최상의 경로 toohello 서비스 버스 큐를 추가 하는 여행 Saleseman 문제 hello hello 계산 집약적인 응용 프로그램을 실행 합니다. Hello 하는 동안 계산 집약적인 응용 프로그램은 실행 (또는 나중에) hello 서비스 버스 큐에서 실행된 hello 클라이언트 toodisplay 결과.

### <a name="toorun-hello-compute-intensive-application"></a>toorun hello 계산 집약적인 응용 프로그램
1. Tooyour 가상 컴퓨터에 로그온 합니다.
2. 응용 프로그램을 실행할 폴더(예: **c:\TSP**를 만듭니다.
3. 복사 **TSPSolver.jar** 너무**c:\TSP**,
4. 라는 파일을 만들어 **c:\TSP\cities.txt** 내용을 따라 hello로 합니다.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. 명령 프롬프트에서 디렉터리 tooc:\TSP를 변경 합니다.
6. Hello JRE bin 폴더는 hello PATH 환경 변수를 확인 합니다.
7. Hello TSP solver 순열을 실행 하기 전에 toocreate hello 서비스 버스 큐를 필요 합니다. 다음 명령 toocreate hello 서비스 버스 큐 hello를 실행 합니다.
   
        java -jar TSPSolver.jar createqueue
8. Hello 큐를 만든 했으므로 hello TSP solver 순열을 실행할 수 있습니다. 예를 들어 hello 명령 toorun hello solver 8 도시에 대 한 다음를 실행 합니다.
   
        java -jar TSPSolver.jar 8
   
   숫자를 지정하지 않으면 10개 도시에 대해 실행됩니다. Hello solver 현재 가장 짧은 경로 발견 하는 대로 추가 됩니다에 toohello 큐.

> [!NOTE]
> 더 큰 hello hello 번호 지정 하는, 긴 hello solver hello 실행 됩니다. 예를 들어 14개 도시에 대해 실행하면 몇 분이 걸릴 수 있고, 15개 도시에 대해 실행하면 몇 시간이 소요될 수 있습니다. 런타임 (최종적 몇 주, 월 및 연도) 일 too16 또는 도시를 더 증가 될 수 있습니다. Toohello 급증 hello 수 도시 증가로 해 hello 찾기 평가 순열의 hello 수 때문입니다.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>어떻게 toorun hello 모니터링 클라이언트 응용 프로그램
1. Hello 클라이언트 응용 프로그램을 실행할 tooyour 컴퓨터에 로그온 합니다. 필요 하지 않습니다 toobe hello hello를 실행 하는 동일한 컴퓨터 **TSPSolver** 울 수 있지만 응용 프로그램입니다.
2. 응용 프로그램을 실행할 폴더(예: **c:\TSP**를 만듭니다.
3. 복사 **TSPClient.jar** 너무**c:\TSP**,
4. Hello JRE bin 폴더는 hello PATH 환경 변수를 확인 합니다.
5. 명령 프롬프트에서 디렉터리 tooc:\TSP를 변경 합니다.
6. Hello 다음 명령을 실행 합니다.
   
        java -jar TSPClient.jar
   
    필요에 따라 명령줄 인수를 전달 하 여 hello 큐를 확인 하는 중 사이의 분 toosleep hello 수를 지정 합니다. hello hello 큐를 확인 하기 위한 기본 절전 모드 시간은 3 분, 명령줄 인수를 전달 하지 너무 경우 사용 되는**TSPClient**합니다. 예를 들어 hello 대기 간격에 대 한 원하는 toouse 다른 값을 1 분 hello 다음 명령을 실행 합니다.
   
        java -jar TSPClient.jar 1
   
    클라이언트 hello "완료"의 큐 메시지를 발견할 때까지 실행 됩니다. 참고 hello 클라이언트를 실행 하지 않고 hello solver 여러 번을 실행 하면 toorun hello 클라이언트 여러 번 toocompletely 빈 hello 큐를 할 수 있습니다. 또는 hello 큐를 삭제 한 후 다시 만들 수 있습니다. hello 다음 실행 toodelete hello 큐 **TSPSolver** (하지 **TSPClient**) 명령입니다.
   
        java -jar TSPSolver.jar deletequeue
   
    hello solver 모든 경로 검사를 완료 될 때까지 실행 됩니다.

## <a name="how-toostop-hello-java-applications"></a>어떻게 toostop hello Java 응용 프로그램
Hello solver와 클라이언트 응용 프로그램에 대 한 누르면 **Ctrl + C** tooexit tooend 이전 toonormal 완료 하려는 경우.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
