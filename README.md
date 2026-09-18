# ⚡ Релиз 4.26.39.1

## Внедрение системы мониторинга производительности 1С, накопление оповещений и оптимизация расписания регламентных заданий

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <b style="color: #1a73e8;">⚡Релиз 4.26.39.1</b> — новый общий модуль <b>«МониторингПроизводительности»</b>, 
                регламентное задание для автоматического сбора метрик журнала регистрации, 
                а также <b>оптимизация расписания регламентных заданий</b> для снижения нагрузки на сервер.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
               ✅  Метрики собираются <b>с начала текущего дня по конец дня</b> и фиксируются в журнале регистрации.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Результаты <b>дописываются в существующее оповещение</b> в регистре «Оповещения» — свежий отчёт сверху, история ниже.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Если записи в регистре нет — <b>новая не создаётся</b>: механизм работает только с уже заведёнными оповещениями.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Регламентные задания <b>разнесены по времени</b> — тяжёлые операции вынесены в нерабочие часы.
            </p>
        </td>
    </tr>
</table>

---

## 🎯 Основные цели релиза

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 16px 0; font-size: 14px;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Цель</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Описание</th>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Автоматический сбор метрик</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Ошибки, предупреждения и взаимоблокировки из журнала регистрации, состояние регламентных заданий</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Накопление истории</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Свежий отчёт всегда сверху, старые — ниже под разделителем</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Отсутствие «мусорных» записей</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Запись обновляется только если она уже существует — иначе мониторинг молча выходит</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Оптимизация расписания РЗ</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Разнос тяжёлых заданий по времени, отказ от избыточных запусков, снижение пиковой нагрузки</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Чистота архитектуры</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Отдельный общий модуль + регламентное задание вместо ручных проверок</td>
    </tr>
</table>

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <b style="color: #1a73e8;">##⚡ Общий модуль «МониторингПроизводительности»</b></p> 
                <b style="color: #1a73e8;">### Описание функционала </b></p>
                <b style="color: #1a73e8;">Мониторинг собирает ключевые метрики производительности за текущий день и обновляет существующие оповещения.</b>
                <b>**Как это работает:**</b></p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                1. 📅 <b>Период сбора</b> — с начала текущего дня (00:00:00) по конец текущего дня (23:59:59). </p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                2. 🔍 <b>Метрики из ЖР</b> — количество ошибок, предупреждений и взаимоблокировок за период.</p>
        <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                3. 📊 <b>Состояние РЗ</b> — подсчёт регламентных заданий, завершившихся с ошибкой.</p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                4. 📝 <b>Запись в ЖР</b> — полный текст отчёта фиксируется в журнале регистрации как информационное событие.</p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                5. 📨 <b>Обновление оповещения</b> — если запись в регистре «Оповещения» уже есть, текст дописывается в неё сверху.</p>
        </td>
    </tr>
</table>

---

## 🔄 Бизнес-процесс

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 16px 20px;"> <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;"> <span style="font-size: 20px;">🔄</span> <b style="color: #1a73e8;">Бизнес-процесс</b> — ежедневный автоматический сбор метрик и обновление единого оповещения для администратора, с сохранением истории. </p> </td> </tr> </table>

<table cellpadding="14" cellspacing="0" style="border-left: 5px solid #f5a623; background: #fff8f0; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 14px 18px;">
1. ⏰ Регламентное задание <b>«МониторингПроизводительности»</b> запускается по расписанию

2. 📅 Определяется период: <b>НачалоДня(ТекущаяДата())</b> — <b>КонецДня(ТекущаяДата())</b>

3. 🔍 Выполняется сбор метрик:

<table cellpadding="8" cellspacing="0" style="border-collapse: collapse; width: 100%; margin: 8px 0; border: none;"> <tr> <td style="padding: 6px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #e8f5e9; padding: 10px 14px; border-radius: 6px; border-left: 4px solid #2e7d32;"> <b>✅ Журнал регистрации</b><br> <span style="padding-left: 18px;">Ошибки</span><br> <span style="padding-left: 18px;">Предупреждения</span><br> <span style="padding-left: 18px;">Взаимоблокировки</span> </div> </td> <td style="padding: 6px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #e3f2fd; padding: 10px 14px; border-radius: 6px; border-left: 4px solid #1565c0;"> <b>📊 Регламентные задания</b><br> <span style="padding-left: 18px;">Количество с ошибкой</span><br> <span style="padding-left: 18px;">Перебор через метаданные</span> </div> </td> </tr> </table>

4. 📝 Формируется текст отчёта и пишется в ЖР

5. 📨 Обновляется запись в регистре «Оповещения»:
   - если записи нет — <b>ничего не создаётся</b>
   - если запись есть — <b>новый текст добавляется в начало</b>

</td> </tr> </table>

### Приоритет источников значения

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;"> <tr> <th style="background: #6a1b9a; color: white; padding: 10px;">🥇 Приоритет</th> <th style="background: #6a1b9a; color: white; padding: 10px;">📌 Источник</th> <th style="background: #6a1b9a; color: white; padding: 10px;">⚙️ Условие</th> </tr> <tr> <td style="padding: 10px; text-align: center;"><b>1</b></td> <td style="padding: 10px;">Журнал регистрации</td> <td style="padding: 10px;">События за текущий день по фильтру уровней</td> </tr> <tr> <td style="padding: 10px; text-align: center;"><b>2</b></td> <td style="padding: 10px;">Регламентные задания</td> <td style="padding: 10px;">Перебор всех заданий, состояние «ЗавершеноСОшибкой»</td> </tr> <tr> <td style="padding: 10px; text-align: center;"><b>3</b></td> <td style="padding: 10px;">Регистр «Оповещения»</td> <td style="padding: 10px;">Запись с таким же АдресБазы + Заголовок уже существует</td> </tr> </table>

---

## 📦 Накопление текста в оповещении

---

### 📌 Описание функционала

<div style="background: #f0f7ff; border-left: 5px solid #4a90d9; padding: 16px 20px; border-radius: 8px; margin: 12px 0;">

При каждом запуске мониторинга система выполняет **дополнение существующей записи**:

- 🔍 **Ищет** запись в регистре по АдресБазы + Заголовок
- 🛑 **Если записи нет** — выходит, ничего не создавая
- 📝 **Если запись есть** — добавляет новый текст в начало, сохраняя старый ниже под разделителем
- 🕒 **Шапка с датой** — каждая итерация отмечена датой запуска

</div>

---

### ⚙️ Механизм работы

#### 📄 При запуске регламентного задания

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #4a90d9; color: white; padding: 10px;">✅ Условие</th>
        <th style="background: #4a90d9; color: white; padding: 10px;">🔄 Действие</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Запись в регистре<br><b>НЕ найдена</b></td>
        <td style="padding: 10px;">⏭️ Выход из процедуры, запись не создаётся</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Запись в регистре<br><b>найдена</b></td>
        <td style="padding: 10px;">
            • 🕒 Формируется шапка с датой<br>
            • 📝 Новый текст добавляется в начало<br>
            • ➖ Старый текст остаётся ниже под разделителем<br>
            • 🔄 Обновляются реквизиты (ДатаОповещения, Версия, Получатели, ВРаботе)
        </td>
    </tr>
    <tr>
        <td style="padding: 10px;">Ошибка при обновлении</td>
        <td style="padding: 10px;">📝 Запись в журнал регистрации</td>
    </tr>
</table>

---

### 🛡️ Защита от лишних записей

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #2e7d32; color: white; padding: 10px;">✅ Проверка</th>
        <th style="background: #2e7d32; color: white; padding: 10px;">⏭️ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Наличие записи в регистре</td>
        <td style="padding: 10px;">⏭️ Новая запись не создаётся</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Сравнение Заголовка через ПОДСТРОКА(1, 150)</td>
        <td style="padding: 10px;">🛡️ Обход строк неограниченной длины</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Поиск без фильтра по ДатаОповещения</td>
        <td style="padding: 10px;">🛡️ Запись не «теряется» на следующий день</td>
    </tr>
</table>

---

