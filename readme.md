Сначала собираем устройство по схеме
Я использовал плату wemos d1, но в принципе можно использовать любую на esp8266 с не менее 1024к памяти.
Качаем последнюю прошивку с https://github.com/letscontrolit/ESPEasy/releases
Ставим esptool и прошиваем контроллер, указав вместо COM3 устройство, на котором определился контроллер:
esptool.py --port COM3 --baud 115200 write_flash -fm dio -fs 32m 0x00000 ESPEasy_R120_4096.bin 
Перегружаем контроллер, подключаемся к сети ESP_Easy_0, пароль configesp, заходим на 192.168.4.1, настраиваем имя устройства и параметры подключения к WI-FI, перезагружаем, смотрим в роутере новый IP и снова заходим. 
На вкладке Devices создаем новое устройство, выставляем Device:	Switch input - Switch, Name: power, GPIO ⇄ : GPIO-14(D5).
На вкладке Tools нажимаем Advanced, отмечаем чекбокс напротив Rules. Заходим на вкладку Rules, вставляем туда содержимое файла rules1.txt, сохраняем. На вкладке Tools выбираем File browser, загружаем файлы pc.esp, pc0.png, pc1.png. 
В результате по адресу http://наш_ip/pc.esp будет доступен веб-интерфейс с кнопками, команды можно отдавать get-запросами:
http://наш_ip/control?cmd=event,poweron
http://наш_ip/control?cmd=event,poweroff
http://наш_ip/control?cmd=event,reboot
