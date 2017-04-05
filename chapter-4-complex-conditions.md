# Глава 4. По-сложни проверки

В настоящата глава ще разгледаме вложените проверки в езика C#, чрез които нашата програма може да съдържа условни конструкци, в които има вложени други условни конструкции. Наричаме ги вложени, защото поставяме if конструкция в друга if конструкция. Ще разгледаме по-сложни логически условия с подходящи примери.

## Видео

<div class="video-player">
  Гледайте видео-урок по тази глава тук: <a target="_blank"
  href="https://www.youtube.com/watch?v=z8XxYIyesz0">
  https://www.youtube.com/watch?v=z8XxYIyesz0</a>.
</div>
<script src="/assets/js/video.js"></script>

## Вложени проверки

Конструкциите if-else могат да се влагат една в друга:

```csharp
if (condition1)
{
   if (condition2)
      Console.WriteLine("condition2 valid");
   else
      Console.WriteLine("condition2 not valid");
   Console.WriteLine("condition1 valid");
}
```

### Пример: Обръщение според възраст и пол

Според въведени възраст и пол (m / f) да се отпечата обръщение:
“Mr.” – мъж (пол “m”) на 16 или повече години
“Master” – момче (пол “m”) под 16 години
“Ms.” – жена (пол “f”) на 16 или повече години
“Miss” – момиче (пол “f”) под 16 години

| Вход | Изход | Вход | Изход | Вход | Изход |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2<br>10<br>20 | 30 | 3<br>-10<br>-20<br>-30 | -60 | 4<br>45<br>-20<br>7<br>11<br> | 43 |


Първото нещо, което забелязваме, е, че изходът на програмата зависи от няколко неща. Първо трябва да проверим какъв пол е въведен и после да проверим възрастта. Съответно ще използваме повече от 1  if-else блока. Тези блокове ще бъдат вложени. Т.е от резултата на първия ще определим кои от другите да изпълним.

![task1](/assets/chapter-4-images/missOrMaster.png)

Решение на задачата:
```cs
var age = double.Parse(Console.ReadLine());
var gender = Console.ReadLine();
if (age < 16)
{
   if (gender == "m") Console.WriteLine("Master");
   else if (gender == "f") Console.WriteLine("Miss");
}
else
{
   if (gender == "m") Console.WriteLine("Mr.");
   else if (gender == "f") Console.WriteLine("Ms.");
}
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#0


### Пример: Квартално магазинче

Предприемчив българин отваря по едно квартално магазинче в няколко града с различни цени за следните продукта:

![shop](/assets/chapter-4-images/shop.png)

По даден град, продукт и количество да се пресметне цената. Примери:


<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">coffe<br />Varna 
2</td>

<td style="border:1px solid black;">0.9<br /></td>
</tr>
</tbody>
</table>
</div>

Решение: квартално магазинче

```cs
var product = Console.ReadLine().ToLower();
var town = Console.ReadLine().ToLower();
var quantity = double.Parse(Console.ReadLine());
if (town == "sofia")
{
   if (product == "coffee") 
      Console.WriteLine(0.50 * quantity);
  // TODO: finish this …
}
if (town == "varna") // TODO: finish this …
if (town == "plovdiv") // TODO: finish this …
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#1


## По-сложни проверки

Нека разгледаме как можем да правим по-сложни логически проверки, ако се наложи. Може да използваме логическо "и", логическо "или", логическо отрицание и скоби...


## Логическо "И"

Както видяхме в някои задачи се налага да правим много проверки наведнъж. Но какво става, когато за да изпълним някакъв код, трябва да изпълнени повече условия и не искаме да правим отрицание(else) за всяко едно от тях. Вариантът с вложените if-блокове важи, но кодът би изглеждал много неподреден и със сигурност и труден за поддръжка.  

Логическо "И" (оператор &&) означава няколко условия да са изпълнени едновременно

if (x >= x1 && x <= x2 && y >= y1 && y <= y2) …