### 📋 Использование

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #6a1b9a; color: white; padding: 10px;">🖐️ Способ</th>
        <th style="background: #6a1b9a; color: white; padding: 10px;">📌 Описание</th>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">⏰ <b>Регламентное задание</b></td>
        <td style="padding: 10px;">Метод <code>МониторингПроизводительности.ВыполнитьМониторинг</code>, расписание — ежедневно</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">🖐️ <b>Ручной запуск</b></td>
        <td style="padding: 10px;">Вызов процедуры из внешней обработки или консоли заданий</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">📨 <b>Получатель</b></td>
        <td style="padding: 10px;">Фиксированный адрес в реквизите «Получатели» — <code>artem240992@bk.ru</code></td>
    </tr>
</table>

---

### ⚙️ Технические особенности

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 12px 0;">

<div style="background: #e8f5e9; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #2e7d32;">
    ✅ Период сбора: с начала дня по конец дня
</div>

<div style="background: #e3f2fd; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #1565c0;">
    📊 Регистр «Оповещения» — обновление без создания
</div>

<div style="background: #fff3e0; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #f57c00;">
    🛠️ Обработка ошибок в журнале регистрации
</div>

<div style="background: #fce4ec; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #c62828;">
    🚫 Блокировка не используется — гонок нет
</div>

<div style="background: #f3e5f5; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #6a1b9a;">
    📝 Текст накапливается сверху вниз
</div>

<div style="background: #e0f7fa; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #00838f;">
    🔍 Сравнение заголовков через ПОДСТРОКА
</div>

</div>

---

### 📊 Схема работы

<div style="background: #f8fafc; border-radius: 12px; padding: 20px; border: 1px solid #e1e4e8; margin: 16px 0; font-family: 'Segoe UI', Arial, sans-serif;">

    <div style="text-align: center; font-size: 16px; font-weight: 600; color: #1a1a2e; margin-bottom: 12px;">
        📋 СХЕМА РАБОТЫ МЕХАНИЗМА
    </div>

    <!-- Шаг 1 -->
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: center; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);">
        ⏰ РЕГЛАМЕНТНОЕ ЗАДАНИЕ ЗАПУЩЕНО
    </div>

    <div style="text-align: center; font-size: 28px; color: #4a90d9; line-height: 1.2;">
        ⬇️
    </div>

    <!-- Шаг 2 -->
    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: center; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(245, 87, 108, 0.3);">
        🔍 СБОР МЕТРИК ЗА ТЕКУЩИЙ ДЕНЬ
    </div>

    <div style="display: flex; justify-content: space-around; align-items: center; padding: 6px 0;">
        <div style="text-align: center; font-size: 28px; color: #2e7d32;">⬇️</div>
        <div style="font-size: 18px; color: #888;">и</div>
        <div style="text-align: center; font-size: 28px; color: #c62828;">⬇️</div>
    </div>

    <!-- Шаг 3: Две колонки -->
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 8px 0;">

        <!-- Левая колонка -->
        <div style="background: linear-gradient(135deg, #a8e063 0%, #56ab2f 100%); color: white; padding: 16px 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(86, 171, 47, 0.3);">
            <div style="font-size: 20px; font-weight: 700; margin-bottom: 8px;">📝 ЗАПИСЬ В ЖР</div>
            <div style="line-height: 1.8; font-size: 14px;">
                🟢 Информационное событие<br>
                ⚙️ Полный текст отчёта<br>
                📊 Видно в журнале регистрации
            </div>
        </div>

        <!-- Правая колонка -->
        <div style="background: linear-gradient(135deg, #fdc830 0%, #f37335 100%); color: white; padding: 16px 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(243, 115, 53, 0.3);">
            <div style="font-size: 20px; font-weight: 700; margin-bottom: 8px;">📨 ОБНОВЛЕНИЕ ОПОВЕЩЕНИЯ</div>
            <div style="line-height: 1.8; font-size: 14px;">
                🔄 Запись есть → дописываем сверху<br>
                🛑 Записи нет → выходим<br>
                📅 История сохраняется
            </div>
        </div>

    </div>

</div>

---

### 🎯 Итог

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">📌 Что делает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">🔧 Как работает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">✅ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Собирает метрики производительности</td>
        <td style="padding: 10px;">ЖР + состояние РЗ за текущий день</td>
        <td style="padding: 10px;">📊 Актуальная картина дня</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Фиксирует отчёт в ЖР</td>
        <td style="padding: 10px;">Информационное событие</td>
        <td style="padding: 10px;">📋 Полный аудит работы РЗ</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Обновляет существующее оповещение</td>
        <td style="padding: 10px;">Новый текст сверху, старый ниже</td>
        <td style="padding: 10px;">📂 Накопительная история</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Не создаёт лишних записей</td>
        <td style="padding: 10px;">При отсутствии записи — выход</td>
        <td style="padding: 10px;">🚫 Мусор в регистре не плодится</td>
    </tr>
</table>

---

## ⚙️ Основные возможности

### ✅ Автоматический ежедневный сбор метрик

При запуске регламентного задания система:

- Определяет период **с начала текущего дня по конец текущего дня**
- Выгружает из журнала регистрации события уровня «Ошибка» и «Предупреждение»
- Считает количество взаимоблокировок (`_$Transaction$_.Deadlock`)
- Перебирает все регламентные задания и считает завершившиеся с ошибкой
- Формирует текстовый отчёт

---

### 📝 Обновление оповещения без создания новой записи

Механизм обновления работает по принципу «существует — дополняем, не существует — не трогаем»:

1. Запрос к регистру «Оповещения» по `АдресБазы` + `Заголовок` (через `ПОДСТРОКА`)
2. Если запись не найдена — выход без создания
3. Если запись найдена — через `МенеджерЗаписи` она открывается и обновляется:
   - новый текст с шапкой даты ставится в начало
   - старый текст остаётся ниже под разделителем

---

### 🛡️ Сохранение совместимости

<div style="background: #f0f7ff; border-left: 5px solid #4a90d9; padding: 16px 20px; border-radius: 8px; margin: 12px 0;">

- 📅 **Записи, созданные ранее**, продолжают использоваться — механизм только дополняет их
- 🔄 **Сравнение заголовков** через `ПОДСТРОКА(..., 1, 150)` — обход типа «Строка неограниченной длины»
- 📋 **Ошибки** (например, при выгрузке ЖР или обновлении записи) фиксируются в ЖР отдельным событием

</div>

---

## ⏰ Оптимизация расписания регламентных заданий

---

### 📌 Описание доработки

<div style="background: #f0f7ff; border-left: 5px solid #4a90d9; padding: 16px 20px; border-radius: 8px; margin: 12px 0;">

В рамках релиза проведён **аудит и пересмотр расписания всех регламентных заданий** с целью снижения пиковой нагрузки на сервер и исключения параллельных тяжёлых операций.

**Ключевые принципы оптимизации:**

- 🔀 **Разнос тяжёлых операций по времени** — чтобы они не выполнялись одновременно
- 🌙 **Вынос ресурсоёмких заданий в ночные часы** и выходные дни
- 🚫 **Отказ от избыточных запусков** — интервалы приведены к реально необходимым
- 📊 **Оптимизация частоты обновления данных**, не влияющих на оперативную работу пользователей

</div>

---

### ⚙️ Механизм работы

