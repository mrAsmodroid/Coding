# mrAsmodroid Coding Rules

[![Site](https://softwaredev.space/assets/images/ico.webp)](https://softwaredev.space/)

Введение:

[Методы](#Методы)

## Методы

В начале названия нестандартного метода, пишется “V_” и далее, название метода слитно. 
#### Пример:
```csharp
public void V_Metod()
{
   ...
}
```

Наименования методов используют стиль PascalCase в этом стиле каждое слово начинается с заглавной буквы, после "V_"
#### Пример:
```csharp
public void V_SendMessage()
{
   ...
}

public void V_CloseManagerWindow()
{
   ...
}
```

Методы, к которым идет обращение из внешнего интерфейса, например кнопки, пишутся капслоком
#### Пример:
```csharp
public void V_CLICK()
{
   ...
}
```