<table>
<tr>
<th>a</th> <th>b</th> <th>a && b </th>
</tr>
<tr>
<td>True</td><td align="center"> True </td><td rowspan="1"> True</td>
</tr>
<tr>
<td>True</td><td align="center"> False </td><td rowspan="1"> False</td>
</tr>
<tr>
<td>False</td><td align="center"> True </td><td rowspan="1"> False</td>
</tr>
<tr>
<td>False</td><td align="center"> False </td><td rowspan="1"> False</td>
</tr>
</table>


### Как работи оператора && ?


Операторът && приема два булеви израза (които имат стойност true или false) и ни връща 1 булев израз като резултат. Ползвайки го вместо редица вложени if блокове, прави кода по-четлив, подреден и лесен за поддръжка.Но как работи, когато поставим няколко условия едно след друго? Както видяхме горе Логическото "И" връща true, само когато приема като аргументи изрази със стойност true. Съответно, когато имаме последователност  от аргументи, логическото "И" проверява или докато свършват аргументите, или докато не срещне аргумент със стойност false. Пример:
```cs
bool a = true;
bool b = true;
bool c = false;
bool d = true;
bool result = a&&b&&c&&d; ///false (като d не се проверява)
```
Програмата ще се изпълни по следния начин: Започва проверката от <b>а</b>, отчита го като истина и проверява <b>b</b>. След като е отчело, че <b>a</b> и <b>b</b> е истина, проверява следващия аргумент. Стига до <b>c</b> и веднага вижда, че то има стойност false. Аргумента <b>c</b> бъдейки false, целия израз бива изчислен до стойност false, независимо от стойността на <b>d</b>. За това проверката на <b>d</b> се прескача и целия израз бива изчислен до стойност false.

### Точка в правоъгълник
Пример: проверка дали точка {x, y} се намира вътре в правоъгълника {x1, y1} – {x2, y2}

![shop](/assets/chapter-4-images/PointInRect.png)

Необходимо е точката {x, y} да е:
надясно от x1 и наляво от x2 и
надолу от y1 и нагоре от y2

Точка е вътрешна за даден правоъгълник, ако е:
надясно от лявата му страна, наляво то дясната му страна, надолу от горната му страна и нагоре от долната му страна
```cs
var x = 8, y = -1;
var x1 = 2, y1 = -3;
var x2 = 12, y2 = 3;
if (x >= x1 && x <= x2 && y >= y1 && y <= y2)
   Console.WriteLine("Inside");
else
   Console.WriteLine("Outside");
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#2


## Логическо "ИЛИ"

Логическо "ИЛИ" (оператор ||) означава да е изпълнено поне едно измежду няколко условия.
Подобно на оператора &&, логическото "ИЛИ" приема 2 аргумента от булев тип и ни връща true или false. Лесно можем да се досетим, че получаваме като стойност true, винаги когато един от аргументите е true. Типичен  пример в логиката за този оператор е следния:

"В училище учителят казва : 'Иван или Петър да измият дъската'. За да бъде изпълнено това, което казва учителя, е възможно само Иван да измие дъската, само Петър или и двамата да го направят."


<table>
<tr>
<th>a</th> <th>b</th> <th>a || b </th>
</tr>
<tr>
<td>True</td><td align="center"> True </td><td rowspan="1"> True</td>
</tr>
<tr>
<td>True</td><td align="center"> False </td><td rowspan="1"> True</td>
</tr>
<tr>
<td>False</td><td align="center"> True </td><td rowspan="1"> True</td>
</tr>
<tr>
<td>False</td><td align="center"> False </td><td rowspan="1"> False</td>
</tr>
</table>


### Как работи оператора || ?


Разбрахме вече какво представлява логическото "ИЛИ". Но как всъщност е реализиран? Като при логическото "И" програмата проверява от ляво на дясно аргументите, които са изредени.Понеже за да получим true от израза е необходимо един единствен аргумент да има стойност true, проверката продължава докато се срещне аргумент с тази стойност или докато не свършат аргументите.
 ```cs