#### 📄 Что изменено

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #4a90d9; color: white; padding: 10px;">✅ Задание</th>
        <th style="background: #4a90d9; color: white; padding: 10px;">🔄 Новое расписание</th>
    </tr>
    <tr>
        <td style="padding: 10px;">ОбновлениеИндекса</td>
        <td style="padding: 10px;">Раз в день, ночью (02:00)</td>
    </tr>
    <tr>
        <td style="padding: 10px;">СлияниеИндексов</td>
        <td style="padding: 10px;">Раз в неделю, выходной день</td>
    </tr>
    <tr>
        <td style="padding: 10px;">СвернутьРегистры</td>
        <td style="padding: 10px;">Раз в месяц, выходной день</td>
    </tr>
    <tr>
        <td style="padding: 10px;">СборИнформацииВЖР</td>
        <td style="padding: 10px;">Раз в день, ночью (03:00)</td>
    </tr>
    <tr>
        <td style="padding: 10px;">КурсВалюты</td>
        <td style="padding: 10px;">Раз в день, утром (07:00)</td>
    </tr>
    <tr>
        <td style="padding: 10px;">КонтрольАктивностиПользователей</td>
        <td style="padding: 10px;">Раз в день, утром</td>
    </tr>
    <tr>
        <td style="padding: 10px;">ПроверкаОбновлений</td>
        <td style="padding: 10px;">Раз в день, днём (13:00)</td>
    </tr>
    <tr>
        <td style="padding: 10px;">ОбновлениеДоступаНаУровнеЗаписей</td>
        <td style="padding: 10px;">Каждые 15 минут, рабочее время</td>
    </tr>
    <tr>
        <td style="padding: 10px;">ЗаполнениеДанныхДляОграниченияДоступа</td>
        <td style="padding: 10px;">Каждые 15 минут, рабочее время</td>
    </tr>
    <tr>
        <td style="padding: 10px;">ОтложенноеОбновлениеИБ</td>
        <td style="padding: 10px;">Вручную, по окну обслуживания</td>
    </tr>
    <tr>
        <td style="padding: 10px;">БлокировкаСеансов</td>
        <td style="padding: 10px;">Вручную, при обслуживании</td>
    </tr>
</table>

---

### 🛡️ Защита от пиковых нагрузок

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #2e7d32; color: white; padding: 10px;">✅ Правило</th>
        <th style="background: #2e7d32; color: white; padding: 10px;">⏭️ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Тяжёлые задания не пересекаются по времени</td>
        <td style="padding: 10px;">🛡️ Нет конкуренции за ресурсы сервера</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Периодичность &gt; среднего времени выполнения</td>
        <td style="padding: 10px;">🛡️ Задания не «догоняют» друг друга</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Тяжёлые операции в нерабочее время</td>
        <td style="padding: 10px;">🛡️ Пользователи не ощущают замедления</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Частые задания — только для оперативных данных</td>
        <td style="padding: 10px;">🛡️ Нет избыточной нагрузки на СУБД</td>
    </tr>
</table>

---

### 📋 Рекомендации по настройке

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #6a1b9a; color: white; padding: 10px;">🖐️ Категория</th>
        <th style="background: #6a1b9a; color: white; padding: 10px;">📌 Что делать</th>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">⚙️ <b>Тяжёлые задания</b></td>
        <td style="padding: 10px;">Запускать ночью или в выходные, разносить по времени</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">🔐 <b>Безопасность</b></td>
        <td style="padding: 10px;">Оставить частый запуск (5–15 минут) — критично для прав доступа</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">💰 <b>Финансы и торговля</b></td>
        <td style="padding: 10px;">Раз в день ночью или перед началом рабочего дня</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">🔄 <b>Обновления</b></td>
        <td style="padding: 10px;">Только вручную, в согласованное окно обслуживания</td>
    </tr>
</table>

---

### ⚙️ Технические особенности

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 12px 0;">

<div style="background: #e8f5e9; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #2e7d32;">
    ✅ Единый график для всех РЗ
</div>

<div style="background: #e3f2fd; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #1565c0;">
    📊 Разнос тяжёлых операций по времени
</div>

<div style="background: #fff3e0; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #f57c00;">
    🌙 Тяжёлое — в нерабочие часы
</div>

<div style="background: #fce4ec; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #c62828;">
    🚫 Отключены избыточные запуски
</div>

<div style="background: #f3e5f5; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #6a1b9a;">
    📝 Документированное расписание
</div>

<div style="background: #e0f7fa; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #00838f;">
    🔍 Возможность точечной перенастройки
</div>

</div>

---

### 📊 Схема распределения нагрузки

<div style="background: #f8fafc; border-radius: 12px; padding: 20px; border: 1px solid #e1e4e8; margin: 16px 0; font-family: 'Segoe UI', Arial, sans-serif;">

    <div style="text-align: center; font-size: 16px; font-weight: 600; color: #1a1a2e; margin-bottom: 12px;">
        📋 РАСПРЕДЕЛЕНИЕ РЕГЛАМЕНТНЫХ ЗАДАНИЙ ПО ВРЕМЕНИ
    </div>

    <!-- Утро -->
    <div style="background: linear-gradient(135deg, #a8e063 0%, #56ab2f 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: left; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(86, 171, 47, 0.3);">
        🌅 УТРО (07:00) — Курс валют, контроль активности пользователей
    </div>

    <div style="text-align: center; font-size: 22px; color: #4a90d9; line-height: 1.2;">⬇️</div>

    <!-- День -->
    <div style="background: linear-gradient(135deg, #fdc830 0%, #f37335 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: left; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(243, 115, 53, 0.3);">
        ☀️ ДЕНЬ (13:00) — Проверка обновлений, доступ на уровне записей (каждые 15 мин)
    </div>

    <div style="text-align: center; font-size: 22px; color: #4a90d9; line-height: 1.2;">⬇️</div>

    <!-- Вечер -->
    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: left; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(245, 87, 108, 0.3);">
        🌆 ВЕЧЕР (20:00) — Перенос актов на следующий день
    </div>

    <div style="text-align: center; font-size: 22px; color: #4a90d9; line-height: 1.2;">⬇️</div>

    <!-- Ночь -->
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: left; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);">
        🌙 НОЧЬ (01:00–03:00) — Обновление индексов, купоны, акции, отчёты, ЖР
    </div>

    <div style="text-align: center; font-size: 22px; color: #4a90d9; line-height: 1.2;">⬇️</div>

    <!-- Выходные -->
    <div style="background: linear-gradient(135deg, #c62828 0%, #b71c1c 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: left; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(198, 40, 40, 0.3);">
        📅 ВЫХОДНЫЕ / РАЗ В МЕСЯЦ — Слияние индексов, сворачивание регистров
    </div>

</div>

---

### 🎯 Итог

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">📌 Что делает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">🔧 Как работает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">✅ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Разносит РЗ по времени</td>
        <td style="padding: 10px;">Единый график запусков</td>
        <td style="padding: 10px;">📉 Снижение пиковой нагрузки</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Убирает параллельные тяжёлые операции</td>
        <td style="padding: 10px;">Разные временные окна</td>
        <td style="padding: 10px;">⚡ Стабильная работа сервера</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Снижает нагрузку в рабочее время</td>
        <td style="padding: 10px;">Тяжёлое — ночью и в выходные</td>
        <td style="padding: 10px;">🙂 Комфортная работа пользователей</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Убирает лишние запуски</td>
        <td style="padding: 10px;">Периодичность по потребности</td>
        <td style="padding: 10px;">🚫 Меньше нагрузок на СУБД</td>
    </tr>
</table>

---

## ⚙️ Настройка мониторинга

### Сравнение: до и после

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 16px 0; font-size: 14px;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Параметр</th>
        <th style="background: linear-gradient(135deg, #c62828, #b71c1c); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">До релиза 4.26.39.1</th>
        <th style="background: linear-gradient(135deg, #2e7d32, #1b5e20); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">После релиза 4.26.39.1</th>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Сбор метрик</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Вручную</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Автоматически по расписанию РЗ</td>
    </tr>
    <tr style="background: #e8f5e9;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>История отчётов</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">❌ Нет</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">✅ Накопительный текст в регистре</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Создание «пустых» записей</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Возможно</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Исключено — запись не создаётся</td>
    </tr>
    <tr style="background: #e8f5e9;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Период сбора</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">24 часа от текущего момента</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">С начала дня по конец дня</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Адресация ошибок</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Только почта</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Через регистр «Оповещения»</td>
    </tr>
    <tr style="background: #e8f5e9;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Расписание регламентных заданий</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Разрозненное, с параллельными тяжёлыми операциями</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Единое, с разносом тяжёлых операций по времени</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Нагрузка в рабочее время</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Пиковая — из-за совпадения тяжёлых заданий</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Равномерная — тяжёлое вынесено в ночь</td>
    </tr>
</table>

---

### 🛠️ Где задаётся

Общий модуль и РЗ доступны в конфигураторе:

> **Общие модули → МониторингПроизводительности → ВыполнитьМониторинг**
>
> **Регламентные задания → МониторингПроизводительности** (расписание: ежедневно)
>
> **Регламентные задания → [все остальные]** — расписание настроено вручную согласно таблице распределения

