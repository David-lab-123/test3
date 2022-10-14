 # Необычное решение
 Чтобы обеспечить достаточные ресурсы, Sony выделила для общего использования 2 МБ ОЗУ. Любопытно, что
 компания установила на материнскую плату чипы Extended Data Out (EDO). Они чуть более эффективнее
 обычной DRAM и обеспечивают меньшие задержки.
 
 ## Перехват управления у CPU
 
 В определённые моменты одной из подсистем (графика, звук или CD) могут с высокой частотой требоваться
 большие блоки данных. Однако CPU не всегда способен справиться с такими запросами.
 
 По этой причине контроллер CD-ROM, MDEC, GPU, SPU и параллельный порт при необходимости имеют доступ
 к DMA-контроллеру. DMA берёт на себя управление основной шиной и выполняет передачу данных. Получающаяся
 частота передачи намного выше, чем при использовании CPU, однако последний всё равно необходим для
 подготовки DMA-передачи.
 
 ### Не думай о секундах свысока
 Также стоит помнить о том, что при срабатывании DMA процессор не может получить доступа к основной шине.
 Это значит, что CPU будет простаивать, если только для него нет работы в Scratchpad!
 
 Дополнения к ядру
 =================
 
 Как и другие CPU на основе MIPS R3000, CW33000 поддерживает конфигурации с четырьмя сопроцессорами.
 Sony решила использовать три:
 
 
 ### System Control Coprocessor
 
 
 
 
 System Control Coprocessor (сопроцессор управления системой), обозначенный как CP0, является стандартным
 блоком CPU MIPS. В системах на основе R3000 сопроцессор CP0 управляет реализацией кэша.
 То есть он обеспечивает прямой доступ к кэшу данных (имеющему форму «Scratchpad») и к кэшу команд
 (при помощи «изоляции кэша»). Управляющий сопроцессор также отвечает за обработку прерываний,
 исключений и контрольных точек (последнее полезно при отладке).
 
 Постойте, но разве сопроцессоры не должны только расширять функции CPU? Почему CP0 так тесно связан с CPU?