bool a = false;
bool b = true;
bool c = false;
bool d = true;
bool result = a||b||c||d; ///true (като c и d не се проверяват)
```
Проверява се <b>а</b>, отчита се, че има стойност false и се продължава. Стигайки до <b>b</b>, се отчита, че има стойност true и целия израз получава стойност true, без да се проверават <b>c</b> и <b>d</b>, защото техните стойности не биха променили резултата от израза.
 


```cs
if (s == "banana" || s == "apple" || s == "kiwi")
  Console.WriteLine("fruit");
```
### Задача: плод или зеленчук?
Плодовете "fruit" са: banana, apple, kiwi, cherry, lemon, grapes
Зеленчуците "vegetable" са: tomato, cucumber, pepper, carrot
Всички останали са "unknown"

<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">banana<br /></td>
<td style="border:1px solid black;">fruit<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">tomato <br /></td>
<td style="border:1px solid black;">vegetable<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">java <br /></td>
<td style="border:1px solid black;">unknown<br /></td>
</tr>
</tbody>
</table>
</div>

Решение на задачата "плод или зеленчук":


```cs
var s = Console.ReadLine();
if (s == "banana" || s == "apple" || s == "kiwi" ||
    s == "cherry" || s == "lemon" || s == "grapes")
  Console.WriteLine("fruit");
else if (s == "tomato" || s == "cucumber" ||    s == "pepper" || s == "carrot")
  Console.WriteLine("vegetable");
else
  Console.WriteLine("unknown");
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#3


## Логическо отрицание

Логическо отрицание (оператор !) означава да не е изпълнено дадено условиe

<table>
<tr>
<th>a</th> <th>!a</th>
</tr>
<tr>
<td>True</td><td rowspan="1"> False</td>
</tr>
<tr>
<td>False</td><td rowspan="1"> True</td>
</tr>
</table>
Операторът ! приема като аргумент булева променлива и обръща стойността и.

### Пример:
Дадено число е валидно, ако е в диапазона [100…200] или е 0
Да се направи проверка за невалидно число
```cs
var inRange = (num >= 100 && num <= 200) || num == 0;
if (!inRange)
  Console.WriteLine("invalid");
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#4

## По-сложни логически условия


### Пример: Точка върху страна на правоъгълник

Да се напише програма, която чете 6 десетични числа x1, y1, x2, y2, x и y
Печата дали точката е върху страна от правоъгълника или не.

Ограничения: x1 < x2 и y1 < y2

![rect](/assets/chapter-4-images/pointOnSideRect.png)


<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">2 -3 12 3 12 -1 <br /></td>
<td style="border:1px solid black;">Border<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">2 -3 12 3 8 -1 <br /></td>
<td style="border:1px solid black;">Inside/Outside<br /></td>
</tr>
</tbody>
</table>
</div>



Точка лежи върху някоя от страните на правоъгълник, ако:
x съвпада с x1 или x2 и същевременно y е между y1 и y2 или
y съвпада с y1 или y2 и същевременно x е между x1 и x2

```cs
if (((x == x1 || x == x2) && 
     (y >= y1) && (y <= y2)) ||
    ((y == y1 || y == y2) && 
     (x >= x1) && (x <= x2)))
{
   Console.WriteLine("Border");
}
```
Предходното условие може да се опрости ето така:
```cs
var onLeftSide = (x == x1) && (y >= y1) && (y <= y2);
var onRightSide = (x == x2) && (y >= y1) && (y <= y2);
var onUpSide = (y == y1) && (x >= x1) && (x <= x2);
var onDownSide = (y == y2) && (x >= x1) && (x <= x2);
if (onLeftSide || onRightSide ||     onUpSide || onDownSide)
{
    Console.WriteLine("Border");
}
```

Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#5

### Пример: Магазин за плодове

Магазин за плодове в работни дни продава на следните цени:

![fruit1](/assets/chapter-4-images/fruitShop.png)


В почивни дни цените са по-високи:

![fruit2](/assets/chapter-4-images/fruitShop2.png)

Примерен вход и изход:

<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">apple <br />Thuesday  2</td>
<td style="border:1px solid black;">2.4<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">orange <br />Sunday  3</td>
<td style="border:1px solid black;">2.7<br /></td>
</tr>
</tbody>
</table>
</div>

Решение на задачата:
```cs
if (day == "saturday" || day == "sunday")
{
   if (fruit == "banana") price = 2.70;
   else if (fruit == "apple") price = 1.25;
   // TODO: more fruits come here …
}
else if (day == "monday" || day == "tuesday" || day ==
   "wednesday" || day == "thursday" || day == "friday")
{
   if (fruit == "banana") price = 2.50;
   // TODO: more fruits come here …
}
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#6