Получатель уведомлений задаётся в реквизите `Получатели` регистра «Оповещения» — по умолчанию `artem240992@bk.ru`. При необходимости значение меняется в самой записи регистра.

---

### 📊 Схема работы
┌─────────────────────────────────────────────────────────────────────┐
│ Ежедневный мониторинг производительности 1С │
│ │
│ 1️⃣ РЗ запускается по расписанию │
│ │
│ 2️⃣ Сбор метрик: │
│ ├─ Ошибки из ЖР за текущий день │
│ ├─ Предупреждения из ЖР │
│ ├─ Взаимоблокировки │
│ └─ РЗ со статусом «ЗавершеноСОшибкой» │
│ │
│ 3️⃣ Формирование текста отчёта │
│ │
│ 4️⃣ Запись отчёта в ЖР (информационное событие) │
│ │
│ 5️⃣ Обновление оповещения: │
│ ├─ Запись есть → новый текст сверху, старый ниже │
│ └─ Записи нет → выход без создания │
└─────────────────────────────────────────────────────────────────────┘


---

## ✍️ Заключение

Релиз 4.26.39.1 внедряет **систему автоматического мониторинга производительности** и **оптимизацию расписания регламентных заданий**, обеспечивая:

- ✅ **Автоматизацию** – ежедневный сбор метрик без участия администратора
- ✅ **Прозрачность** – все данные фиксируются в журнале регистрации
- ✅ **Накопительную историю** – отчёты дописываются в существующее оповещение, свежий сверху
- ✅ **Отсутствие мусора** – новые записи в регистре не создаются, если их не было
- ✅ **Снижение нагрузки** – тяжёлые регламентные задания вынесены в нерабочее время
- ✅ **Чистоту архитектуры** – отдельный модуль `МониторингПроизводительности` + РЗ

Система даёт администратору постоянную обратную связь о состоянии информационной базы, не засоряя регистр лишними записями и не создавая дубликатов. Расписание регламентных заданий теперь исключает пиковые нагрузки и обеспечивает стабильную работу пользователей в течение всего рабочего дня.

---

# ⚡ Релиз 4.26.38.1

## Переход на периодический регистр настроек проверки материалов: история, аудит и гибкое управление

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <b style="color: #1a73e8;">⚡Релиз 4.26.38.1</b> — замена константы <b>«ДатаВключениеПроверкиматериаловВПереплет»</b> 
                на периодический регистр сведений <b>«НастройкиПроверкиМатериаловПереплета»</b>.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
               ✅  Теперь проверка материалов управляется <b>по дате документа</b>, а не по одной «дате отсечения».
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Каждое изменение настройки <b>версионируется</b>: видно, кто и когда включал или выключал проверку.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Старое значение из константы <b>переносится автоматически</b> — история документов не ломается.
            </p>
        </td>
    </tr>
</table>

---

## 🎯 Основные цели релиза

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 16px 0; font-size: 14px;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Цель</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Описание</th>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Гибкое управление проверкой</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Включение и выключение проверки многократно, с привязкой к датам</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Аудит изменений</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Фиксация ответственного и комментария для каждой записи</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Безболезненная миграция</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Значение из константы переносится автоматически, старое поведение сохраняется</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Чистота архитектуры</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Уход от «заплатки» в виде константы-переключателя</td>
    </tr>
</table>

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <b style="color: #1a73e8;">##⚡ Регистр сведений «НастройкиПроверкиМатериаловПереплета»</b></p> 
                <b style="color: #1a73e8;">### Описание функционала </b></p>
                <b style="color: #1a73e8;">Проверка материалов теперь управляется периодическим регистром сведений с историей изменений.</b>
                <b>**Как это работает:**</b></p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                1. 📅 **Периодичность «По дню»** — каждая запись действует с указанной даты до следующей записи. </p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                2. 🔄 **Режим записи «Независимый»** — одна настройка, один ресурс.</p>
        <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                3. 📊 **Ресурс «ПроверкаВключена»** — булево значение, действующее на дату.</p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                4. 👤 **Реквизит «Ответственный»** — пользователь, изменивший настройку.</p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                5. 📝 **Реквизит «Комментарий»** — причина или пояснение изменения.</p>
        </td>
    </tr>
</table>

---

## 🔄 Бизнес-процесс

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 16px 20px;"> <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;"> <span style="font-size: 20px;">🔄</span> <b style="color: #1a73e8;">Бизнес-процесс</b> — единый цикл управления материалами для переплета, в котором правило проверки теперь определяется <b>по дате документа</b>, а не по одной дате отсечения. </p> </td> </tr> </table>

<table cellpadding="14" cellspacing="0" style="border-left: 5px solid #f5a623; background: #fff8f0; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 14px 18px;">
1. 📄 Пользователь создаёт документ «ПереплетВКР»

2. 📅 Система определяет дату документа

3. 🔍 Запрос к регистру <b>«НастройкиПроверкиМатериаловПереплета»</b>:

<table cellpadding="8" cellspacing="0" style="border-collapse: collapse; width: 100%; margin: 8px 0; border: none;"> <tr> <td style="padding: 6px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #e8f5e9; padding: 10px 14px; border-radius: 6px; border-left: 4px solid #2e7d32;"> <b>✅ Запись найдена</b><br> <span style="padding-left: 18px;">Берём значение из регистра</span><br> <span style="padding-left: 18px;">Игнорируем константу</span> </div> </td> <td style="padding: 6px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #fff3e0; padding: 10px 14px; border-radius: 6px; border-left: 4px solid #f57c00;"> <b>⚠️ Записей нет</b><br> <span style="padding-left: 18px;">Fallback на константу</span><br> <span style="padding-left: 18px;">Старое поведение сохранено</span> </div> </td> </tr> </table>

4. ⚙️ Проверка выполняется только если на дату документа настройка активна

</td> </tr> </table>

### Приоритет источников значения

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;"> <tr> <th style="background: #6a1b9a; color: white; padding: 10px;">🥇 Приоритет</th> <th style="background: #6a1b9a; color: white; padding: 10px;">📌 Источник</th> <th style="background: #6a1b9a; color: white; padding: 10px;">⚙️ Условие</th> </tr> <tr> <td style="padding: 10px; text-align: center;"><b>1</b></td> <td style="padding: 10px;">Регистр «НастройкиПроверкиМатериаловПереплета»</td> <td style="padding: 10px;">Есть запись с периодом ≤ даты документа</td> </tr> <tr> <td style="padding: 10px; text-align: center;"><b>2</b></td> <td style="padding: 10px;">Константа «ДатаВключениеПроверкиматериаловВПереплет»</td> <td style="padding: 10px;">Записей в регистре нет — используется как история</td> </tr> <tr> <td style="padding: 10px; text-align: center;"><b>3</b></td> <td style="padding: 10px;">Проверка выключена</td> <td style="padding: 10px;">Ни регистр, ни константа не задают значение</td> </tr> </table>

---

## 📦 Автоматический перенос значения из константы

---

### 📌 Описание функционала

<div style="background: #f0f7ff; border-left: 5px solid #4a90d9; padding: 16px 20px; border-radius: 8px; margin: 12px 0;">

При обновлении конфигурации система выполняет **однократную миграцию**:

- 🔍 **Проверяет**, есть ли записи в регистре
- 📅 **Читает** текущее значение константы
- 📝 **Создаёт запись** в регистре с датой из константы и значением «Проверка включена»
- 🛡️ **Повторный запуск** ничего не делает — миграция идемпотентна

</div>

---

### ⚙️ Механизм работы

#### 📄 При обновлении конфигурации

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #4a90d9; color: white; padding: 10px;">✅ Условие</th>
        <th style="background: #4a90d9; color: white; padding: 10px;">🔄 Действие</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Регистр пуст<br><b>И</b><br>Константа заполнена</td>
        <td style="padding: 10px;">
            • 📅 Создаётся запись с периодом = дате из константы<br>
            • ✅ Значение <b>«ПроверкаВключена = Истина»</b><br>
            • 📝 Комментарий: <b>«Автоматический перенос из константы»</b>
        </td>
    </tr>
    <tr>
        <td style="padding: 10px;">Регистр уже содержит записи</td>
        <td style="padding: 10px;">⏭️ Миграция пропускается</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Константа не заполнена</td>
        <td style="padding: 10px;">⏭️ Переносить нечего</td>
    </tr>
