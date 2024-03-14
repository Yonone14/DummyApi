# DummyAPI
Dummy API - площадка для тестирования API сервиса разразбатываемой социальной сети. Проект описывает процесс тестирования действий пользователя по созданию поста и проверки отображения листа ранее опубликованных постов. Информация представлена в виде майнд-карты и коллекции запросов в Postman, для которых создано окружение DummyAPI.postman_environment. 
## Оглавление
1. [Кратко о проекте](#Кратко-о-проекте)
2. [POST](#POST)
   * [GET/post (Get List)](#Get-post-Get-List)
   * [POST/post/create (Create Post)](#Post-post-create-Create-Post)
3. [Майнд-карта](#Майнд-карта)
4. [Баг-репорты](#Баг-репорты)
5. [Коллекции](#Коллекции)
   
## Кратко о проекте
https://dummyapi.io/ Dummy API - сервис для тестирования API. На сайт встроен блок документации, который содержит базовые настройки и данные для проверки ключевых объектов - пользователя, поста и комментариев. Для каждого из них приведены допустимые методы, адреса, тела запросов и ожидаемые ответы. Для выполнения запросов необходим персональный ключ app-id, получить который можно после регистрации на сервисе. Тестирование выполнено на примере объекта **Post**.
### POST
_____
### GET /post (Get List)
Возвращает список постов, отсортированных по дате создания.
* Доступен query params для вывода опредленной страницы.
* Доступен query params для вывода количества выводимых на одно странице постов.
* Доступен query params для филльтрации вывода только своих постов.

**Responce body**:
```javascript
{
data: Array(Model)
total: number(total items in DB)
page: number(current page)
limit: number(number of items on page)
}
```
**Post preview**:
```javascript
{
id: string(autogenerated)
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```
**User preview**:
```javascript
{
id: string(autogenerated)
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
picture: string(url)
}
```
____
### POST /post/create (Create Post)
Создает новый пост. Возвращает данные о посте.

**Request body**:
```javascript
{
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
owner: string(User id)
}
```
**Responce body**:
```javascript
{
id: string(autogenerated)
text: string(length: 6-1000)
image: string(url)
likes: number(init value: 0)
link: string(url, length: 6-200)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```
**User Preview**:
```javascript
{
id: string(autogenerated)
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
picture: string(url)
}
```
## Майнд-карта
Графическая форма тестирования объекта **Post**. Детализация сделана для **Get List** и **Create Post**.
<img src="Пост%20DummiAPI.jpg"/>

Также майнд-карту можно ![скачать](https://github.com/Yonone14/DummyApi/blob/main/DummiAPI.xmind)

## Баг-репорты
По результатам тестирования былы обнаружены баги. Вот несколько примеров:
* Создание поста с полем "text" из 5 символов ([ссылка_на_doc](https://github.com/Yonone14/DummyApi/blob/main/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BF%D0%BE%D1%81%D1%82%D0%B0%20%D1%81%20%D1%82%D0%B5%D0%BA%D1%81%D1%82%D0%BE%D0%BC%20%D0%B8%D0%B7%205%20%D1%81%D0%B8%D0%BC%D0%B2%D0%BE%D0%BB%D0%BE%D0%B2.docx)).
* Создание поста с boolean-значением поля "text" ([ссылка_на_doc](https://github.com/Yonone14/DummyApi/blob/main/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BF%D0%BE%D1%81%D1%82%D0%B0%20%D1%81%20Boolean-%D0%B7%D0%BD%D0%B0%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%D0%BC%20%D0%BF%D0%BE%D0%BB%D1%8F%20text.docx)).
* Переход на 999 страницу выдачи вместо недопустимой 1000-й ([ссылка_на_doc](https://github.com/Yonone14/DummyApi/blob/main/%D0%9F%D0%B5%D1%80%D0%B5%D1%85%D0%BE%D0%B4%20%D0%BD%D0%B0%20999%20%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D1%83%20%D0%B2%D1%8B%D0%B4%D0%B0%D1%87%D0%B8%20%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%BE%20%D0%BD%D0%B5%D0%B4%D0%BE%D0%BF%D1%83%D1%81%D1%82%D0%B8%D0%BC%D0%BE%D0%B9%201000-%D0%B9.docx)).

## Коллекции
Для проверки корректности функционала добавления нового поста и просмотра листа постов в Postman была создана коллекция **POST**. Для удобства работы запросы для разного функционала разделены по папкам Get Post List и Create Post. Ознакомиться с содержанием папок можно по ссылке https://github.com/Yonone14/DummyApi/blob/main/POST.postman_collection.json.



