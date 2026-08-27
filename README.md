# ⚡ Релиз 4.26.36.1

## Комплексная система управления материалами для переплета и автоматизация создания заявок на пополнение склада

---

<table cellpadding="16" cellspacing="0" style="border-left: 5px solid #4a90d9; background: #f8fafc; border-radius: 8px; margin: 12px 0; width: 100%;">
    <tr>
        <td style="padding: 16px 20px;">
            <p style="margin: 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                <span style="font-size: 20px;">⚡</span>
                <b style="color: #1a73e8;">Релиз 4.26.36.1</b> — полный цикл управления материалами для переплета: 
                от контроля остатков на складе до автоматического формирования приходных документов.
            </p>
            <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                Система объединяет документы <b>«ПереплетВКР»</b>, <b>«ЗаявкаНаПриходНаСклад»</b> и <b>«ПриходнаяНакладная»</b> 
                в единый бизнес-процесс, минимизируя ручной труд и исключая ошибки, связанные с нехваткой материалов.
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
                1. 🔄 **Регламентное задание** «Проверка обновлений» выполняется автоматически (по умолчанию ежедневно) и проверяет наличие новой версии в репозитории GitHub. 
                2. 📊 **Результат проверки** сохраняется в регистре сведений `РезультатыПроверкиОбновлений`.
                3. 🔔 **При запуске 1С** система проверяет наличие непрочитанных уведомлений и, если новая версия доступна, показывает оповещение.
</p>
    <p style="margin: 8px 0 0 0; font-size: 15px; line-height: 1.8; color: #2d3748;">
                📋 Что видит пользователь
                При запуске 1С, если доступна новая версия, в окне сообщений появляется уведомление:
                <b>📢 Доступна новая версия: 35.08.24.26. Текущая версия: 4.26.36.1.
                📢 Рекомендуем обновить конфигурацию до актуальной версии.</b>
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
        <td style="padding: 10px;">Настроено регламентное задание (ежедневно в 02:00)</td>
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