</table>

---

### 🛡️ Защита от повторной миграции

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #2e7d32; color: white; padding: 10px;">✅ Проверка</th>
        <th style="background: #2e7d32; color: white; padding: 10px;">⏭️ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Наличие записей в регистре</td>
        <td style="padding: 10px;">⏭️ Миграция не выполняется</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Пустая константа</td>
        <td style="padding: 10px;">⏭️ Миграция не выполняется</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Ошибка при записи</td>
        <td style="padding: 10px;">📝 Запись в журнал регистрации</td>
    </tr>
</table>

---

### 📋 Использование

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #6a1b9a; color: white; padding: 10px;">🖐️ Способ</th>
        <th style="background: #6a1b9a; color: white; padding: 10px;">📌 Описание</th>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">🖐️ <b>Ручное включение / выключение</b></td>
        <td style="padding: 10px;">Через форму списка регистра — доступно администратору</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">⏰ <b>Автоматический перенос</b></td>
        <td style="padding: 10px;">Однократно при обновлении конфигурации через обработчик обновления ИБ</td>
    </tr>
</table>

---

### ⚙️ Технические особенности

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 12px 0;">

<div style="background: #e8f5e9; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #2e7d32;">
    ✅ Периодичность «По дню» — история изменений
</div>

<div style="background: #e3f2fd; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #1565c0;">
    📊 Режим записи «Независимый»
</div>

<div style="background: #fff3e0; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #f57c00;">
    🛠️ Обработка ошибок миграции в журнале регистрации
</div>

<div style="background: #fce4ec; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #c62828;">
    🚫 Блокировка не используется — гонок нет
</div>

<div style="background: #f3e5f5; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #6a1b9a;">
    📝 Ответственный и комментарий в каждой записи
</div>

</div>

---

### 📊 Схема работы

<div style="background: #f8fafc; border-radius: 12px; padding: 20px; border: 1px solid #e1e4e8; margin: 16px 0; font-family: 'Segoe UI', Arial, sans-serif;">

    <div style="text-align: center; font-size: 16px; font-weight: 600; color: #1a1a2e; margin-bottom: 12px;">
        📋 СХЕМА РАБОТЫ МЕХАНИЗМА
    </div>

    <!-- Шаг 1 -->
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: center; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);">
        📄 ДОКУМЕНТ «ПЕРЕПЛЕТВКР» СОЗДАЁТСЯ
    </div>

    <div style="text-align: center; font-size: 28px; color: #4a90d9; line-height: 1.2;">
        ⬇️
    </div>

    <!-- Шаг 2 -->
    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: center; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(245, 87, 108, 0.3);">
        🔍 ЗАПРОС К РЕГИСТРУ ПО ДАТЕ ДОКУМЕНТА
    </div>

    <div style="display: flex; justify-content: space-around; align-items: center; padding: 6px 0;">
        <div style="text-align: center; font-size: 28px; color: #2e7d32;">⬇️</div>
        <div style="font-size: 18px; color: #888;">или</div>
        <div style="text-align: center; font-size: 28px; color: #c62828;">⬇️</div>
    </div>

    <!-- Шаг 3: Две колонки -->
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 8px 0;">

        <!-- Левая колонка -->
        <div style="background: linear-gradient(135deg, #a8e063 0%, #56ab2f 100%); color: white; padding: 16px 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(86, 171, 47, 0.3);">
            <div style="font-size: 20px; font-weight: 700; margin-bottom: 8px;">✅ ЗАПИСЬ НАЙДЕНА</div>
            <div style="line-height: 1.8; font-size: 14px;">
                🟢 Берём значение из регистра<br>
                ⚙️ Проверка по настройке<br>
                📊 Константа игнорируется
            </div>
        </div>

        <!-- Правая колонка -->
        <div style="background: linear-gradient(135deg, #fdc830 0%, #f37335 100%); color: white; padding: 16px 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(243, 115, 53, 0.3);">
            <div style="font-size: 20px; font-weight: 700; margin-bottom: 8px;">⚠️ ЗАПИСЕЙ НЕТ</div>
            <div style="line-height: 1.8; font-size: 14px;">
                🔄 Fallback на константу<br>
                📅 Старое поведение сохранено<br>
                🛡️ История не ломается
            </div>
        </div>

    </div>

</div>

---

### 🎯 Итог

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">📌 Что делает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">🔧 Как работает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">✅ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Управляет проверкой материалов</td>
        <td style="padding: 10px;">Периодический регистр сведений</td>
        <td style="padding: 10px;">📂 Гибкая настройка по датам</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Хранит историю изменений</td>
        <td style="padding: 10px;">Ответственный + комментарий</td>
        <td style="padding: 10px;">📋 Полный аудит</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Сохраняет совместимость</td>
        <td style="padding: 10px;">Fallback на константу</td>
        <td style="padding: 10px;">🚫 Старые документы не ломаются</td>
    </tr>
</table>

---

## ⚙️ Основные возможности

### ✅ Управление проверкой по дате документа

При проведении документа «ПереплетВКР» система автоматически:

- Определяет дату документа
- Запрашивает у регистра «НастройкиПроверкиМатериаловПереплета» последнюю запись с периодом ≤ даты документа
- Если запись найдена — использует её значение
- Если записей нет — обращается к константе (fallback)
- Выполняет проверку остатков только при активной настройке

---

### 📝 Изменение настройки без конфигуратора

Администратор может:

1. Открыть форму списка регистра «НастройкиПроверкиМатериаловПереплета»
2. Добавить запись с нужной датой и значением «ПроверкаВключена»
3. Указать комментарий (например, «Включаем проверку с нового квартала»)
4. Система автоматически зафиксирует ответственного и дату записи

---

### 🛡️ Сохранение совместимости

<div style="background: #f0f7ff; border-left: 5px solid #4a90d9; padding: 16px 20px; border-radius: 8px; margin: 12px 0;">

- 📅 **Старые документы** продолжают проверяться по правилам константы
- 🔄 **Новые документы** используют актуальное значение из регистра
- 📋 **Дата константы** автоматически становится первой записью регистра при обновлении

</div>

---

## ⚙️ Настройка проверки материалов

### Сравнение: до и после

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 16px 0; font-size: 14px;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Параметр</th>
        <th style="background: linear-gradient(135deg, #c62828, #b71c1c); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">До релиза 4.26.38.1</th>
        <th style="background: linear-gradient(135deg, #2e7d32, #1b5e20); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">После релиза 4.26.38.1</th>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Источник настройки</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Константа</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Регистр сведений (+ fallback на константу)</td>
    </tr>
    <tr style="background: #e8f5e9;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>История изменений</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">❌ Нет</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">✅ Полная, с ответственным и комментарием</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Логика применения</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Дата документа ≥ дата константы</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Значение из регистра на дату документа</td>
    </tr>
    <tr style="background: #e8f5e9;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Многократное переключение</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">❌ Невозможно</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">✅ Да, с привязкой к датам</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Изменение из интерфейса</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Только через форму констант</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Через форму списка регистра</td>
    </tr>
</table>

---

### 🛠️ Где задаётся

Регистр доступен в разделе:

> **Администрирование → Настройки проверки материалов → Форма списка регистра «НастройкиПроверкиМатериаловПереплета»**

Константа **«ДатаВключениеПроверкиматериаловВПереплет»** остаётся в конфигурации как **fallback** и используется только при отсутствии записей в регистре. Планируется удаление константы в следующих релизах после полного перехода.

---

### 📊 Схема работы

