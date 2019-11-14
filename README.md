# mmc-code-guide
# Соглашения
### Сохранение контекста
```javascript
const self = this;
```
### this.get и this.set
this.get необходимо делать в начале метода, this.set - в конце
```javascript
var readonly = this.get('readonly');
readonly= ...
this.set('readonly', readonly);
```
### Работа с промисами
Если промис завершается с ошибкой, используйте для этого Promise.reject.
Запрещается определять успешность промиса через возвращаемую переменную:
```javascript
promiseFunc().then((ok) => {
	if (ok) {...} //так делать нельзя
	else {...}
})
```
Верный вариант:
```javascript
	promiseFunc().then(() => 
	{		//promise resolved (ok)	},
	{		//promise rejected (!ok)	});
```

# Рекомендации
### Расширение стандартных Ember объектов
Создайте инициализатор. Сделайте reopen расширяемого объекта. 
```javascript
export function initialize() {
	Ember.Route.reopen({
		...
	})
  }
```
Не забудьте использовать this.super в его наследниках, если они используют этот метод.