### Пример: Търговски комисионни

Фирма дава следните комисионни на търговците си според града, в който работят и обема на продажбите s:

![Comssions](/assets/chapter-4-images/Comissions.png)

Напишете програма, която по град и обемна продажбите изчислява комисионната
Резултатът да се изведе закръглен с 2 десетични цифри


<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">Plovdiv <br />499.99</td>
<td style="border:1px solid black;">27.5<br /></td>
</tr>
</tbody>
</table>
</div>


```cs
var comission = -1.0;
if (town == "sofia")
{
  if (0 <= sales && sales <= 500) comission = 0.05;
  else if (500 < sales && sales <= 1000) comission = 0.07;
  // TODO: check the other price ranges …
}
else if (town == "varna") // TODO: check the price ranges …
else if (town == "plovdiv") // TODO: check the price ranges …
if (comission >= 0)
  Console.WriteLine("{0:f2}", sales * comission);
else Console.WriteLine("error");
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#7

## Условна конструкция switch-case

Switch-case работи като поредица if-else-if-else
Когато работата на програмата ни зависи от стойността на една променлива, можем, вместо да правим последователности от if-else блокове, да използваме условната конструкция switch. Тя се използва за избор измежду списък с възможности. Конструкцията сравнява дадена стойност с определени константи и в зависимост от резултата предприема действие.


Пример: Принтирайте деня от седмицата (на английски) според въведеното число (1…7)
```cs
int day = int.Parse(Console.ReadLine());
switch (day)
{
  case 1: Console.WriteLine("Monday"); break;
  case 2: Console.WriteLine("Tuesday"); break;
  …
  case 7: Console.WriteLine("Sunday"); break;
  default: Console.WriteLine("Error!"); break;
}
```
Променливата, която искаме да сравняваме, поставяме в скобите след switch. Тука типът трябва да е сравним (числа,стрингове,булеви изрази). Последователно започва сравняването с всички стойности, които се намират в 'case'. При съвпадение започва изпълнението на кода от съответното място и продължава, докато стигне оператора "break". В някои програмни езици (като C и C++) "break" може да се изпускан съответно да се изпълнява код от друг 'case', докато не стигне до оператора.В C# обаче, 'break' е задължителен за всеки 'case'.
При липса на съвпадение, се изпълнява default конструкцията, когато такава съществува.


В C# имаме възможността да използваме множество 'case'-ве, когато те трябва да изпълняват един и същи код. При този начин на записване, когато намерим съвпадение, тъй като след съответния case етикет липсва код за изпълнение и break оператор, ще се изпълни следващия срещнат код. Ако такъв липсва ще се изпълни default конструкцията.
```cs
int number = 6;
switch (number)
{
 int day = int.Parse(Console.ReadLine());
switch (day)
{
  case 1:
  case 2:
  case 3:
  case 4:
  case 5:
  case 6:
  case 7:Console.WriteLine("Valid day!");break;
  
  default: Console.WriteLine("Error!"); break;
}
}
```
<table><tr><td><img src="/assets/alert-icon.png" style="max-width:50px" /></td>
<td>Добра практика е първо място да поставяме онези case случаи, които обработват най-често случилите се ситуации, а case конструкциите, обработващи по-рядко възникващи ситуации да оставим в края.</td>
</tr></table>

Тестване на решението : https://judge.softuni.bg/Contests/Practice/Index/153#8

### Множество етикети в switch-case

Напишете програма, която принтира вида на животно според името му: 
* dog -> mammal; 
* crocodile, tortoise, snake -> reptile;
* others -> unknown
```cs
switch (animal)
{
  case "dog": Console.WriteLine("mammal"); break;
  case "crocodile":
  case "tortoise":
  case "snake": Console.WriteLine("reptile"); break;
  default: Console.WriteLine("unknown"); break;
}
```
Тестване на решението: https://judge.softuni.bg/Contests/Practice/Index/153#9


## Какво научихме от тази глава?

Вложени проверки:
```cs
if (condition1)
{
   if (condition2) …
   else …
}
```
По-сложни проверки с &&, ||, ! и ():
```cs
if ((x == left || x == right) && y >= top && y <= bottom)
  Console.WriteLine("Point on the left or right side.");
