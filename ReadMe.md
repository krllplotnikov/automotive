# Проект "Менеджер батареи"
## Оглавление
1. [Описание](#Описание)
2. [Структура менеджера батареи](#Структура-менеджера-батареи)
3. [Функции менеджера батареи](#Функции-менеджера-батареи)
4. [Результаты работы](#Результаты-работы)
____
## Описание
Менеджер батареи позволяет контролировать состояние роботы батареи, выполнять безопасную зарядку и разрядку. Имеется защита от переразряда батареи.

Работа менеджера происходит бесконечном цикле.
При помощи консоли имитируются различные действия с батареей, например подключение зарядного устройства. Также через консоль можно получать информацию о состоянии батареи и различных ее параметрах.
____
## Структура менеджера батареи
Структура менеджера батареи состоит из таких полей:
```C
typedef struct 
{
    double capacity;
    double nominalVoltage;
    double minVoltage;
    double maxVoltage;
    double currentVoltage;
    double maxOutputCurrent;

    double chargingVoltage;
    double maxChargingCurrent;

    uint8_t isChargerConnected;
    uint8_t isLoadConnected;
} BatteryManager;
```
*capacity* - номинальная емкость батареи.

*nominalVoltage* - номинальное напряжение батареи.

*minVoltage* - минимальное допустимое напряжение батареи.

*maxVoltage* - максимально допустимое напряжение батареи.

*currentVoltage* - текущее напрежение батареи.

*maxOutputCurrent* - максимальный выходной ток батареи.

*chargingVoltage* - номинальное напряжение зарядки.

*maxChargingCurrent* - максимальный ток зарядки.

*isChargerConnected* - флаг подключения зарядноко устройства.

*isLoadConnected* - флаг подключения нагрузки.
___
## Функции менеджера батареи
```C
double getBatteryVoltage(BatteryManager* batteryManager);
double getBatteryCapacity(BatteryManager* batteryManager);
double getStateOfCharge(BatteryManager* batteryManager);

uint8_t connectCharger(BatteryManager* batteryManager, double voltage, double current);
void disconnectCharger(BatteryManager* batteryManager);
uint8_t chargeBattery(BatteryManager* batteryManager, double voltage, double current);

uint8_t connectLoad(BatteryManager* batteryManager, double voltage, double current);
void disconnectLoad(BatteryManager* batteryManager);
uint8_t unchargeBattery(BatteryManager* batteryManager, double voltage, double current);
```
*getBatteryVoltage()* - получение текущего напряжения батареи.

*getBatteryCapacity()* - получение номинальной емкости батареи.

*getStateOfCharge()* - получение уровня заряда батареи в процентах.

*connectCharger()* - подключение зарядного устройства.
 - При подключении зарядного устройства проверяется напряжение и максимальный ток зарядки. Если параметры устройства не соответствуют допустимым, то зарядное устройство не подключится.

*disconnectCharger()* - отключение зарядного устройства

*chargeBattery()* - зарядка батареи.
 - Во время зарядки проверяется напряжение и ток зарядки. Если параметры не соответствуют допустимым, то зарядка прекратится и зарядное устройство отключится. При низком заряде батареи она заряжается маленьким током. Когда батарея зарядится полностью зарядное устройство отключится.

*connectLoad()* - подключение нагрузки к батарее.
 - При подключении нагрузки проверяется напряжение и максимальное потребление. Если параметры нагрузки не соответствуют допустимым, то нагрузки не подключится.

*disconnectLoad()* - отключение нагрузки от батареи.

*unchargeBattery()* - разрядка батареи.
 - Во время разряда батареи проверяется напряжение и ток разряда. Если параметры не соответствуют допустимым, то нагрузка отключится. При низком заряде батареи нагрузка автоматически отключится.
___
## Результаты работы
### Подключение зарядного устройства
<img src="./raw/conn_ch.png"/>

### Подключение нагрузки
<img src="./raw/conn_load.png"/>

### Некорректное напряжение зарядки
<img src="./raw/inc_ch_volt.png"/>

### Вывод всей информации о батарее
<img src="./raw/all_info.png"/>

____
