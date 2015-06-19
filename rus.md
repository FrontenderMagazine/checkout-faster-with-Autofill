Люди ненавидят заполнять веб формы, особенно на мобильных устройствах. Они 
могут быть долгими и разочаровывающими и часто содержат несколько страниц шагов и проверок. Это приводит к негативному осадку у пользователя и его большому разочарованию. Чтобы упросить эти вещи для пользователей, браузеры уже давно имеют механизм автозаполнения полей от имени пользователя. Хром принял это шаг в далеком 2011 году путем введения [Автозаполнения][1], которое заполняет форму целиком, основываясь на автозаполнении профиль пользователя.

Начиная с следующей версии Chrome (M43), мы делаем еще один шаг, помогая пользователям заполнять формы быстрее, расширяем нашу поддержку для кредитных карт и адресов в Google. Это означает, что одну и ту же информацию пользователи используют, при покупке вещей внутри Google Play магазина и на сайтах которые они посещают. Используя стандартные атрибуты *автозаполнения*, вы можете убедиться в счастье ваших пользователей, помогая Chrome автозаполнять ваши пароли в формы с 100% точностью.

Атрибуты автозаполнения — это способ для тебя, разработчик, контролировать, как браузер должен заполнить данное поле формы. Например, если вы ожидаете от пользователя который укажет `Улицу` вы можете подсказать браузеру, что вы ожидали его с помощью `autocomplete="address-line1"`. Это предотвращает браузер от неправильно угадывания поля формы на вашем сайте, которые могут привести к плохому опыту пользователя.

Мы обнаружили, что, правильно используя атрибуты автозаполнения в формах, пользователи заполняют их до 30% быстрее. А так как автозаполнение является частью [WHATWG HTML][2] стандарта, мы надеемся, что другие браузеры будут поддерживать его в ближайшем будущем.

![автозаполнение показавает силу быстрого и легкого заполнения формы][3]

In the past, many developers would add *autocomplete="off"* to their form
fields to prevent the browser from performing any kind of autocomplete 
functionality. While Chrome will still respect this tag for autocomplete data, it will not respect it for autofill data. So when should you use*autocomplete=”off”*? One example is when you’ve implemented your own version of autocompletefor search. Another example is any form field where users will input and submit different kinds of information where it would not be useful to have the browser remember what was submitted previously.

The most common *autocomplete* attributes are shown in the table below and are documented in[Web Fundamentals][4].

### Common Attributes


| **name attribute**                                                  | **
autocomplete attribute
**                                                   |
||
| ccname  
cardnumber  
cvc  
ccmonth  
ccyear  
exp-date  
card-type | cc-name  
cc-number  
cc-csc  
cc-exp-month  
cc-exp-year  
cc-exp  
cc-type |

    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmNameCC"</span><span class="o">></span><span class="nx">Name</span> <span class="nx">on</span> <span class="nx">card</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ccname"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmNameCC"</span> <span class="nx">required</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"Full Name"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-name"</span><span class="o">></span>    
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCCNum"</span><span class="o">></span><span class="nx">Card</span> <span class="nb">Number</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"cardnumber"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCCNum"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-number"</span><span class="o">></span>    
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCCCVC"</span><span class="o">></span><span class="nx">CVC</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"cvc"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCCCVC"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-csc"</span><span class="o">></span> 
      
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCCExp"</span><span class="o">></span><span class="nx">Expiry</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"cc-exp"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCCExp"</span> <span class="nx">required</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"MM-YYYY"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-exp"</span><span class="o">></span>

#### Name







| **name attribute**           | **autocomplete attribute
**                                                                           |
||
| name  
fname  
mname  
lname | name (full name)  
given-name (first name)  
additional-name (middle name)  
family-name (last name) |

    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmNameA"</span><span class="o">></span><span class="nx">Name</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"name"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmNameA"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"Full name"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"name"</span><span class="o">></span>

#### Email







| **name attribute** | **autocomplete attribute** |
||
| email              | email                      |

    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmEmailA"</span><span class="o">></span><span class="nx">Email</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">type</span><span class="o">=</span><span class="s2">"email"</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"email"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmEmailA"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"name@example.com"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"email"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmEmailC"</span><span class="o">></span><span class="nx">Confirm</span> <span class="nx">Email</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">type</span><span class="o">=</span><span class="s2">"email"</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"emailC"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmEmailC"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"name@example.com"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"email"</span><span class="o">></span>

#### Address


