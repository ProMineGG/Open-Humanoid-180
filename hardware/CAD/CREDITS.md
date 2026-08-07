# Источники 3D-моделей

Этот файл содержит информацию об авторстве всех 3D-моделей, используемых в проекте Open-Humanoid-180.

---

## Самостоятельно созданные модели (автор: Open-Humanoid-180)

Эти модели созданы автором проекта с нуля по даташитам и технической документации.  
Они распространяются под лицензией [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

| Модель | Файл в репозитории | Примечания |
| :--- | :--- | :--- |
| LiFePO₄ 60145 50Ah (ячейка) | `power/lifepo4_60145.stp` | Создано в CATIA V5 по спецификации производителя. |
| MT6826S (магнитный энкодер) | `sensors/mt6826s.stp` | Модель QFN-корпуса 14-разрядного энкодера по даташиту. |

---

## Модели с GrabCAD / GitHub / других сайтов

Эти модели взяты с открытых сайтов в формате STEP/STP.

| Модель                             | Файл в репозитории                            | Автор                                                                       | Источник                                                                                                                                         |
| :--------------------------------- | :-------------------------------------------- | :-------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| BLDC 6384 120KV                    | `motors/6384-120KV.step`                      | [LeoDJ](https://grabcad.com/leodj-1)                                        | [GrabCAD](https://grabcad.com/library/6384-brushless-motor-1)                                                                                    |
| BLDC 5065 140KV                    | `motors/5065-140KV.step`                      | [Alex Mordue](https://grabcad.com/alex.mordue-1)                            | [GrabCAD](https://grabcad.com/library/cheap-5065-brushless-motor-1)                                                                              |
| BLDC 3205 110KV                    | `motors/3205-110KV.step`                      | [Robin Fröjd](https://grabcad.com/robin.frojd-1)                            | [GrabCAD](https://grabcad.com/library/pm2805-gimbal-bldc-1)                                                                                      |
| BMI160 (6‑осевой IMU)              | `sensors/bmi160.step`                         | [Kai Compton](https://grabcad.com/kai.compton-2)                            | [GrabCAD](https://grabcad.com/library/bmi160-imu-1)                                                                                              |
| QMC5883L (магнитометр)             | `sensors/qmc5883l.step`                       | [Benas Griauzde](https://grabcad.com/benas.griauzde-1)                      | [GrabCAD](https://grabcad.com/library/gy-271-hmc5883l-triple-3-axis-digital-compass-magnetometer-sensor-module-1)                                |
| FSR402 (датчик давления)           | `sensors/fsr402.step`                         | [M. Adel Ibrahim](https://grabcad.com/m.adel.ibrahim-1)                     | [GrabCAD](https://grabcad.com/library/fsr402-1)                                                                                                  |
| HX711 (АЦП для тензодатчиков)      | `sensors/hx711.STEP`                          | [AD Hietkamp](https://grabcad.com/ad.hietkamp-1)                            | [GrabCAD](https://grabcad.com/library/hx711-loadcell-amplifier-1)                                                                                |
| Керамический конденсатор 104       | `sensors/ceramic_capacitor_104.step`          | [TheElectronicsArchive](https://grabcad.com/theelectronicsarchive-1)        | [GrabCAD](https://grabcad.com/library/ceramic-capacitor-104-1)                                                                                   |
| ODrive 3.6 (драйвер)               | `drivers/odrive3.6.stp`                       | [tezeuz](https://grabcad.com/tezeuz-1)                                      | [GrabCAD](https://grabcad.com/library/motor-driver-odrive-v3-6-1)                                                                                |
| SimpleFOCMini (драйвер MS8313)     | `drivers/simplefocmini.step`                  | [askuric](https://github.com/askuric)                                       | [GitHub](https://github.com/simplefoc/SimpleFOCMini/tree/main)                                                                                   |
| ESP32-S3 N16R8                     | `mcu/esp32-s3.step`                           | [David Scambell](https://grabcad.com/david.scambell-1)                      | [GrabCAD](https://grabcad.com/library/yd-esp32-s3-1)                                                                                             |
| ESP32-S3 GPIO Shield               | `mcu/esp32-s3-shield.STEP`                    | [Serj Minin](https://grabcad.com/serj.minin-1)                              | [GrabCAD](https://grabcad.com/library/esp32-s3-44-v2-1)                                                                                          |
| CD74HC4067 (мультиплексор)         | `mcu/cd74hc4067.stp`                          | [Umberto Arena](https://grabcad.com/umberto.arena-3)                        | [GrabCAD](https://grabcad.com/library/mux-16-channels-1)                                                                                         |
| TJA1050 (CAN-трансивер)            | `mcu/tja1050.STEP`                            | [Luiz Fernando Martinelli](https://grabcad.com/luiz.fernando.martinelli-1)  | [GrabCAD](https://grabcad.com/library/tja1050-module-1)                                                                                          |
| TXS0108E (преобразователь уровней) | `mcu/txs0108e.step`                           | [Tim Treis](https://grabcad.com/tim.treis-1)                                | [GrabCAD](https://grabcad.com/library/txs0108e-logic-level-converter-8-channel-for-arduino-and-raspberry-pi-1)                                   |
| JK Smart BMS B1A8S20P              | `power/jk_bms_b1a8s20p.STEP`                  | [Дмитрий Левин](https://grabcad.com/07b2a22aae-1)                           | [GrabCAD](https://grabcad.com/library/bms-jikong-model-jk-b1a8s20p-1)                                                                            |
| LM25116 300W 20A Buck              | `power/buck_300w_lm25116.step`                | [Ferd kris](https://grabcad.com/ferd.kris-1)                                | [GrabCAD](https://grabcad.com/library/dc-dc-step-down-buck-converter-cc-cv-300w-20a-1)                                                           |
| SZ-BK6012 600W Buck                | `power/buck_600w_sz-bk6012.step`              | [Sam Sim](https://grabcad.com/sam.sim-4)                                    | [GrabCAD](https://grabcad.com/library/buck-converter-600w-dc12-75v-25a-1)                                                                        |
| Автоматический выключатель 200А    | `power/circuit_breaker_200a.STEP`             | [Andrey Kovalev](https://grabcad.com/andrey.kovalev-13)                     | [GrabCAD](https://grabcad.com/library/circuit-breaker-s202-c32-abb-2)                                                                            |
| Хаб предохранителей (12 гнёзд)     | `power/fuse_holder_12slot.step`               | [Refael Cohen](https://grabcad.com/refael.cohen-1)                          | [GrabCAD](https://grabcad.com/library/12-way-blade-fuse-holder-1)                                                                                |
| Предохранитель ATO (стандарт)      | `power/ato_fuse_standard.stp`                 | [SG](https://grabcad.com/sg)                                                | [GrabCAD](https://grabcad.com/library/fuse-ato-atc-5-amp-1)                                                                                      |
| Распределительный блок 160А        | `distribution/dbl160_distribution_block.step` | [Edson Leão](https://www.3dcontentcentral.com/Contributors.aspx?id=1025350) | [3D ContentCentral](https://www.3dcontentcentral.com/download-model.aspx?catalogid=171&id=1353218&partnumber=DBL160) *(Free for Commercial Use)* |
| XT30 (пара)                        | `connectors/xt30/`                            | [stuplja](https://grabcad.com/stuplja-1)                                    | [GrabCAD](https://grabcad.com/library/xt30-female-connector-1)<br>[GrabCAD](https://grabcad.com/library/xt30-male-connector-1)                   |
| XT60 (пара)                        | `connectors/xt60/`                            | [Ahmet Berkay Yılmaz](https://grabcad.com/ahmet.berkay.yilmaz-1)            | [GrabCAD](https://grabcad.com/library/xt60-female-1)<br>[GrabCAD](https://grabcad.com/library/xt60-male-2)                                       |
| XT60H (пара)                       | `connectors/xt60h/`                           | [Nelson Stoldt](https://grabcad.com/nelson.stoldt-1)                        | [GrabCAD](https://grabcad.com/library/power-connectors-male-female-xt60h-mr60-mt60-1)                                                            |
| XT90 (пара)                        | `connectors/xt90/`                            | [Dennis Mazur](https://grabcad.com/dennis.mazur-1)                          | [GrabCAD](https://grabcad.com/library/xt90pb-m-f-1)                                                                                              |

---

## Лицензия

- **Модели автора проекта** (LiFePO₄ и MT6826S) распространяются под лицензией [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
- **Модели с GrabCAD / 3D ContentCentral** принадлежат их авторам и используются в проекте с указанием авторства (модель распределительного блока имеет пометку *Free for Commercial Use*).
- **CAD-сборки** (ассембли), созданные на основе этих моделей, распространяются под лицензией [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) только в части, касающейся новой работы (компоновки и интеграции), при условии сохранения ссылок на оригинальных авторов.

---

*Если вы автор какой-либо модели и хотите изменить способ указания авторства или удалить модель из репозитория — напишите в Issues.*