```

## Упражнения: по-сложни проверки


### 11. Кино

В една кинозала столовете са наредени в правоъгълна форма в r реда и c колони. Има три вида прожекции с билети на различни цени:
* Premiere – премиерна прожекция, на цена 12.00 лева.
* Normal – стандартна прожекция, на цена 7.50 лева.
* Discount – прожекция за деца, ученици и студенти на намалена цена от 5.00 лева.

Напишете програма, която въвежда тип прожекция (стринг), брой редове и брой колони в залата (цели числа) и изчислява общите приходи от билети при пълна зала. Резултатът да се отпечата във формат като в примерите по-долу, с 2 знака след десетичната точка.

<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">Premiere<br />100 12</td>
<td style="border:1px solid black;">1440.00<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">Normal <br />21 13</td>
<td style="border:1px solid black;">2047.50<br /></td>
</tr>
</tbody>
</table>
</div>

### 12. Волейбол

Влади е студент, живее в София и си ходи от време на време до родния град. Той е много запален по волейбола, но е зает през работните дни и играе волейбол само през уикендите и в празничните дни. Влади играе в София всяка събота, когато не е на работа и не си пътува до родния град, както и в 2/3 от празничните дни. Той пътува до родния си град h пъти в годината, където играе волейбол със старите си приятели в неделя. Влади не е на работа 3/4 от уикендите, в които е в София. Отделно, през високосните години Влади играе с 15% повече волейбол от нормалното. Приемаме, че годината има точно 48 уикенда, подходящи за волейбол. Напишете програма, която изчислява колко пъти Влади е играл волейбол през годината. Закръглете резултата надолу до най-близкото цяло число (например 2.15 -> 2; 9.95 -> 9).

Входните данни се четат от конзолата:

* Първият ред съдържа думата “leap” (високосна година) или “normal” (невисокосна).
* Вторият ред съдържа цялото число p – брой празници в годината (които не са събота и неделя).
* Третият ред съдържа цялото число h – брой уикенди, в които Влади си пътува до родния град.

<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">leap <br />5 2</td>
<td style="border:1px solid black;">45<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">normal <br />3 2</td>
<td style="border:1px solid black;">38<br /></td>
</tr>
</tbody>
</table>
</div>


### 13. * Точка във фигурата
Фигура се състои от 6 блокчета с размер h * h, разположени като на фигурата вдясно. Долният ляв ъгъл на сградата е на позиция {0, 0}. Горният десен ъгъл на фигурата е на позиция {2*h, 4*h}. На фигурата координатите са дадени при h = 2. Напишете програма, която въвежда цяло число h и координатите на дадена точка {x, y} (цели числа) и отпечатва дали точката е вътре във фигурата (inside), вън от фигурата (outside) или на някоя от стените на фигурата (border).

<div style="display:inline-block">
<table>
<thead>
<tr style="background-color:#d9d9d9;">
<th style="border:1px solid black;background-color:#d9d9d9;">Вход</th>
<th style="border:1px solid black;background-color:#d9d9d9;">Изход</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td style="border:1px solid black;">2 3 10 <br /></td>
<td style="border:1px solid black;">outside<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">2 3 1 <br ></td>
<td style="border:1px solid black;">inside<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">2 2 2 <br ></td>
<td style="border:1px solid black;">border<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">2 6 0<br ></td>
<td style="border:1px solid black;">border<br /></td>
</tr>
<tr>
<td style="border:1px solid black;">2 0 6 <br ></td>
<td style="border:1px solid black;">outside<br /></td>
</tr>
</tbody>
</table>
</div>

![PointInFigure](/assets/chapter-4-images/pointInFigure.png)


* Може да разделите фигурата на два правоъгълника с обща стена.
* Една точка е външна (outside) за фигурата, когато е едновременно извън двата правоъгълника.
* Една точка е вътрешна (inside) за фигурата, ако е вътре в някой от правоъгълниците (изключвайки стените им) или лежи върху общата им стена.
* В противен случай точката лежи на стената на правоъгълника (border).

## Упражнения: графични и уеб приложения

### 14. * Точка и правоъгълник – графично (GUI) приложение
Да се разработи графично (GUI) приложение за визуализация на точка и правоъгълник. Приложението трябва да изглежда приблизително по следния начин:

![PointAndFigure](/assets/chapter-4-images/PointAndRect1.png)
![PointAndFigure](/assets/chapter-4-images/PointAndRect2.png)
![PointAndFigure](/assets/chapter-4-images/PointAndRect3.png)

От контролите вляво се задават координатите на два от ъглите на правоъгълник (десетични числа) и координатите на точка. Приложението визуализира графично правоъгълника и точката и изписва дали точката е вътре в правоъгълника (Inside), вън от него (Outside) или на някоя от стените му (Border).
Приложението премества и мащабира координатите на правоъгълника и точката, за да бъдат максимално големи, но да се събират в полето за визуализация в дясната страна на приложението.

<table><tr><td><img src="/assets/alert-icon.png" style="max-width:50px" /></td>
<td>Внимание: това приложение е значително по-сложно от предходните графични приложения, които разработвахте до сега, защото изисква ползване на функции за чертане и нетривиални изчисления за преоразмеряване и преместване на правоъгълника и точката. Следват инструкции за изграждане на приложението стъпка по стъпка.</td>
</tr></table>

* Създайте нов Windows Forms Application с подходящо име, например “Point-and-Rectangle”:

![PointAndFigure](/assets/chapter-4-images/PointAndRect4.png)

*  Наредете контролите във формата както е показано на фигурата по-долу: 6 кутийки за въвеждане на число (NumericUpDown) с надписи (Label) пред всяка от тях, бутон (Button) за изчертаване на правоъгълника и точката и текстов блок за резултата (Label). Нагласете размерите и свойствата на контролите, за да изглеждат долу-горе като на картинката:
![PointAndFigure](/assets/chapter-4-images/PointAndRect5.png)

* Задайте следните препоръчителни настройки на контролите:

За главната форма (Form), която съдържа всички контроли:

*	(name) = FormPointAndRectangle
*	Text = "Point and Rectangle"
*	Font.Size = 12
*	Size = 700, 410
*	MinimumSize = 500, 400
*	FormBorderStyle = FixedSingle

За полетата за въвеждане на число (NumericUpDown):

*	(name) = numericUpDownX1; numericUpDownY1; numericUpDownX2; numericUpDownY2; numericUpDownX; numericUpDownY
*	Value = 2; -3; 12; 3; 8; -1
*	Minimum = -100000
*	Maximum = 100000
*	DecimalPlaces = 2

За бутона (Button) за визуализация на правоъгълника и точката:

*	(name) = buttonDraw
*	Text = “Draw” 

За текстовия блок за резултата (Label):

*	(name) = labelLocation
*	AutoSize = False
*	BackColor = PaleGreen
*	TextAlign = MiddleCenter


За полето с чертежа (PictureBox):

*	(name) = pictureBox
*	Anchor = Top, Bottom, Left, Right
*	Хванете следните събития, за да напишете C# кода, който ще се изпълни при настъпването им:
*	Събитието Click на бутона buttonDraw (извиква се при натискане на бутона).
*	Събитието ValueChanged на контролите за въвеждане на числа numericUpDownX1, numericUpDownY1, numericUpDownX2, numericUpDownY2, numericUpDownX и numericUpDownY (извиква се при промяна на стойността в контролата за въвеждане на число).
*	Събитието Load на формата FormPointAndRectangle (извиква се при стартиране на приложението, преди да се появи главната форма на екрана).
*	Събитието Resize на формата FormPointAndRectangle (извиква се при промяна на размера на главната формата).
*	Всички изброени по-горе събития ще изпълняват едно и също действие – Draw(), което ще визуализира правоъгълника и точката и ще показва дали тя е вътре, вън или на някоя от страните. Кодът трябва да прилича на този: 

```cs
private void buttonDraw_Click(object sender, EventArgs e)
{
    Draw();
}