| **name attribute
**                                                         | **autocomplete 
attribute
**                                                                                                                                                                    |
||
| address  
city  
region  
province  
state  
zip  
zip2  
postal  
country | For one address input: street-address  
For two address inputs:
address-line1 , address-line2
address-level1 (state or
province
)  
address-level2 (city)  
postal-code (zip code)  
country |

    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmAddressS"</span><span class="o">></span><span class="nx">Address</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ship-address"</span> <span class="nx">required</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmAddressS"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"123 Any Street"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"shipping street-address"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCityS"</span><span class="o">></span><span class="nx">City</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ship-city"</span> <span class="nx">required</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCityS"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"New York"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"shipping locality"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmStateS"</span><span class="o">></span><span class="nx">State</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ship-state"</span> <span class="nx">required</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmStateS"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"NY"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"shipping region"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmZipS"</span><span class="o">></span><span class="nx">Zip</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ship-zip"</span> <span class="nx">required</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmZipS"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"10011"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"shipping postal-code"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCountryS"</span><span class="o">></span><span class="nx">Country</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ship-country"</span> <span class="nx">required</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCountryS"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"USA"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"shipping country"</span><span class="o">></span>

#### Phone


| **name attribute**                                                  | **
autocomplete attribute
** |
||
| phone  
mobile  
country-code  
area-code  
exchange  
suffix  
ext | tel                        |

    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmPhoneNumA"</span><span class="o">></span><span class="nx">Phone</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">type</span><span class="o">=</span><span class="s2">"tel"</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"phone"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmPhoneNumA"</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"+1-650-450-1212"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"tel"</span><span class="o">></span>

The autocomplete attributes can be accompanied with a section name, such as:

*   **shipping** - given-name
*   **billing** - street-address  
    

It is recommended because it will make your markup easier to parse and
understand. The browser will autofill different sections separately and not as a
continuous form.

    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmNameCC"</span><span class="o">></span><span class="nx">Name</span> <span class="nx">on</span> <span class="nx">card</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"ccname"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmNameCC"</span> <span class="nx">required</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"Full Name"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-name"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCCNum"</span><span class="o">></span><span class="nx">Card</span> <span class="nb">Number</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"cardnumber"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCCNum"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-number"</span><span class="o">></span>
    
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCCCVC"</span><span class="o">></span><span class="nx">CVC</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"cvc"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCCCVC"</span> <span class="nx">required</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-csc"</span><span class="o">></span>
      
    <span class="o"><</span><span class="nx">label</span> <span class="k">for</span><span class="o">=</span><span class="s2">"frmCCExp"</span><span class="o">></span><span class="nx">Expiry</span><span class="o"><</span><span class="err">/label></span>
    <span class="o"><</span><span class="nx">input</span> <span class="nx">name</span><span class="o">=</span><span class="s2">"cc-exp"</span> <span class="nx">id</span><span class="o">=</span><span class="s2">"frmCCExp"</span> <span class="nx">required</span> <span class="nx">placeholder</span><span class="o">=</span><span class="s2">"MM-YYYY"</span> <span class="nx">autocomplete</span><span class="o">=</span><span class="s2">"cc-exp"</span><span class="o">></span>

**Forms best practices**

1.  **Use \_labels\_on form inputs**, and ensure they’re visible when the
    field is in focus. The label element provides direction to the user, telling 
    them what information is needed in a form element. Each label is associated with
    an input element by placing it inside the label element. Applying labels to form
    elements also helps to improve the touch target size: the user can touch either 
    the label or the input in order to place focus on the input element.
   
2.  **Use placeholder to provide guidance** about what you expect. The
    placeholder attribute provides a hint to the user about what’s expected in the 
    input, typically by displaying the value as light text until the the user starts
    typing in the element. Placeholders disappear as soon as the user starts typing 
    in an element, thus they are not a replacement for labels. They should be used 
    as an aid to help guide users on the required format and content.
   

### Demo

You can see it in action over at: 
[greenido.github.io/Product-Site-101/form-cc-example.html][5]  
Or check the code: <https://github.com/greenido/Product-Site-101>

![An example to a form that use autocomplete tags][6]

 [1]: https://support.google.com/chrome/answer/142893?hl=en
 [2]: https://html.spec.whatwg.org/multipage/forms.html#autofill
 [3]: img/autofill-1-0269161300058bacff11479cd8ef2a3c.gif
 [4]: https://developers.google.com/web/fundamentals/input/?hl=en
 [5]: https://greenido.github.io/Product-Site-101/form-cc-example.html
 [6]: img/autofill-ex-2a8bc613079b80e48c6ef42558c69d57.png