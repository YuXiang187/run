# JavaFX基础

## 结构

* 窗口（stage）
  * 场景（scene）
    * 根节点（Parent）
    * 根节点……

```java
public class TsetStage extends Application{
    public static void main(String[] args) {
        Application.launch(args);
    }
    //launch首先启动init，可以在这里连接数据库、读取配置文件
    public void init() throws Exception {}
    //窗口在这里写
    public void start(Stage primaryStage) throws Exception {}
    //关闭窗口时执行，可以在这里关闭数据库
    public void stop() throws Exception {}
}
```

## Application示例

```java
public void start(Stage stage) {
    Button button = new Button("我的Github");
    BorderPane pane = new BorderPane(button);

    button.setOnAction(e -> {
        getHostServices().showDocument("https://github.com/YuXiang187");
    });

    Scene scene = new Scene(pane, 300, 300);
    stage.setScene(scene);
    stage.setTitle("关于");
    stage.show();
}
```

## Stage示例

* Title

* icon：`stage.getIcons().add(new Image("image/logo.jpg"));`

* resiziable（是否可改变窗口大小）

* x, y, width, height

* StageStyle

  * DECORATED——白色背景，带有最小化/最大化/关闭等有操作系统平台装饰（默认）
  * UNDECORATED——白色背景，没有操作系统平台装饰（常用）
  * TRANSPARENT——透明背景，没有操作系统平台装饰
  * UTILITY——白色背景，只有关闭操作系统平台装饰

* Modality

  * `stage.initModality(Modality.NONE);`：可以操作父窗口
  * Modality.APPLICATION_MODAL：禁止操作父窗口以及在副窗口打开的其他窗口
  * Modality.WINDOW_MODAL：禁止操作父窗口，其他在副窗口打开的窗口可以使用

* event

  * 设置关闭事件：

    ```java
    Platform.setImplicitExit(false);//取消操作系统默认退出动作
    stage.setOnCloseRequest(windowEvent -> {
        windowEvent.consume();//点击关闭按钮，窗口不会退出
        Alert alert = new Alert(Alert.AlertType.CONFIRMATION);
        alert.setTitle("退出程序");
        alert.setHeaderText(null);
        alert.setContentText("您是否要退出程序？");
        Optional<ButtonType> result = alert.showAndWait();
        if (result.get() == ButtonType.OK) {
    //        stage.close(); //仅关闭窗口，程序仍在运行
            Platform.exit();
        }
    });
    ```

* 切换场景：`stage.setScene()`

* 设置鼠标图片：`scene.setCursor(new ImageCursor(new Image("image/cursorlogo.jpg")))`

## Node UI控件

* layoutX / layoutY / preWidth / preHeight
* style / visible / opacity / blendMode
  * `label.setStyle("-fx-border-color: blue; -fx-border-width: 3px");`
  * `label.setAlignment(Pos.CENTER);`：设置居中
  * `label.setOpacity(0.5);`：设置半透明
  * `label.setRotate(45);`：旋转
* translateX / translateY：横/竖移
* rotate / scaleX / scale：3D旋转
* parent / scene / id

## UI控件的属性绑定和监听

```java
public void start(Stage stage) {
    stage.setTitle("Title");

    Circle circle = new Circle();
    circle.setCenterX(250);
    circle.setCenterY(250);
    circle.setRadius(100);
    circle.setStroke(Color.BLACK);// 边框
//    circle.setStrokeWidth(10);// 边框大小
    circle.setFill(Color.WHITE);

    BorderPane pane = new BorderPane(circle);
    Scene scene = new Scene(pane);

    //绑定控件与场景，使圆一直显示在中间
    circle.centerXProperty().bind(scene.widthProperty().divide(2));
    circle.centerYProperty().bind(scene.heightProperty().divide(2));

    circle.centerXProperty().addListener(new ChangeListener<Number>() {
        @Override
        public void changed(ObservableValue<? extends Number> observableValue, Number number, Number t1) {
            System.out.println("x轴改变：" + t1);
        }
    });

    stage.setScene(scene);
    stage.show();
}
```

## 事件驱动

