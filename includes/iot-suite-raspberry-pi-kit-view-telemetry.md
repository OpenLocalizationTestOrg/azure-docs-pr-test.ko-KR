## <a name="view-hello-telemetry"></a>Hello 원격 분석 보기

이제 hello 라스베리 Pi 원격 분석 toohello 원격 모니터링 솔루션을 보내는 중입니다. Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다. Hello 솔루션 대시보드에서 메시지 tooyour 라스베리 Pi를 보낼 수도 있습니다.

- Toohello 솔루션 대시보드를 탐색 합니다.
- Hello에 장치를 선택 합니다. **장치 tooView** 드롭다운입니다.
- hello에서 hello 원격 분석 라스베리 Pi hello 대시보드에 표시 됩니다.

![Hello 라스베리 Pi에서에서 원격 분석 표시][img-telemetry-display]

## <a name="act-on-hello-device"></a>Hello 장치에서 작동 합니다.

Hello 솔루션 대시보드에서 라스베리 원주율 메서드를 호출할 수 있습니다. Hello 라스베리 Pi toohello 원격 모니터링 솔루션에 연결 되 면 지원 hello 방법에 대 한 정보를 보냅니다.

- Hello 솔루션 대시보드 클릭 **장치** toovisit hello **장치** 페이지. Hello에 라스베리 Pi 선택 **장치 목록**합니다. 그런 다음 **메서드**를 선택합니다.

    ![대시보드에서 장치 나열][img-list-devices]

- Hello에 **메서드 호출** 페이지에서 선택 **LightBlink** hello에 **메서드** 드롭다운입니다.

- **InvokeMethod**를 선택합니다. hello LED 연결 toohello 라스베리 Pi 여러 번 깜박입니다. hello 응용 프로그램에 액세스 hello 라스베리 Pi 승인 백 toohello 솔루션 대시보드를 보냅니다.

    ![메서드 기록 표시][img-method-history]

- 전환할 수 있습니다 hello LED 켜고 hello를 사용 하 여 **ChangeLightStatus** 메서드는 **LightStatusValue** 도**1** 에 대 한에 또는 **0** 에 대 한 해제 합니다.

> [!WARNING]
> Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다. 사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md