private void FormPointAndRectangle_Load(object sender, EventArgs e)
{
    Draw();
}

private void FormPointAndRectangle_Resize(object sender, EventArgs e)
{
    Draw();
}

private void numericUpDownX1_ValueChanged(object sender, EventArgs e)
{
    Draw();
}

// TODO: implement the same way event handlers numericUpDownY1_ValueChanged, numericUpDownX2_ValueChanged, numericUpDownY2_ValueChanged, numericUpDownX_ValueChanged and numericUpDownY_ValueChanged

private void Draw()
{
    // TODO: implement this a bit later …
}

```

* 	Започнете от по-лесната част: печат на информация къде е точката спрямо правоъгълника (Inside, Outside или Border). Можете да ползвате следния код:

```cs
private void Draw()
{
    // Get the rectangle and point coordinates from the form
    var x1 = this.numericUpDownX1.Value;
    var y1 = this.numericUpDownY1.Value;
    var x2 = this.numericUpDownX2.Value;
    var y2 = this.numericUpDownY2.Value;
    var x = this.numericUpDownX.Value;
    var y = this.numericUpDownY.Value;

    // Display the location of the point: Inside / Border / Outside
    DisplayPointLocation(x1, y1, x2, y2, x, y);
}

private void DisplayPointLocation(
    decimal x1, decimal y1, decimal x2, decimal y2, decimal x, decimal y)
{
    var left = Math.Min(x1, x2);
    var right = Math.Max(x1, x2);
    var top = Math.Min(y1, y2);
    var bottom = Math.Max(y1, y2);
    if (x > left && x < right && …)
    {
        this.labelLocation.Text = "Inside";
        this.labelLocation.BackColor = Color.LightGreen;
    }
    else if (… || y < top || y > bottom)
    {
        this.labelLocation.Text = "Outside";
        this.labelLocation.BackColor = Color.LightSalmon;
    }
    else
    {
        this.labelLocation.Text = "Border";
        this.labelLocation.BackColor = Color.Gold;
    }
}
```

Помислете как да допишете недовършените (нарочно) условия в if-проверките! Кодът по-горе нарочно не се компилира, защото целта му е да помислите как и защо работи и да допишете липсващите части.
Горният код взима координатите на правоъгълника и точките и проверява дали точката е вътре, вън или на страната на правоъгълника. При визуализацията на резултата се сменя и цвета на фона на текстовия блок, който го съдържа.
*	Остава да се имплементира най-сложната част: визуализация на правоъгълника и точката в контролата pictureBox с преоразмеряване. Можете да ползвате кода по-долу, който прави малко изчисления и рисува син правоъгълник и тъмносиньо кръгче (точката) според зададените във формата координати. За съжаление сложността на кода надхвърля изучавания до момента материал и е сложно да се обясни в детайли как точно работи. Можете да разгледате коментарите за ориентация. Това е пълната версия на действието Draw():
```cs
private void Draw()
{
  // Get the rectangle and point coordinates from the form
  var x1 = this.numericUpDownX1.Value;
  var y1 = this.numericUpDownY1.Value;
  var x2 = this.numericUpDownX2.Value;
  var y2 = this.numericUpDownY2.Value;
  var x = this.numericUpDownX.Value;
  var y = this.numericUpDownY.Value;

  // Display the location of the point: Inside / Border / Outside
  DisplayPointLocation(x1, y1, x2, y2, x, y);

  // Calculate the scale factor (ratio) for the diagram holding the
  // rectangle and point in order to fit them well in the picture box
  var minX = Min(x1, x2, x);
  var maxX = Max(x1, x2, x);
  var minY = Min(y1, y2, y);
  var maxY = Max(y1, y2, y);
  var diagramWidth = maxX - minX;
  var diagramHeight = maxY - minY;
  var ratio = 1.0m;
  var offset = 10;
  if (diagramWidth != 0 && diagramHeight != 0)
  {
    var ratioX = (pictureBox.Width - 2 * offset - 1) / diagramWidth;
    var ratioY = (pictureBox.Height - 2 * offset - 1) / diagramHeight;
    ratio = Math.Min(ratioX, ratioY);
  }

  // Calculate the scaled rectangle coordinates
  var rectLeft = offset + (int)Math.Round((Math.Min(x1, x2) - minX) * ratio);
  var rectTop = offset + (int)Math.Round((Math.Min(y1, y2) - minY) * ratio);
  var rectWidth = (int)Math.Round(Math.Abs(x2 - x1) * ratio);
  var rectHeight = (int)Math.Round(Math.Abs(y2 - y1) * ratio);
  var rect = new Rectangle(rectLeft, rectTop, rectWidth, rectHeight);

  // Calculate the scalled point coordinates
  var pointX = (int)Math.Round(offset + (x - minX) * ratio);
  var pointY = (int)Math.Round(offset + (y - minY) * ratio);
  var pointRect = new Rectangle(pointX - 2, pointY - 2, 5, 5);

  // Draw the rectangle and point
  pictureBox.Image = new Bitmap(pictureBox.Width, pictureBox.Height);
  using (var g = Graphics.FromImage(pictureBox.Image))
  {
    // Draw diagram background (white area)
    g.Clear(Color.White);

    // Draw the rectangle (scalled to the picture box size)
    var pen = new Pen(Color.Blue, 3);
    g.DrawRectangle(pen, rect);

    // Draw the point (scalled to the picture box size)
    pen = new Pen(Color.DarkBlue, 5);
    g.DrawEllipse(pen, pointRect);
  }
}

private decimal Min(decimal val1, decimal val2, decimal val3)
{
  return Math.Min(val1, Math.Min(val2, val3));
}

private decimal Max(decimal val1, decimal val2, decimal val3)
{
  return Math.Max(val1, Math.Max(val2, val3));
}
```
В горния код се срещат доста преобразувания на типове, защото се работи с различни типове числа (десетини числа, реални числа и цели числа) и понякога се изисква да се преминава между тях.
* Компилирайте кода. Ако има някакви грешки, ги отстранете. Най-вероятната причина за грешка е несъответстващо име на някоя от контролите или ако сте написали кода на неправилно място.
*	Стартирайте приложението и го тествайте (с разцъкване). Пробвайте да въвеждате различни правоъгълници и позиционирайте точката на различни позиции, преоразмерявайте приложението и вижте дали се държи коректно.

TODO: да се ползва като основа файла "4. Complex-Conditions-Exercises.docx".
