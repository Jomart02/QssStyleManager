![Windows](https://github.com/barry-ran/QtScrcpy/workflows/Windows/badge.svg)
![Ubuntu](https://github.com/barry-ran/QtScrcpy/workflows/Ubuntu/badge.svg)
[![Qt](https://img.shields.io/badge/Qt-6.x-66cc00.svg)](https://www.qt.io/)
[![C++](https://img.shields.io/badge/C%2B%2B-17.0-4c979e.svg)](https://isocpp.org/)

# QssStyleManager
StyleManager for dynamically setting qt qss styles and working with several styles simultaneously from different parts of the program (qt c++)

# Feautures

## Init QSS 

In order to register your style file, you need to install it through this function
``` c++ 

//example 
StyleManager::getInstance()->setQssFile(objectName(),":/style/style");

// set QSS-file for owner
void setQssFile(const OwnerStyle &owner, const QString &qssFilePath);
```

OwnerStyle - your key to working with your style

## Init style settings 
In order to add style settings, you must set them using the same key as follows

```c++
//example
StyleManager::getInstance()->addStyle(objectName(), "day", ":/style/day");
StyleManager::getInstance()->addStyle(objectName(), "night", ":/style/night");
// add JSON-settings for style
 void addStyle(const OwnerStyle &owner, const NameStyle &styleName, const QString &jsonFilePath);
```
## Get result style

After that you can get your result
```c++
 setStyleSheet(StyleManager::getInstance()->getStyle(objectName(), "day"));
```

## QSS structure 

For this manager to work, you will need a style in which all fields for parsing must be wrapped in { }

```css
/* example */
QComboBox, QAbstractSpinBox, QLineEdit , QDateTimeEdit , QTimeEdit, QDateEdit{
    border: 1px solid {editWidgetBorder}; 
    padding-left: 2px;
    font-weight: bold;
    background-color:{editWidgetBackground};
    border-radius: 8px;
    color: {baseTextColor};
}

QCheckBox{
    color: {baseTextColor};
    font-weight: bold;
    background-color: transparent;
    height: 40px;
}
QCheckBox::indicator {
    width: 40px;
    height: 40px;
    image: url({iconCheckBox});
}
QCheckBox::indicator:checked {
    image: url({iconCheckBoxChecked});
}

```

And the settings json file for these keys

```json 
     day.json example

    "baseBackgroundColor":"#E9F8FF",
    "labelDefault":"#7E7E7E",
    "GroupBoxColor": "#FFFFFF",
    "baseTextColor": "#000000",

    "iconCombobox": ":/style/ArrowPopup",
    "iconCheckBox": ":/style/unchecked",
    "iconCheckBoxChecked": ":/style/checked",
    "iconRadioButton": ":/style/radioNo",
    "iconRadioButtonChecked": ":/style/radioYes",

    "editWidgetBorder":"#4150de",
    "editWidgetBorderDisabled":"#F0F0F0",
    "editWidgetDisabledText":"#CECECE",
     ...
```
```json 
     hight.json example
     
     "baseBackgroundColor":"#485160",
     "labelDefault":"#CECECE",
     "GroupBoxColor": "#2B313A",
     "baseTextColor": "#F0F0F0",

     "iconCombobox": ":/style/ArrowPopupNight",
     "iconCheckBox": ":/style/uncheckedNight",
     "iconCheckBoxChecked": ":/style/checkedNight",
     "iconRadioButton": ":/style/radioNoNight",
     "iconRadioButtonChecked": ":/style/radioYesNight",

     "editWidgetBorder":"#4150de",
     "editWidgetBorderDisabled":"#000000",
     "editWidgetDisabledText":"#7E7E7E",
     ...
```


## Custom style
To set up a directory for custom styles, you must specify its directory

```c++
     StyleManager::getInstance()->init(CUSTOM_STYLES);
```

You can check if there are custom styles and the directory itself
```c++
     StyleManager::getInstance()->isCustomStyles(CUSTOM_STYLES)
```


Get custom Styles
```c++
     // using CustomStyles = QList<QPair<QString, QString>>;
     // first - name style(filename)
     // second - path to file

 auto styles =  StyleManager::getInstance()->getCustomStyl(CUSTOM_STYLES);
    if(!styles.empty()){
        for(auto style : styles){
            StyleManager::getInstance()->addStyle(objectName(), style.first, style.second);
        }
    }
```

You can use any key for your style 
