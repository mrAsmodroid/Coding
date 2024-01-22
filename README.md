# mrAsmodroid Coding Rules

[![Site](https://softwaredev.space/assets/images/ico.webp)](https://softwaredev.space/)

Данное правило, распространяется для языка C# под разработку на движке Unity. Не является истиной для всех и применяется только в разработке проектов относящихся к моей комаде. Все, чего нет тут, уточняется лично со мной и тут будет дописываться. 

Введение:
   * [Методы](#Методы)
   * [Типы_Данных_(Переменные)](#Типы_Данных_Переменные)
   * [Скрипты](#Скрипты)
   * [Каталоги](#Каталоги)
   * [Настройки_GIT](#Настройки_GIT)
   

## Методы

В начале названия нестандартного метода, пишется “V_” и далее, наименование. 
#### Пример:
```csharp
void V_Metod()
{
   //
   //...code...
   //
}
```

Наименования методов используют стиль PascalCase в этом стиле каждое слово начинается с заглавной буквы, после "V_"
#### Пример:
```csharp
void V_SendMessage()
{
   //
   //...code...
   //
}

void V_CloseManagerWindow()
{
   //
   //...code...
   //
}
```

Методы, к которым идет обращение из внешнего интерфейса, например кнопки, пишутся капслоком. Визуально отсекая методы, которые вызваеются извне кодов и облегчая их поиск, при объявлении ссылки на той же кнопке
#### Пример:
```csharp
public void V_CLICK()
{
   //
   //...code...
   //
}
```

В начале названия каждого IEnumerator, пишется “IE_” и далее, наименование. 
#### Пример:
```csharp
IEnumerator IE_Action()
{
   //
   //...code...
   //
}
```

Каждый метод, должен выполнять только одну поставленную задачу, не превращая методы в мусорку из кучи кодов. Так же, если мето открытого типа, то подметоды, являются только закрытыми.
#### Пример не верного решения:
```csharp
//Метод, в которое идет обращение кода, для выполения действия
public void V_RunAPP()
{
   //
   //...Some code...
   //

   //Preload

   //
   //...Some Preload code...
   //

   //set texture

   //
   //...Some elttexturehe code...
   //

   //create local BD

   //
   //...Some BD code...
   //
}
```
#### Пример верного решения:
```csharp
public void V_RunAPP()
{
   //
   //...Some code...
   //

   //Preload
   V_Preload();

   //set texture
   V_SetTexure();

   //create local BD
   V_CreateLocalBD();
}
void V_Preload()
{
   //
   //...Some elthe code...
   //
}
void V_SetTexure()
{
   //
   //...Some elthe code...
   //
}
void V_CreateLocalBD()
{
   //
   //...Some elthe code...
   //
}
```

Инкапсуляция методов
#### Пример:
```csharp
//Все приватные методы, корутины и т.д. пишутся без слова private. Так как метод пермаментно является приватным и таким образом, можно визуально отделить закрытые и открытые методы.
void V_One()
{
   ...
}

//Все открытые методы, корутины и т.д. выглядят стандартно
public void V_Two()
{
   ...
}
```

## Типы_Данных_(Переменные)

Глобальные типы данных начинаются с "_тип переменной"(c самленькой буквы, кроме исключений) далее "_подтип"(если есть) далее "_наименование". Исключение у bool (_is_), [Enum.cs](#Enumcs)(_e_), [Data.cs](#Datacs)(_d_), синглтона(m_). Или сокращение у стандартных типов данных Unity или string. Само наименование, имеет стиль PascalCase. 
#### Пример:
```csharp
public static scr_SomeScript scr_SomeScript;
E_SomeEnum _e_SomeEnum;
bool _is_What;
int _int_Number;
float _float_Speed;
string _str_Text;
double _double_Math;
Vector3 _v3_pos;
Vector2 _v2_pos;
Transform _trans_ContactObj;
GameObject _go_Player;
Texture2D _txt2D_Plane;
RectTransform _rect_UI;
ScrollRect _scroll_Button;
TMP_Text _TMP_Title;
TMP_InputField _inputField_Input;
List<int> _int_List_NumbersFromBD;
```
Так же, если типы данных используются для дополнительных проверок или являются временными зеркальными копиями основного типа или для временной установки данных, идут следующее прописание
#### Пример:
```csharp
//основной тип
bool _is_What;
//тип триггерного типа, который проверяет позицию основного и принимает его значение, в случае смены позиции. Является отсечкой выполения кода
bool _is_What_CHECK;
//тип контролирующего типа, основная проверка котрого идет через основную позицию. Является отсечкой выполения кода
bool _is_What_CONTROL;
```

Все глобальные типы данных, являются закрытыми, если требуется их внешнее изменения, то устанавливается атрибут [SerializeField]
#### Пример:
```csharp
bool _is_one;
[SerializeField] bool _is_two;
```

Изменение типов данных идет через локальный метод, если требуется взаимодействие извне, то через одинарные функции get или set. Устанавливаются под комментарием //GET или //SET и начинаются названия начинаются с "GET_" or "SET_"
#### Пример:
```csharp
[SerializeField] bool _is_one;
[SerializeField] TMP_Text _TMP_title;

//GET
public bool GET_one { get => _is_one; }
public string GET_titleText { get => _TMP_title.text; }
//SET
public bool SET_one { set => _is_one = value; }
public string SET_titleText { set => _TMP_title.text = value; }
```

Массивы, используются List<> а не [];

В случае, если типы данных, можно сгрупировать, то делать это, через структуру [Data.cs](#Datacs)
#### Пример не верного решения:
```csharp
//script Scripts/scr_Test.cs
public class scr_Test : MonoBehaviour
{
   [SerializeField] int _int_PlayerSize;
   [SerializeField] float _float_PlayerSpeed;
   [SerializeField] Texture2D _txt2D_Texture;
   [SerializeField] GameObject _gO_PlayerPrefub;
   [SerializeField] Transform _trans_ContactObj;
   [SerializeField] List<float> _float_List_Path;
}
```
#### Пример верного решения:
```csharp
//script Scripts/scr_Test.cs
public class scr_Test : MonoBehaviour
{
   [SerializeField] D_PlayerSetting _d_PlayerSetting;
   [SerializeField] Transform _trans_ContactObj;
   [SerializeField] List<float> _float_List_Path;
}
//script Scripts/Data.cs
{
   using System;
   [Serializable]
   public struct D_PlayerSetting
   {
      public int _int_PlayerSize;
      public float _float_PlayerSpeed;
      public Texture2D _txt2D_Texture;
      public GameObject _gO_PlayerPrefub;
   }
}
```

## Скрипты

Наименование скриптов начинается с "scr_" далее каталого и название в стиле PascalCase.
#### Пример:
Scripts
   - scr_General.cs
   - Data.cs
   - Enum.cs
   - /F_Player/
      - scr_Player_Setting.cs
      - scr_Player_Move.cs

Основная троица скриптов, которая обязательна в начале любого проекта, это:
Scripts
   - scr_General.cs
   - Data.cs
   - Enum.cs

### scr_General.cs
Есть скрипт, который управляет всеми основными настройками и хранит в себе БД всех материалов, которыми пользуется приложение. Явлыется синглтоном (m_General) и имеет функцию DontDestroyOnLoad(this);. Называется scr_General.cs и находится в корне каталога Scripts в проекте, привязан к объекту "GlobalSettings". При запросе исходников материалов или данных настроек, идет обращение к нему.

### Data.cs
Данный скрипт, хранит в себе структуры, для формирования групп типов данных для использования во всем проекте. Они имеют два уровня, основная структура и подструктура, котора относится к основной. Отличаются наименованием "D_name" и "Dm_name". Называется Data.cs и находится в корне каталога Scripts в проекте.
#### Пример из структуры готовог проекта:
```csharp
{
   using System;
   [Serializable]
   public struct D_Quest
   {
      public List<Dm_Quest_Data> _quests;
   }
   [Serializable]
      public struct Dm_Quest_Data
   {
      public string _name;
      public List<Dm_Quests> _quests;
   }
   [Serializable]
      public struct Dm_Quests
   {
      public string _name; // для редактора
      public int COUNT;
      public string _comment; //личный комментарий к этому вопросу
      public string _str_main_quest; // Основной вопрос
      public string _str_add_text_wind; // Дополнительная плашка с текстом
      public string _str_end_message; // Если это последний вопрос, отображение напутствующего сообщения
      public bool _is_ansers; // проверка на то, что ответ дан
      public int _int_emotion; // Эмоция над символом
      public string _str_emotion; // Текст вопроса эмоции
      public List<int> _int_list_emotion_number; // Номера ответов которые подулючаеют эмоцию
      public int _int_position_plaler; // Позиция игрока у символа
      public List<Dm_Symbol> _symbols; // База с объектом символа и его позиция
      public List<string> _ansers; //База с вопросом и возможными ответами
      public string _str_own_Anser; // Собственный ответ
      public bool _is_multy_anser; // Если ИСТИНА, то возможно выбирать несколько ответов
      public List<Dm_BlockAnswer> _block_check; //При _is_multy_anser = true, проверяется, нужно ли ограничить возможные ответы
      public bool _is_extra_end; // Если диаграмма обрывается на этом вопросе
      public int _int_extra_end; // Номер вопроса, являющегося консовкой
      public List<int> _int_list_answer_number; // Номера ответов
      public int _back_emotion; //Проверка предыдущего ответа по эмоции
      public List<Dm_BackAnser> _back_answers; // Проверка предыдущего связаного вопроса
   }
   [Serializable]
      public struct Dm_Symbol
   {
      public int _int_answer;
      public int _int_symbol_data;
   }
   [Serializable]
      public struct Dm_BackAnser
   { 
      public int _int_controll_quest; // номер предыдущего вопроса
      public List<int> _int_list_controll_answer_number; // номера ответов ведущий к этому вопросу
   }
}
```

### Enum.cs
Данный скрипт отвечает за все перечесления, используеммые в проекте. Называется Enum.cs и находится в корне каталога Scripts в проекте. Первое перечисление, всегда должно быть "Null,"
#### Пример из структуры готовог проекта:
```csharp
public enum E_Emotion
{
    Null,
    Bad,
    Normal,
    Good
}
public enum E_PlusMinus
{
    Null,
    Plus,
    Minus
}
public enum E_ButtonStatus
{
    Null,
    UnPress,
    Press
}
```

## Каталоги

Особенности в архитектуре каталогов проекта не много, но есть.
Стартово, в проект добавляется два каталога:
#### Пример
   - DATA_project
   - DATA_resources

В чем разница:

### DATA_project
Данный тип каталога хранит в себе все ресурсы, которые созданы внутри Unity, такие как префабы, материалы, шейдеры, анимации, настройки света и т.п. Под каждый тип, создется подкаталог, для организации врхитектуры.
#### Пример
- DATA_project
   - Prefabs
   - Animations
   - Shaders
   - ...
   - LightSettings

### Подкаталоги в папке Scripts
Все подкаталоги в папуе "/Scripts/" в начале имуют "F_".
#### Пример
- Scripts
   - F_VFX
   - F_Player
   - F_Camera

### DATA_resources
Данный каталог хранит в себе все внешние ресурсы, которые добавляются извне, такие как текстуры, аудио, 3Д модели, шрифты и т.д. плюс в отдельном подкаталоге "AddOn" хранятся дополнительные ассеты.
- DATA_resources
   - Sprites
   - Sounds
   - Fonts
   - 3D
   - ...
   - AddOn
      - TextMesh Pro

## Настройки_GIT

### Git Ignore
Последняя строчка добавляется только, если папка AddOn в сумме со всем проектом, превышает допустимые лимиты загрузки GIT (2Gb)
```
/*
!/Assets/
!/Packages/
!/ProjectSettings/
!/UserSettings/
/Assets/DATA_resources/AddOn*
```