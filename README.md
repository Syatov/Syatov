# Сятов Амир

**Позиция:** *Python jun+*

## Работа
Работаю в MixAI

## Обо мне
• [Подкаст](https://www.youtube.com/watch?v=enoZRj_lbPw)  
• [Статья](https://astanahub.com/ru/article/kak-14-letnii-rezident-jaiq-hub-zarabatyvaet-400-tysiach-tenge)  

## Навыки
• *Python*  
• *REST*  
• *Linux*  
• *CloudFare*  
• *disnake*  
• *aiogram*  
• *MySql*  

## Ссылки
• [Github](https://github.com/Syatov)  
• [Telegram](https://t.me/Syatov)  
• [Codeforces](https://codeforces.com/profile/Syatov)  

## Опыт работы
• **ApexNodes** — Техподдержка VDS 2года

• **Millida** — Создание Minecraft серверов, Python разработчик 6 месяцев

## Заказчики
• [*Millida*](https://millida.net/)   
• [*MCRU*](https://discord.gg/mcru)   
• *NewEra*  
• *Futurismo*  
• *Minecraft CIS*  
• [*JaiqHub*](https://www.instagram.com/jaiq.hub)   
• [*ndendena*](https://www.youtube.com/@ndendena)   

## Посмотреть мои работы
- [Futurismo bot](https://discord.gg/N4JxbJ5suC) - Универсальный дискорд бот
- [Боты Newera](https://discord.gg/S7aRAKMQWh) - Телеграмм и Discord боты для заказа , и также их синхронизация
- [Google-Sheet-Bot](https://github.com/Syatov/Google-Shets--TG-bot) - Телеграмм бот для рефералов и учета клиентов с занесением в Google таблицу
```
@router.message(AddContract.waiting_for_first_full_name)
async def add_first_employee(message: types.Message, state: FSMContext):
    first_name = message.text.strip()

    with get_db_connection() as db:
        cursor = db.cursor()
        cursor.execute("SELECT id FROM employees WHERE full_name = ?", (first_name,))
        first_employee = cursor.fetchone()

        if not first_employee:
            # Автоматически регистрируем сотрудника, если его нет
            cursor.execute("INSERT INTO employees (full_name) VALUES (?)", (first_name,))
            db.commit()
            first_employee_id = cursor.lastrowid
        else:
            first_employee_id = first_employee[0]

    await state.update_data(first_name=first_name, first_id=first_employee_id)
    await message.answer("Введите ФИО второго сотрудника:")
    await state.set_state(AddContract.waiting_for_second_full_name)


@router.message(AddContract.waiting_for_second_full_name)
async def add_second_employee(message: types.Message, state: FSMContext):
    second_name = message.text.strip()

    with get_db_connection() as db:
        cursor = db.cursor()
        cursor.execute("SELECT id FROM employees WHERE full_name = ?", (second_name,))
        second_employee = cursor.fetchone()

        if not second_employee:
            # Автоматически регистрируем второго сотрудника, если его нет
            cursor.execute("INSERT INTO employees (full_name) VALUES (?)", (second_name,))
            db.commit()
            second_employee_id = cursor.lastrowid
        else:
            second_employee_id = second_employee[0]

    data = await state.get_data()
    if second_employee_id == data["first_id"]:
        await message.answer("Ошибка: Оба сотрудника не могут быть одним и тем же человеком.")
        return

    await state.update_data(second_name=second_name, second_id=second_employee_id)
    await message.answer("Введите ссылку на документ соц. контракта:")
    await state.set_state(AddContract.waiting_for_link)
```