```
┌─────────────────────────────────────────────────────────────────────┐
│           Определение настройки проверки на дату документа          │
│                                                                     │
│  1️⃣  Запрос к регистру «НастройкиПроверкиМатериаловПереплета»       │
│                                                                     │
│  2️⃣  Есть запись с периодом ≤ даты документа?                       │
│      ├─ Да → Возвращаем значение «ПроверкаВключена»                 │
│      └─ Нет → Переход к шагу 3                                      │
│                                                                     │
│  3️⃣  Константа заполнена?                                           │
│      ├─ Нет → Проверка НЕ выполняется                                │
│      └─ Да → Дата документа ≥ Дата константы?                       │
│              ├─ Нет → Проверка НЕ выполняется                        │
│              └─ Да → Проверка ВЫПОЛНЯЕТСЯ                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## ✍️ Заключение

Релиз 4.26.38.1 переводит управление проверкой материалов на **периодический регистр сведений**, обеспечивая:

- ✅ **Гибкость** – включение и выключение проверки в любой момент, с привязкой к датам
- ✅ **Прозрачность** – видно, кто и когда менял настройку
- ✅ **Совместимость** – старое значение из константы переносится автоматически
- ✅ **Чистоту архитектуры** – уход от «заплатки» в виде единственной константы

Система становится более предсказуемой и удобной для администрирования: теперь настройку можно менять без правки конфигурации, а история изменений всегда под рукой.

---

# ⚡ Релиз 4.26.36.1

## Комплексная система управления материалами для переплета и автоматизация создания заявок на пополнение склада

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <b style="color: #1a73e8;">⚡Релиз 4.26.36.1</b> — полный цикл управления материалами для переплета: 
                от контроля остатков на складе до автоматического формирования приходных документов.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
               ✅  Система объединяет документы <b>«ПереплетВКР»</b>, <b>«ЗаявкаНаПриходНаСклад»</b> и <b>«ПриходнаяНакладная»</b> 
                в единый бизнес-процесс, минимизируя ручной труд и исключая ошибки, связанные с нехваткой материалов.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Автоматическое оповещение о новых версиях при запуске 1С.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                ✅  Закрытие устаревших заказов роботом.
            </p>
        </td>
    </tr>
</table>

---
## 🎯 Основные цели релиза

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 16px 0; font-size: 14px;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Цель</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Описание</th>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Автоматизация контроля остатков</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Исключение проведения документов при нехватке материалов</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Ускорение создания заявок</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Снижение временных затрат на формирование заявок на пополнение</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Ограничение выбора товаров</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Предотвращение ошибочного выбора материалов для переплета</td>
    </tr>
    <tr>
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>Автоматическая обработка заявок</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">Сокращение ручного труда при создании приходных накладных</td>
    </tr>
</table>

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <b style="color: #1a73e8;">##⚡Автоматическое оповещение о новых версиях</b></p> 
                <b style="color: #1a73e8;">### Описание функционала </b></p>
                <b style="color: #1a73e8;">Реализован механизм автоматического оповещения пользователей о выходе новой версии конфигурации.</b><b>**Как это работает:**</b></p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                1. 🔄 **Регламентное задание** «Проверка обновлений» выполняется автоматически (по умолчанию ежедневно) и проверяет наличие новой версии в репозитории GitHub. </p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                2. 📊 **Результат проверки** сохраняется в регистре сведений `РезультатыПроверкиОбновлений`.</p>
        <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                3. 🔔 **При запуске 1С** система проверяет наличие непрочитанных уведомлений и, если новая версия доступна, показывает оповещение.</p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                При запуске 1С, если доступна новая версия, в окне сообщений появляется уведомление:
                <b> Доступна новая версия: 35.08.24.26. Текущая версия: 4.26.36.1. Рекомендуем обновить конфигурацию до актуальной версии.</b>
            </p>
        </td>
    </tr>
</table>

---

## 🔄 Бизнес-процесс
<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 16px 20px;"> <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;"> <span style="font-size: 20px;">🔄</span> <b style="color: #1a73e8;">Бизнес-процесс</b> — единый цикл управления материалами для переплета, объединяющий документы <b>«ПереплетВКР»</b>, <b>«ЗаявкаНаПриходНаСклад»</b> и <b>«ПриходнаяНакладная»</b>. </p> </td> </tr> </table>

<table cellpadding="14" cellspacing="0" style="border-left: 5px solid #f5a623; background: #fff8f0; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 14px 18px;">
1. 🔍 Проверка остатков материалов (папки, скобы)

2. 📊 Остаток < требуемого?

<table cellpadding="8" cellspacing="0" style="border-collapse: collapse; width: 100%; margin: 8px 0; border: none;"> <tr> <td style="padding: 6px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #e8f5e9; padding: 10px 14px; border-radius: 6px; border-left: 4px solid #2e7d32;"> <b>✅ Да</b> → Документ записывается <b>(НЕ ПРОВОДИТСЯ)</b><br> <span style="padding-left: 18px;">❓ Задаётся вопрос о создании заявки</span><br> <span style="padding-left: 18px;">👍 Пользователь соглашается → Создание ЗНПТ</span> </div> </td> <td style="padding: 6px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #ffebee; padding: 10px 14px; border-radius: 6px; border-left: 4px solid #c62828;"> <b>❌ Нет</b> → Документ <b>проводится</b><br> <span style="padding-left: 18px;">✅ Движения по регистрам</span><br> <span style="padding-left: 18px;">📊 Обновление накоплений</span> </div> </td> </tr> </table> </td> </tr> </table>

### Документ «ЗАЯВКА НА ПРИХОД НА СКЛАД»

<table cellpadding="14" cellspacing="0" style="border-left: 5px solid #6a1b9a; background: #f3e5f5; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 14px 18px;">
3. 🟢 Автоматически заполняется реквизит <b>«ДляПереплета» = Истина</b>

4. 🎯 Контроль выбора товаров:

<table cellpadding="6" cellspacing="0" style="border-collapse: collapse; width: 100%; margin: 6px 0; border: none;"> <tr> <td style="padding: 4px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #e8f5e9; padding: 6px 12px; border-radius: 4px; border-left: 3px solid #2e7d32; font-size: 14px;"> 🟢 <b>«ДляПереплета» включена</b> → только вид <b>«ТоварыДляПереплета»</b> </div> </td> <td style="padding: 4px 0; border: none; width: 50%; vertical-align: top;"> <div style="background: #fff3e0; padding: 6px 12px; border-radius: 4px; border-left: 3px solid #f57c00; font-size: 14px;"> 🟠 <b>«ДляПереплета» выключена</b> → все, кроме этого вида </div> </td> </tr> </table>
5. ⚙️ Проведение заявки → формирование движений по регистру <b>«УчетМатериаловПереплета»</b>

6. ⏳ Ожидание обработки регламентным заданием

</td> </tr> </table>


### РЕГЛАМЕНТНОЕ ЗАДАНИЕ «ОБРАБОТКА ЗАЯВОК»

<table cellpadding="14" cellspacing="0" style="border-left: 5px solid #1565c0; background: #e3f2fd; border-radius: 8px; margin: 12px 0; width: 100%;"> <tr> <td style="padding: 14px 18px;">
7. 🔍 Поиск необработанных заявок (Обработан = Ложь)

8. 📄 Создание документа <b>«ПриходнаяНакладная»</b> с переносом товаров

9. ✅ Отметка заявки как обработанной (Обработан = Истина)

</td> </tr> </table>


---

## 🤖 Автоматическое закрытие устаревших заказов

---

### 📌 Описание функционала

<div style="background: #f0f7ff; border-left: 5px solid #4a90d9; padding: 16px 20px; border-radius: 8px; margin: 12px 0;">

Реализован механизм автоматического закрытия заказов, которые:

- 📅 **Созданы в прошлых годах** (год даты заказа < текущего года)
- 🚫 **Не имеют статуса «Закрыт»**
- 🔍 **Не были ранее закрыты роботом** (проверка по комментарию)

</div>

---

### ⚙️ Механизм работы

#### 📄 При открытии документа

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #4a90d9; color: white; padding: 10px;">✅ Условие</th>
        <th style="background: #4a90d9; color: white; padding: 10px;">🔄 Действие</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Заказ создан в прошлом году<br><b>И</b><br>В комментариях есть «Закрыт роботом»</td>
        <td style="padding: 10px;">
            • 🟢 Элемент <b>«ФайлЗакрыт»</b> становится видимым<br>
            • 🔴 Элемент <b>«СтатусЗаказа»</b> скрывается<br>
            • 🔒 Форма переводится в режим <b>«Только просмотр»</b>
        </td>
    </tr>
</table>

#### 📦 Массовое закрытие заказов

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #f5a623; color: white; padding: 10px;">🔍 Поиск заказов</th>
        <th style="background: #f5a623; color: white; padding: 10px;">⚡ Обработка</th>
        <th style="background: #f5a623; color: white; padding: 10px;">📝 Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">
            • Год даты < текущего<br>
            • Статус ≠ «Закрыт»<br>
            • Нет фразы «Закрыт роботом»
        </td>
        <td style="padding: 10px;">
            • Статус → «Закрыт»<br>
            • Добавлен комментарий:<br>
            <code>«Закрыт роботом [дата]»</code><br>
            • Привилегированный режим
        </td>
        <td style="padding: 10px;">
            ✅ Заказ закрыт<br>
            📋 История в комментариях<br>
            📊 Логирование в сообщениях
        </td>
    </tr>
</table>

---

### 🛡️ Защита от повторного закрытия

<table border="1" cellpadding="10" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #2e7d32; color: white; padding: 10px;">✅ Проверка</th>
        <th style="background: #2e7d32; color: white; padding: 10px;">⏭️ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Наличие фразы <b>«Закрыт роботом»</b></td>
        <td style="padding: 10px;">⏭️ Заказ пропускается</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Статус уже <b>«Закрыт»</b></td>
        <td style="padding: 10px;">⏭️ Заказ пропускается</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Комментарий пустой</td>
        <td style="padding: 10px;">📝 Добавляется новая строка</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Комментарий не пустой</td>
        <td style="padding: 10px;">📝 Добавляется строка с датой закрытия</td>
    </tr>
</table>

---

### 📋 Использование

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: #6a1b9a; color: white; padding: 10px;">🖐️ Способ</th>
        <th style="background: #6a1b9a; color: white; padding: 10px;">📌 Описание</th>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">🖐️ <b>Ручной запуск</b></td>
        <td style="padding: 10px;">Через кнопку на форме или внешнюю обработку</td>
    </tr>
    <tr>
        <td style="padding: 10px; text-align: center;">⏰ <b>Автоматический</b></td>
        <td style="padding: 10px;">Настроено регламентное задание (каждый день; с 7:00:00 по 18:00:00 один раз в день, завершать после 18:00:00)</td>
    </tr>
</table>

---

### ⚙️ Технические особенности

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 12px 0;">

<div style="background: #e8f5e9; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #2e7d32;">
    ✅ Работает в привилегированном режиме
</div>

<div style="background: #e3f2fd; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #1565c0;">
    📊 Логирование всех операций в окно сообщений
</div>

<div style="background: #fff3e0; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #f57c00;">
    🛠️ Обработка ошибок по каждому заказу
</div>

<div style="background: #fce4ec; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #c62828;">
    🚫 Игнорирование уже обработанных заказов
</div>

<div style="background: #f3e5f5; padding: 12px 16px; border-radius: 8px; border-left: 4px solid #6a1b9a;">
    📝 Сохранение истории закрытия в комментариях
</div>

</div>

---

### 📊 Схема работы
<div style="background: #f8fafc; border-radius: 12px; padding: 20px; border: 1px solid #e1e4e8; margin: 16px 0; font-family: 'Segoe UI', Arial, sans-serif;">

    <div style="text-align: center; font-size: 16px; font-weight: 600; color: #1a1a2e; margin-bottom: 12px;">
        📋 СХЕМА РАБОТЫ МЕХАНИЗМА
    </div>

    <!-- Шаг 1 -->
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: center; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);">
        📅 ЗАКАЗ СОЗДАН В ПРОШЛОМ ГОДУ
    </div>

    <!-- Стрелка вниз -->
    <div style="text-align: center; font-size: 28px; color: #4a90d9; line-height: 1.2;">
        ⬇️
    </div>

    <!-- Шаг 2 -->
    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; padding: 14px 20px; border-radius: 10px; text-align: center; font-weight: 600; font-size: 15px; margin: 8px 0; box-shadow: 0 4px 12px rgba(245, 87, 108, 0.3);">
        🔍 ПРОВЕРКА: статус ≠ «Закрыт» И нет «Закрыт роботом»
    </div>

    <!-- Стрелка вниз с разветвлением -->
    <div style="display: flex; justify-content: space-around; align-items: center; padding: 6px 0;">
        <div style="text-align: center; font-size: 28px; color: #2e7d32;">⬇️</div>
        <div style="font-size: 18px; color: #888;">или</div>
        <div style="text-align: center; font-size: 28px; color: #c62828;">⬇️</div>
    </div>

    <!-- Шаг 3: Две колонки -->
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 8px 0;">

        <!-- Левая колонка (ДА) -->
        <div style="background: linear-gradient(135deg, #a8e063 0%, #56ab2f 100%); color: white; padding: 16px 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(86, 171, 47, 0.3);">
            <div style="font-size: 20px; font-weight: 700; margin-bottom: 8px;">✅ УСЛОВИЕ ВЫПОЛНЕНО</div>
            <div style="line-height: 1.8; font-size: 14px;">
                🟢 Статус → <b>«Закрыт»</b><br>
                📝 Добавлен комментарий<br>
                📊 Логирование в сообщениях
            </div>
        </div>

        <!-- Правая колонка (НЕТ) -->
        <div style="background: linear-gradient(135deg, #fdc830 0%, #f37335 100%); color: white; padding: 16px 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(243, 115, 53, 0.3);">
            <div style="font-size: 20px; font-weight: 700; margin-bottom: 8px;">⏭️ УСЛОВИЕ НЕ ВЫПОЛНЕНО</div>
            <div style="line-height: 1.8; font-size: 14px;">
                🔄 Заказ <b>пропускается</b><br>
                📋 Остаётся без изменений<br>
                💤 Ожидание следующей проверки
            </div>
        </div>

    </div>

</div>
---

### 🎯 Итог

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 12px 0;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">📌 Что делает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">🔧 Как работает</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; padding: 12px;">✅ Результат</th>
    </tr>
    <tr>
        <td style="padding: 10px;">Закрывает устаревшие заказы</td>
        <td style="padding: 10px;">Автоматически или вручную</td>
        <td style="padding: 10px;">📂 База чистая, порядок</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Отмечает закрытые роботом</td>
        <td style="padding: 10px;">Проверка комментариев</td>
        <td style="padding: 10px;">📋 История закрытий</td>
    </tr>
    <tr>
        <td style="padding: 10px;">Защищает от повторной обработки</td>
        <td style="padding: 10px;">Двойная проверка</td>
        <td style="padding: 10px;">🚫 Нет дублей</td>
    </tr>
</table>


## ⚙️ Основные возможности

### ✅ Контроль остатков материалов

При проведении документа «ПереплетВКР» система автоматически:

- Суммирует потребность в материалах из табличной части
- Получает актуальные остатки из регистра «УчетМатериаловПереплета»
- Сравнивает и принимает решение:
  - **Остаток < требуемого** → документ записывается, но не проводится
  - **Остаток ≥ 100 шт.** → документ проводится в штатном режиме
  - **0 < Остаток < 100** → документ проводится, предлагается создать заявку

---

### 📝 Создание заявки на пополнение

При недостатке материалов пользователю предлагается:

1. Создать заявку на пополнение склада
2. Заявка формируется с заполненными реквизитами:
   - `ДляПереплета = Истина`
   - `Склад = Справочники.Склады.ЭБ`
   - Товары: папки и/или скобы (объединены в один документ)

---

### 🛡️ Ограничение выбора товаров для переплета

В документе «ЗаявкаНаПриходНаСклад» реализована интеллектуальная фильтрация:

<table border="1" cellpadding="12" cellspacing="0" style="border-collapse: collapse; width: 100%; border-color: #ddd; margin: 16px 0; font-size: 14px;">
    <tr>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Режим</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Разрешённые товары</th>
        <th style="background: linear-gradient(135deg, #4a90d9, #357abd); color: white; font-weight: 600; padding: 12px 16px; text-align: left; border: 1px solid #ddd;">Запрещённые товары</th>
    </tr>
    <tr style="background: #e8f5e9;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>🟢 ДляПереплета = Истина</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">✅ Только вид <b>«ТоварыДляПереплета»</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">⛔ Все остальные</td>
    </tr>
    <tr style="background: #fff3e0;">
        <td style="padding: 10px 14px; border: 1px solid #ddd;"><b>🟠 ДляПереплета = Ложь</b></td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">✅ Все товары</td>
        <td style="padding: 10px 14px; border: 1px solid #ddd;">⛔ Вид <b>«ТоварыДляПереплета»</b></td>
    </tr>
</table>

**Механизмы контроля:**

<ul style="list-style-type: none; padding-left: 0; line-height: 2;">
    <li>🔹 <b>При выборе товара</b> в табличной части</li>
    <li>🔹 <b>При изменении состояния</b> галочки</li>
    <li>🔹 <b>В форме подбора</b> товаров</li>
</ul>

---

## ⚙️ Настройка проверки материалов

### Константа «ДатаВключениеПроверкиматериаловВПереплет»

Для гибкого управления моментом начала проверки остатков материалов при проведении документа «ПереплетВКР» введена глобальная константа:

| Параметр | Значение |
|----------|----------|
| **Имя константы** | `ДатаВключениеПроверкиматериаловВПереплет` |
| **Тип** | Дата |
| **Назначение** | Определяет дату, с которой начинает действовать проверка остатков материалов (папки, скобы) |
| **Формат** | Дата в формате `ДД.ММ.ГГГГ` |

---

### 📋 Как это работает

1. Если константа **не заполнена** — проверка материалов **не выполняется**.
2. Если константа **заполнена**:
   - Проверка выполняется только для документов, у которых **дата документа >= дата константы**.
   - Для документов, созданных до указанной даты, проверка остатков **не выполняется**.

---

### 🎯 Назначение

- ✅ Позволяет **поэтапно внедрять** контроль остатков в старые документы
- ✅ Даёт возможность **тестировать** механизм на новых документах, не затрагивая историю
- ✅ Обеспечивает **гибкость** настройки без изменения программного кода

---

### 🛠️ Где задаётся

Константа доступна в разделе:

> **Администрирование → Форма констант → Вкладка «Технические» → ДатаВключениеПроверкиматериаловВПереплет**

---

### 📊 Схема работы
┌─────────────────────────────────────────────────────────────────────┐
│ Проверка остатков материалов при проведении «ПереплетВКР» │
│ │
│ 1️⃣ Константа «ДатаВключениеПроверкиматериаловВПереплет» │
│ │
│ 2️⃣ Константа заполнена? │
│ ├─ Нет → Проверка НЕ выполняется │
│ └─ Да → Дата документа >= Дата константы? │
│ ├─ Нет → Проверка НЕ выполняется │
│ └─ Да → Проверка ВЫПОЛНЯЕТСЯ │
└─────────────────────────────────────────────────────────────────────┘


### 🤖 Регламентное задание

Автоматическая обработка заявок выполняется в фоновом режиме:

- **Расписание:** настроено администратором (рекомендуется 5 минут)
- **Действия:**
  1. Поиск необработанных заявок
  2. Создание приходных накладных
  3. Отметка заявок как обработанных
- **Логирование:** все операции фиксируются в окне сообщений
---

## ✍️ Заключение

Релиз 4.26.36.1 полностью автоматизирует процесс управления материалами для переплета, обеспечивая:

- ✅ **Надёжность** – контроль остатков на каждом этапе
- ✅ **Скорость** – мгновенное создание заявок
- ✅ **Безопасность** – ограничение выбора товаров
- ✅ **Эффективность** – автоматическая обработка заявок

Система становится более интеллектуальной и дружественной к пользователю, освобождая сотрудников от рутинных операций и минимизируя вероятность ошибок.

---

# ⚡ Релиз 3.07.20.26

### 1. Автоматическая проверка обновлений из GitHub

- Добавлен общий модуль `ПроверкаОбновленийСервер` с логикой HTTP-запроса к GitHub API для получения последнего релиза.
- Создано регламентное задание «Проверка обновлений», выполняющееся с заданной периодичностью (по умолчанию раз в сутки).
- Реализовано сравнение версии конфигурации с версией из репозитория (поле `name` или `tag_name` ответа GitHub).
- Добавлен регистр сведений `РезультатыПроверкиОбновлений` для хранения результатов проверки и статуса прочтения пользователем.
- При старте системы пользователю показывается оповещение, если обнаружена новая версия.

### 2. Гибкая настройка через константы

Созданы константы:

- `РепозиторийОбновленийURL` – адрес API GitHub
- `ТокенДоступаGitHub` – токен для приватных репозиториев (опционально)
- `EmailАдминистратора` – для уведомлений (опционально)
- `ИспользоватьGitHubAPI` – флаг для выбора способа получения версии
- `ПериодПроверкиОбновлений` – интервал в часах
- `ПутьКПроверкеОбновлений` – путь к внешней обработке

### 3. Оптимизация и поддержка мобильной платформы

- Вся бизнес-логика вынесена в общие модули
- Клиентский код формы документа упрощён
- Обеспечена совместимость с мобильной платформой и режимом совместимости 8.3.12
- Заменён проблемный `HTTPСоединение` на `WinHTTP.WinHTTPRequest.5.1`

### 4. Служебные доработки

- Добавлена процедура автоматической инициализации констант
- Регистр `ПравилаЗаполнения` пополнен правилами для распознавания паспортных данных
- Устранены ошибки инициализации модулей

---

# ⚡ Релиз 2.07.19.26

## 🆕 Новые возможности

### Интеграция с облачными OCR-сервисами

Добавлена поддержка распознавания текста и структурированных данных из изображений через:

- **Yandex Vision OCR** (модель `passport` для паспортов РФ, модель `text` для прочих документов)
- **OCR.space** (резервный/альтернативный вариант)

### Автоматическое заполнение реквизитов справочников

Создан универсальный механизм на основе регистра сведений «ПравилаЗаполнения», позволяющий:

- Заполнять реквизиты «Клиенты» из паспорта (ФИО, дата рождения, серия/номер, кем выдан, код подразделения)
- Заполнять реквизиты «Контрагенты» из справок (ИНН, КПП, ОГРН, адрес, телефон, email)

### Интерактивная проверка заполненных данных

- Незаполненные обязательные поля подсвечиваются на форме
- Пользователь может отредактировать данные до сохранения
- Реализован диалог подтверждения сохранения

### Управление ключами доступа через константы

Введены константы для хранения API-ключей:

- `YandexVisionAPIKey` – ключ Яндекс.Облака
- `YandexVisionFolderID` – идентификатор каталога
- `OCRspaceAPIKey` – ключ OCR.space
- `DefaultOCRService` – выбор сервиса по умолчанию

---

## 🔧 Технические особенности

- Обеспечена совместимость с мобильной платформой (режим совместимости 8.3.12)
- Все вызовы к серверу вынесены в серверные методы
- Реализована обработка ошибок при распознавании и заполнении

---

## 📦 Для работы необходимо

1. Зарегистрироваться в Yandex Cloud и получить API-ключ и Folder ID
2. Заполнить соответствующие константы в системе
3. Создать регистр сведений «ПравилаЗаполнения»
4. Убедиться, что справочники содержат все необходимые реквизиты

---

## 🐛 Исправления

- Устранена ошибка инициализации модуля `СтандартныеПодсистемыСервер`
- Исправлен синтаксис удаления записей из регистра
- Исправлены ошибки совместимости с мобильной платформой

---

# ⚡ Релиз 1.07.13.26

- Переработана работа сверки регистров
- Введена константа для работы механизма «СвернутьРегистрКурсовВалютЗаГод»

---

# ⚡ Релиз 1.06.21.26

- Переработан механизм загрузки курса валют
- Если у курса валют есть свернутый месяц, то для него не грузятся больше курсы

---

# ⚡ Релиз 2.05.21.26

- Добавлена роль `ИзменениеОрганизацииИФилиалаВПереплете` для открытия на постоянной основе редактирования в Переплете

---

# ⚡ Релиз 1.04.08.26

- Доработан регистр «Купоны»
- Введена новая форма для вывода информации по обновлениям

---

# ⚡ Релиз 1.03.16.26

- Сделано создание купонов из рандомных символов
- Доработана форма изменения версии
- Добавлен регистр «ДатыСкидок»
- В версии 2.03.26.26 регистры «Купоны» и «ДатыСкидок» будут доработаны

---

**📅 Последнее обновление:** 26.08.2026
