# Помощь пользователям быстрее проходить проверку с автозаполнителем

Люди ненавидят заполнять веб формы, особенно на мобильных устройствах. Они 
могут быть долгими и разочаровывающими и часто содержат несколько страниц шагов и проверок. Это приводит к негативному осадку у пользователя и его большому разочарованию. Чтобы упросить эти вещи для пользователей, браузеры уже давно имеют механизм автозаполнения полей от имени пользователя. Хром принял это шаг в далеком 2011 году путем введения [Автозаполнения][1], которое заполняет форму целиком, основываясь на профиле пользователя.

Начиная с следующей версии Chrome (M43), мы делаем еще один шаг, помогая пользователям заполнять формы быстрее, расширяем нашу поддержку для кредитных карт и адресов в Google. Это означает, что одну и ту же информацию пользователи используют и при покупке вещей внутри Google Play магазина, и на сайтах, которые они посещают. Используя стандартные атрибуты *автозаполнения*, вы можете убедиться в лояльности ваших пользователей, помогая Chrome автозаполнять ваши пароли в формы с 100% точностью.

Атрибуты автозаполнения — это способ для тебя, разработчик, контролировать, как браузер должен заполнить данное поле формы. Например, если вы ожидаете от пользователя который укажет `Улицу` вы можете подсказать браузеру, что вы ожидали его с помощью `autocomplete="address-line1"`. Это предотвращает браузер от неправильно угадывания поля формы на вашем сайте, что может привести к плохому опыту пользователя.

Мы обнаружили, что, правильно используя атрибуты автозаполнения в формах, пользователи заполняют их до 30% быстрее. А так как автозаполнение является частью [WHATWG HTML][2] стандарта, мы надеемся, что другие браузеры будут поддерживать его в ближайшем будущем.

![автозаполнение показавает силу быстрого и легкого заполнения формы][3]

В прошлом, большинство разработчиков добавляли *autocomplete="off"* в свои поля форм, чтобы предотвратить браузер от любой функциональности автозаполнения. В то время как Chrome по-прежнему принимает этот тег для автозаполнения, он не будет принимать его данных автозаполнения. Когда же следует использовать *autocomplete="off"*? Один из примеров - когда вы реализовали свою собственную версию автозаполнения для поиска. Другим примером является любая форма, на которой пользователи вводять и представляют различные виды информации, где браузеру не обязательно помнить  что было введено ранее.

Наиболее распространенные атрибуты *автозаполнения* приведены в таблице ниже и описаны в [Веб основах][4].

### Общие атрибуты

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

Атрибуты автозаполнения могут сопровождаться именем раздела, например:

*   **shipping** - имя
*   **billing** - адрес улицы

Это рекомендуется, потому что это сделает вашу разметки легче для разбора и понимания. Браузер автозаполняет различные секции отдельно, а не в виде непрерывной формы.

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

**Лучшие практики форм**

1.  **Используйте \_метки\_ на полях ввода в формах**, и убедитесь, что они отображаются, когда поле в фокусе. Метка элемента указывает пользователю, какая информация необходима для элемента формы. Каждая метка ассоциируется с элементом ввода, путем размещения его внутри метки элемента. Применение меток для элементов формы также помогает улучшить удобство ввода пользователем данных: пользователь может коснуться метки или элемента ввода, чтобы поставить фокус на элементе ввода.
   
2.  **Используйте плейсхолдеры, чтобы обеспечить руководство**, которое вы ожидали. Атрибут плейсхолдер подсказывает пользователю о том, что ожидается при вводе, как правило показывая значение светлым текстом, когда пользователь начинает набирать текст в элементе. Плейсхолдеры исчезают, как только пользователь начинает вводить в элементе. Таким образом, они не являются заменой для меток. Они должны быть использованы в качестве помощи, чтобы сориентировать пользователей на требуемом формате и содержании.

### Демо

Вы можете увидеть это в действии по адресу: 
[greenido.github.io/Product-Site-101/form-cc-example.html][5]  
Или посмотреть код: <https://github.com/greenido/Product-Site-101>

![Пример формы, ипользующей автозаполнения тегов][6]

 [1]: https://support.google.com/chrome/answer/142893?hl=en
 [2]: https://html.spec.whatwg.org/multipage/forms.html#autofill
 [3]: img/autofill-1-0269161300058bacff11479cd8ef2a3c.gif
 [4]: https://developers.google.com/web/fundamentals/input/?hl=en
 [5]: https://greenido.github.io/Product-Site-101/form-cc-example.html
 [6]: img/autofill-ex-2a8bc613079b80e48c6ef42558c69d57.png