
# Архитектура ПО. Семинар 11. Сервис-ориентированные архитектуры

Представить MVP проект с мессенджером, спроектированного в прошлой домашней работе.

---

В коде для этого семинара — три файла. App.java — класс расширяющий Application — загружает сцену, описанную в файле chatroom.fxml. А Controler.java — отвечает за обработку событий. То есть приложение, дизайн и управление не привязаны друг к другу, разработку, соблюдая внутренние стандарты можно вести независимо.

## Работа приложения:

Минимальные условия: считаем, что сервер запущен, и к нему подключен пользователь __ELIZA__.

![Screenshot01 - работа приложения](https://github.com/Ask1509/Software_Architecture_HW11/blob/722a613874818b91c4aa72631a2fb29553f1c1d5/img/page01.png))

В нижнее текстовое поле пользователь вводит сообщение, и нажав `ENTER`, или кликнув кнопку `Send`, отправляет его в поле __Chat__.

![Screenshot02 - работа приложения](https://github.com/Ask1509/Software_Architecture_HW11/blob/722a613874818b91c4aa72631a2fb29553f1c1d5/img/page02.png))
![Screenshot03 - работа приложения](https://github.com/Ask1509/Software_Architecture_HW11/blob/722a613874818b91c4aa72631a2fb29553f1c1d5/img/page03.png))
![Screenshot04 - работа приложения](/img/page04.png)
![Screenshot05 - работа приложения](/img/page05.png)
![Screenshot06 - работа приложения](/img/page06.png )

## Компоновка приложения
Графический интерфейс редактируется с помощью [Scene Builder](https://gluonhq.com/products/scene-builder/ "Страница Scene Builder"). 

Слева — иерархия объектов окна приложения. Справа — идентификатор _fx:id send_ для кнопки `Send`, и указание на вызов метода _sendButton_ из класса Controller.java. 


![Screenshot07 - работа в Scene Builder](/img/scenebuilder01.png)

Для текстового поля и соседней с ним кнопки в контроллер введены методы

```java
@FXML
private void sendEnter(KeyEvent event) {
	if (event.getCode() == KeyCode.ENTER) {
		sendMessage();
	}
}
```
и

```java
@FXML
private void sendButton(ActionEvent event) {
	sendMessage();
}
```

вызывающий общий метод обновления окна чата

```java
private void sendMessage() {
	String message = chat.getText();
	String probe = string.getText();
	message = message + probe + System.lineSeparator();
	chat.setText(message);
	string.setText("");
}
```

---

Справа — у поля Editable снята галка, для запрета ввода текста в TextArea с меткой Chat. Такой же запрет установлен для TextArea с меткой Clients.

![Screenshot08 - работа в Scene Builder](/img/scenebuilder02.png)

---
Аналогичным образом можно было бы смоделировать интерфейс в Figma, однако в контексте написания кода и работающего MVP в конкретном случае использовалась связка JavaFX и Scene Builder. А проектирование UI уже можно отдать в дизайн-команду вместе с работающим прототипом.