| User Action         | Source Object | Event Type Fired | Event Registration Method                     |
| ------------------- | ------------- | ---------------- | --------------------------------------------- |
| Click a button      | Button        | ActionEvent      | setOnAction(EventHandler\<ActionEvent>)       |
| Enter in text field | TextField     | ActionEvent      | setOnAction(EventHandler\<ActionEvent>)       |
| Check or uncheck    | RadioButton   | ActionEvent      | setOnAction(EventHandler\<ActionEvent>)       |
| Check or uncheck    | CheckBox      | ActionEvent      | setOnAction(EventHandler\<ActionEvent>)       |
| Select a new item   | ComboBox      | ActionEvent      | setOnAction(EventHandler\<ActionEvent>)       |
| Mouse pressed       | Node,Scene    | MouseEvent       | setOnMousePressed(EventHandler\<MouseEvent>)  |
| Mouse released      |               |                  | setOnMouseReleased(EventHandler\<MouseEvent>) |
| Mouse clicked       |               |                  | setOnMouseClicked(EventHandler\<MouseEvent>)  |
| Mouse entered       |               |                  | setOnMouseEntered(EventHandler\<MouseEvent>)  |
| Mouse exited        |               |                  | setOnMouseExited(EventHandler\<MouseEvent>)   |
| Mouse moved         |               |                  | setOnMouseMoved(EventHandler\<MouseEvent>)    |
| Mouse dragged       |               |                  | setOnMouseDragged(EventHandler\<MouseEvent>)  |
| Key pressed         | Node,Scene    | KeyEvent         | setOnKeyPressed(EventHandler\<KeyEvent>)      |
| Key released        |               |                  | setOnKeyReleased(EventHandler\<KeyEvent>)     |
| Key typed           |               |                  | setOnKeyTyped(EventHandler\<KeyEvent>)        |

键盘监听：

```java
KeyCode keyCode = event.getCode();
if(keyCode.equals(KeyCode.DOWN)) {
    //...
}
```

文件拖拽：

```java
public void start(Stage stage) {
    stage.setTitle("Title");

    TextField textField = new TextField();
    textField.setLayoutX(150);
    textField.setLayoutY(200);

    textField.setOnDragOver(dragEvent -> dragEvent.acceptTransferModes(TransferMode.ANY));

    textField.setOnDragDropped(dragEvent -> {
        Dragboard dragboard = dragEvent.getDragboard();
        if (dragboard.hasFiles()) {
            String path = dragboard.getFiles().get(0).getAbsolutePath();
            textField.setText(path);
        }
    });

    AnchorPane root = new AnchorPane();
    root.getChildren().add(textField);
    Scene scene = new Scene(root, 500, 500);
    stage.setScene(scene);
    stage.show();
}
```

## Color,Font,Image

* Color.rgb(255, 0, 0)
  Color.web("#f66a08")

* `button.setFont(Font.font("微软雅黑", FontWeight.BOLD, 30));`

  `label.setFont(new Font(30));`

  `loadFont(InputStream in, double size)`：读取资源文件下的字体

## FXML布局文件

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.*?>
<?import javafx.scene.layout.*?>

<?import javafx.scene.text.Font?>
<AnchorPane xmlns="http://javafx.com/javafx"
            xmlns:fx="http://javafx.com/fxml"
            fx:controller="com.yuxiang.test.AppController"
            prefHeight="400.0" prefWidth="600.0">

    <children>
        <Label fx:id="la" text="Hello World!" layoutX="150" layoutY="200">
            <font>
                <Font size="30"/>
            </font>
        </Label>
        <Button fx:id="bu" text="向上移动" layoutX="150" layoutY="260" onAction="#onUp"/>
    </children>

</AnchorPane>
```

```java
package com.yuxiang.test;

import javafx.fxml.FXML;
import javafx.scene.control.Button;
import javafx.scene.control.Label;

public class AppController {
    @FXML
    Label la;
    @FXML
    Button bu;

    public void onUp() {
        la.setLayoutY(la.getLayoutX() - 5);
    }
}
```

```java
public void start(Stage primaryStage) throws Exception {
    URL url = new File("src/layout/demo.fxml").toURI().toURL();
    Pane root = FXMLLoader.load(url);

    primaryStage.setTitle("连点器");
    Scene scene = new Scene(root, 500, 500);
    primaryStage.setScene(scene);
    primaryStage.show();
}
```

## Controller里的initialize方法

```java
public void initialize(){}
```

## 多线程操作

```java
button.setOnAction(e -> {
    Thread thread = new Thread(() -> {
        Platform.runLater(() -> {
            getHostServices().showDocument("https://github.com/YuXiang187");
            System.out.println("Opened Link");
        });
    });
    thread.start();
});
```