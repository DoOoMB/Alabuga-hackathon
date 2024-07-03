# Alabuga-hackathon
 
Данный репозиторий является решением кейса для хакатона Алабуги. Задача заключалась в анализе тональности относительно конкретных организаций в статьях Ленты. 

## Эксперименты

Результаты экспериментов по нахождению именованных сущностей (в том числе, организаций) можно видеть в следующей таблице
![image](https://github.com/DoOoMB/Alabuga-hackathon/assets/74912440/53fcb62e-f1dc-47ec-a785-28f261d7d871)

Результаты экспериментов по анализу тональности (с учётом сущностей):
![image](https://github.com/DoOoMB/Alabuga-hackathon/assets/74912440/de03a961-e3ee-4a2e-b1a8-8514b168f5d8)

Лучшей моделью была признана "RuBERT x2 (binary classifications, 1-10ep, 0.01lr; 2-20ep, 0.01lr)", как показывающая лучшие результаты на всех классах. Данная модель является последовательным применением двух бинарных классификаторов, один из которых опеределяет нейтральные фразы, а второй - позитивные и отрицательные.

Сами эксперименты можно посмотреть [здесь](https://colab.research.google.com/drive/1Fe_o82vg1jGMxcXqy9WW_NXJb28lo8zB?usp=sharing). Данные расположены [здесь](https://drive.google.com/drive/folders/1YZG2qJDSCl_QZbeXejJ-dwpFmsSFtAJf?usp=drive_link).

## Сервер

Чтобы запустить код на локальной машине необходимо выполнить следующие команды (необходимо наличие Python на компьютере). Код тестировался на Windows 10, Python 3.11.

```
git clone https://github.com/DoOoMB/Alabuga-hackathon
python -m pip install -r requirements.txt
python manage.py
```

На сервере реализована авторизация, история запросов каждого пользователя, а также доступно API.

Команды API:
1. POST-запрос на страницу `https://<домен-сайта>/guest` с json вида ```{"url": "https://lenta.ru/news/2024/07/03/v-dagestane-zapretili-nosit-nikab-ranee-k-etomu-prizyval-bastrykin/"}``` выдаст данные об организациях и отношении к ним в этом тексте в формате `{"status": "ok", "output": {"companies": [{"name": "OrgName1", "estimate": "POSITIVE"}]}}`. В случае ошибки: `{"status": "error", "message": "error message"}`
