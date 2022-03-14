# How to use QT with CPP

## Dynamacly create widgets

```cpp
QLabel *m_TextLabel = new QLabel();

m_TextLabel->setText(“I love you guys”);
m_TextLabel->setStyleSheet("QLabel { background-color : red; color : blue; }");

ui->emptySpace->layout()->addWidget(m_TextLabel);
```

> The important part of it is `addWidget()`, that's how you add a widget to another. (For example, a button on a layout)

## Create UI with `QT Creator`
In this case, first you have to use `QT Creator` to generate the `xx.ui` file.

Then bind it in C++ with `setupUi()`: https://stackoverflow.com/questions/5692991/qt-setupui


Then try to operate it like:

```c++
ui->widgetIDorName->setVisible(false);
```

Check [this](https://github.com/aoloe/cpp-qt-ui-cmake/blob/master/src/mainwindow.cpp) or check [OBS](https://github.com/obsproject/obs-studio).