## <a name="view-device-telemetry-in-hello-dashboard"></a>Hello 대시보드에 장치 원격 분석 보기
hello 대시보드에서 hello 원격 tooview hello 원격 장치 보내기 tooIoT 허브 솔루션 사용을 모니터링 합니다.

1. 반환 toohello 원격 모니터링 솔루션 대시보드를 브라우저에서 클릭 **장치** hello 왼쪽 패널 toonavigate toohello에 **장치 목록**합니다.
2. Hello에 **장치 목록**, 장치의 hello 상태 인지 표시 되어야 **실행**합니다. 그렇지 않은 경우 클릭 **장치 사용** hello에 **장치 세부 정보** 패널입니다.
   
    ![장치 상태 보기][18]
3. 클릭 **대시보드** tooreturn toohello 대시보드 hello에 장치를 선택 합니다. **장치 tooView** 드롭 다운 tooview 해당 원격 분석 합니다. hello 샘플 응용 프로그램에서 hello 원격 분석 내부 온도 대 한 50 단위, 55 단위 외부 온도 및 습도에 50 명의 단위 됩니다.
   
    ![장치 원격 분석 보기][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>장치에서 메서드 호출
hello 원격 모니터링 솔루션에서 hello 대시보드 IoT 허브를 사용 하 여 장치의 tooinvoke 메서드가 있습니다. 예를 들어 hello 모니터링 솔루션 원격 장치를 다시 부팅 메서드 toosimulate를 호출할 수 있습니다.

1. Hello 원격 모니터링 솔루션 대시보드에 클릭 **장치** hello 왼쪽 패널 toonavigate toohello에 **장치 목록**합니다.
2. 클릭 **장치 ID** hello에 장치에 대 한 **장치 목록**합니다.
3. Hello에 **장치 세부 정보** 에서 **메서드**합니다.
   
    ![장치 메서드][13]
4. Hello에 **메서드** 드롭다운 목록에서 선택 **InitiateFirmwareUpdate**, 한 다음 **FWPACKAGEURI** 더미 URL을 입력 합니다. 클릭 **메서드 호출** hello 장치에서 toocall hello 메서드.
   
    ![장치 메서드 호출][14]
   

5. Hello 장치 hello 메서드를 처리할 때 장치 코드를 실행 하는 hello 콘솔에 메시지가 표시 됩니다. hello 메서드의 hello 결과 hello 솔루션 포털에서 toohello 기록을 추가 됩니다.

    ![메서드 기록 보기][img-method-history]

## <a name="next-steps"></a>다음 단계
hello 문서 [사용자 지정 솔루션을 미리 구성 된] [ lnk-customize] 이 샘플을 확장 하는 몇 가지 방법에 설명 합니다. 가능한 확장에는 실제 센서 사용 및 추가적인 명령 구현이 포함됩니다.

Hello에 대 한 자세히 알아볼 수 있습니다 [hello azureiotsuite.com 사이트에 대 한 권한을][lnk-permissions]합니다.

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
