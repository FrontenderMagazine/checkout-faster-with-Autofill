# Ускоряем проверку форм с помощью автозаполнения

Люди ненавидят заполнять формы, особенно на мобильных устройствах. Формы 
могут быть длинными и пугающими, и часто содержат большое количество шагов и
проверок, а их заполнение может вызывать у пользователя раздражение и
разочарование. Чтобы облегчить этот процесс, браузеры 
уже довольно давно внедрили механизм автозаполнения полей от имени 
пользователя. Хром сделал это 2011 году представив [Автозаполнение][1], которое
может заполнить форму целиком, используя данные, которы пользователь уже вводил ранее.

В следующей версии Хрома (M43) мы сделаем еще один шаг, который поможет
пользователям заполнять формы быстрее: мы расширим поддержку данных с кредитных
карт и адресов в Google. Это означает, что одни и те же данные можно будет
использовать и для покупок в Google Play, и на внешних сайтах. 
Используйте стандартные атрибуты *автозаполнения* и вы можете быть уверены, 
что вашим пользователям будет удобно, благодаря тому, что автозаполнение 
Хрома сможет со стопроцентной точностью заполнить поля форм на вашем сайте.

Атрибуты автозаполнения — это способ для вас как для разработчика управлять тем,
как именно браузер должен заполнить конкретное поле. Например, если вы ожидаете,
что пользователь введёт название улицы, с помощью `autocomplete="address-line1"`
вы можете подсказать браузеру какие именно данные вы ожидаете. 
Это помешает браузеру неверно заполнять полей форм, что было бы неудобно для пользователя.

Мы обнаружили, что при правильном использовании атрибутов автозаполнения 
в формах, пользователи заполняют их примерно на 30% быстрее. А так как
автозаполнение является частью [WHATWG HTML][2] стандарта, мы надеемся, что
другие браузеры начнут поддерживать его в ближайшем будущем.

![легкое и быстрое заполнение формы с помощью автозаполнения][3]

В прошлом многие разработчики добавляли `autocomplete="off"` в поля форм,
чтобы запретить браузеру любые действия, связанные с автозаполнением. 
В то время как Хром по-прежнему использует этот атрибут для *автодополнения*, 
он не будет использовать его для *автозаполнения*. Когда же следует использовать `autocomplete="off"`? Например, если вы сделали свою собственную версию автодополнения для поиска. Или формы, в которые пользователи вводят различные данные, которые браузеру помнить не обязательно.

Наиболее распространенные атрибуты *автозаполнения* приведены в таблице ниже и описаны в [Веб основах][4].

### Основные атрибуты

| **Название атрибута** | **Автозаполнение атрибута** |
| --------------------- | --------------------------- |
| ccname | cc-name |
| cardnumber | cc-number |
| cvc | cc-csc |
| ccmonth | cc-exp-month |
| ccyear | cc-exp-year |
| exp-date | cc-exp |
| card-type | cc-type |


```javascript
<label for="frmNameCC">Name on card</label>
<input name="ccname" id="frmNameCC" required placeholder="Full Name" autocomplete="cc-name">

<label for="frmCCNum">Card Number</label>
<input name="cardnumber" id="frmCCNum" required autocomplete="cc-number">    

<label for="frmCCCVC">CVC</label>
<input name="cvc" id="frmCCCVC" required autocomplete="cc-csc"> 
  
<label for="frmCCExp">Expiry</label>
<input name="cc-exp" id="frmCCExp" required placeholder="MM-YYYY" autocomplete="cc-exp">
```

#### Имя

| **Название атрибута** | **Автозаполнение атрибута** |
| --------------------- | --------------------------- |
| name | name (full name) |
| fname | given-name (first name) |
| mname | additional-name (middle name) |
| lname | family-name (last name) |

```javascript
<label for="frmNameA">Name</label>
<input name="name" id="frmNameA" placeholder="Full name" required autocomplete="name">
```

#### Почта

| **Название атрибута** | **Автозаполнение атрибута** |
| --------------------- | --------------------------- |
| email | email |

```javascript
<label for="frmEmailA">Email</label>
<input type="email" name="email" id="frmEmailA" placeholder="name@example.com" required autocomplete="email">

<label for="frmEmailC">Confirm Email</label>
<input type="email" name="emailC" id="frmEmailC" placeholder="name@example.com" required autocomplete="email">
```

#### Адрес

| **Название атрибута** | **Автозаполнение атрибута** |
| --------------------- | --------------------------- |
| address | For one address input: street-address |
| city | For two address inputs: address-line1 , address-line2 |
| region | address-level1 (state or province) |
| province | address-level2 (city) |
| state | postal-code (zip code) |
| zip | country |
| zip2 |  |
| postal |  |
| postal |  |

```javascript
<label for="frmAddressS">Address</label>
<input name="ship-address" required id="frmAddressS" placeholder="123 Any Street" autocomplete="shipping street-address">

<label for="frmCityS">City</label>
<input name="ship-city" required id="frmCityS" placeholder="New York" autocomplete="shipping address-level2">

<label for="frmStateS">State</label>
<input name="ship-state" required id="frmStateS" placeholder="NY" autocomplete="shipping address-level1">

<label for="frmZipS">Zip</label>
<input name="ship-zip" required id="frmZipS" placeholder="10011" autocomplete="shipping postal-code">

<label for="frmCountryS">Country</label>
<input name="ship-country" required id="frmCountryS" placeholder="USA" autocomplete="shipping country">
```

#### Телефон

| **Название атрибута** | **Автозаполнение атрибута** |
| --------------------- | --------------------------- |
| phone | tel |
| mobile |  |
| country-code |  |
| area-code |  |
| exchange |  |
| suffix |  |
| ext |  |

```javascript
<label for="frmPhoneNumA">Phone</label>
<input type="tel" name="phone" id="frmPhoneNumA" placeholder="+1-650-450-1212" required autocomplete="tel">
```

Атрибуты автозаполнения могут быть дополнены именем раздела, например:

*   **shipping** - имя
*   **billing** - адрес улицы

Так рекомендуется делать, потому что это сделает вашу разметки легче для 
чтения и понимания. Браузер автоматически заполнит различные секции отдельно, а не в виде длинной формы.

#### Пример формы оплаты

```javascript
<label for="frmNameCC">Name on card</label>
<input name="ccname" id="frmNameCC" required placeholder="Full Name" autocomplete="cc-name">

<label for="frmCCNum">Card Number</label>
<input name="cardnumber" id="frmCCNum" required autocomplete="cc-number">

<label for="frmCCCVC">CVC</label>
<input name="cvc" id="frmCCCVC" required autocomplete="cc-csc">
  
<label for="frmCCExp">Expiry</label>
<input name="cc-exp" id="frmCCExp" required placeholder="MM-YYYY" autocomplete="cc-exp">
```

**Хорошие привычки при работе с формами**

1.  **Используйте лейблы для полей ввода** и убедитесь, что они отображаются,
когда поле в фокусе. Элемент `label` подсказывает пользователю какую информацию
нужно ввести в поле. Лейбл может быть связан с текстовым полем путём
размещения поля внутри лейбла. Применение лейблов для элементов формы также
позволяет удобнее вводить данные: пользователь может кликнуть как на
текстовое поле, так и на его лейбл, чтобы установить фокус на поле и начать вводить текст.
   
2.  **Используйте плейсхолдеры** как подсказки для полей ввода. Атрибут `placeholder` подсказывает пользователю какие содержимое ожидается в поле, как правило, подсказка показывается светлым текстом, пока пользователь не начинёт печатать. Плейсхолдеры исчезают, как только пользователь начинает вводить текст. Таким образом, плейсхолдеры не являются заменой для лейблов и должны быть использованы как подсказка, чтобы прояснить для пользователя ожидаемое содержимое и его формат.

### Демо

Вы можете увидеть демо в действии здесь: 
[greenido.github.io/Product-Site-101/form-cc-example.html][5]  
Или посмотреть код на этой странице: <https://github.com/greenido/Product-Site-101>

![Пример формы, ипользующей автозаполнения тегов][6]

 [1]: https://support.google.com/chrome/answer/142893?hl=en
 [2]: https://html.spec.whatwg.org/multipage/forms.html#autofill
 [3]: img/autofill-1-0269161300058bacff11479cd8ef2a3c.gif
 [4]: https://developers.google.com/web/fundamentals/input/?hl=en
 [5]: https://greenido.github.io/Product-Site-101/form-cc-example.html
 [6]: img/autofill-ex-2a8bc613079b80e48c6ef42558c69d57.png
