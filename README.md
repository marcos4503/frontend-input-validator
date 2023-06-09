# Frontend Input Validator

The Frontend Input Validator is a Javascript library to be used in the Frontend of your website. The objective of this library is to provide a simple, easy to use and low code system for validating text or file inputs in your website Frontend interface. Which is very common in all types of websites, such as registration forms for example.

This library, when used in conjunction with <a href="https://github.com/marcos4503/backend-input-validator" target="_blank">Backend Input Validator</a>, provides EXTREMELY easy way to validate user/client inputs in the Frontend or Backend of your website.

# How it works?

This library works quite simply. What you must do is instantiate an object of type `InputValidator` informing the ID of an Input Field on your page and the validation parameters (such as whether to allow an empty field, maximum number of characters, special characters allowed, etc).

Once this is done, the `InputValidator` object will be linked with the Input Field and will check if the field is valid, AUTOMATICALLY, whenever the user interacts with the Field or types something in it. You can register a Callback on the instantiated `InputValidator` object to receive automatic validation of the linked Input Field. At any time, you can also easily check whether the field is valid or not.

# How to use?

First you need to clone this repository. Open the downloaded file and go to the "Frontend-Input-Validator-Source" folder then copy the "frontend-input-validator.js" file and place it somewhere on your website.

The next step is to reference the library in your HTML page so that you can use the library's code within your page's Javascript code. To do this, place the HTML code below inside the `<head>` and `</head>` tags of your page. Remember to change the `src` attribute to the path where the "frontend-input-validator.js" file is!

```html
<script type="text/javascript" src="../../folder/folder/frontend-input-validator.js"></script>
```
 
# Understand the basics before starting

When you have fields for User Input you usually expect to receive a text input (`STRING`), a number (`INT` or `FLOAT`) or a file (`FILE`). Therefore, when instantiating an object of type `InputValidator`, you need to inform the ID to target Input Field to be valided, the type of value you expect to obtain from that Input Field and, you must inform the validation parameters. See the code below as an example...

```javascript
//on HTML...
<input type="text" id="nickNameField" />

//on Javascript...
var nickNameValidation = new InputValidator("nickNameField", "STRING", { allowEmpty: false });
```

As you can see in the example code above, we have the text Field for the user to enter the Nickname. As we expect to get a text value, we inform the `STRING` type when instantiating the `InputValidator` object. But if we have an Age Field for example, we expect to get an integer numerical value, as in the example below...

```javascript
//on HTML...
<input type="number" id="ageField" />

//on Javascript...
var ageValidation = new InputValidator("ageField", "INT", { allowEmpty: false, minNumberValue: 0 });
```

These are currently the value types supported for validation by this library...

- STRING
- INT
- FLOAT
- FILE

Now let's pay attention to the validation parameters. Validation parameters work like "rules" that you define for an object of type `InputValidator`, so that it can validate the linked Input Field and say if it respects the rules, being VALID, or if it does not respect any rules, being INVALID. For example, if we want to validate a Name field, we can instantiate the `InputValidator` object as follows...

```javascript
//on HTML...
<input type="text" id="nameField" />

//on Javascript...
var nameFieldValidation = new InputValidator("nameField", "STRING", 
    { 
        allowEmpty: false,
        maxChars: 80,
        allowNumbers: false
    });
```

As you can see, the validation parameters are informed to the `InputValidator` object in a "array" format. When instantiating the `InputValidator` object above, to validate the Name field, we use the `allowEmpty` parameter to say that we don't want an empty field, the `maxChars` parameter to say that the maximum number of characters must be 80 and the `allowNumbers` parameter to say that we do not allow numbers in this field. So, the `InputValidator` object will only consider the Name Field valid if the content typed by the user respects all these parameters.

Notice that we created a validation for the Name Field easily, just using the validation parameters and so we no longer need to create that bunch of lines of Javascript code to do this validation. But ahead, you will see all validation parameters supported by this library!

Now that we understand how to instantiate the `InputValidator` object to link it to an Input Field, we just need to understand how to get the answer to know if the Field is valid or not.

To get the answer if the field is valid or not, you need to use method `SetOnValidateCallback()` of the instantiated `InputValidator` object. In this method you must register a function with a code that you want to execute whenever validation is done by `InputValidator`. As previously mentioned, the `InputValidator` object will AUTOMATICALLY validate the linked Field whenever something is typed, erased, or whenever the user interacts with that field (clicking, leaving focus, etc).

Right after validating, the `InputValidator` object will execute the function that you registered in `SetOnValidateCallback()`, passing a parameter containing a `BOOL` value indicating whether the linked Field is valid or not. See the example code below...

```javascript
/*
 * Step 1:
 * First we instantiate the InputValidator object informing everything necessary to validation...
*/
var nameFieldValidation = new InputValidator("nameField", "STRING", 
    { 
        allowEmpty: false,
        maxChars: 80,
        allowNumbers: false
    });

/*
 * Step 2:
 * Now, we register a callback function to get the answer saying if the field is valid or not
 * whenever it is changed or interacted with
*/
nameFieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true)                                    //<- If the field is VALID...
        console.log("The NAME field is valid!");
    if (isInputValid == false)                                   //<- If the field is INVALID...
        console.log("The NAME field is invalid!");
});
```

It's that! After executing these two steps, the `InputValidator` object will automatically validate the linked Field whenever the user interacts or types something in it. The answer will be given to the function you register in `SetOnValidateCallback()` so you can run whatever logic you want!

<b>There's something else!</b> You don't have to wait just for the response returned to your registered function to know if the Field is valid or not. You can also use the `isTheAssociatedFieldValid()` method of the `InputValidator` object to find out if the linked Field is currently valid or not.

The `isTheAssociatedFieldValid()` method will force a validation of the linked Field and will return you a `BOOL` value indicating whether the linked Field is currently valid or not. But before using this method, know that it will ONLY WORK if you have already instantiated an object of type `InputValidator` and registered a function using `SetOnValidateCallback()` method. See example below...

```javascript
//Instancing and registering the callback function...
var nameFieldValidation = new InputValidator("nameField", "STRING", { allowEmpty: false });
nameFieldValidation.SetOnValidateCallback(function(isInputValid){ 
    //... 
});


//Now, to check if the field is currently valid, any time...
var isNameFieldValidNow = nameFieldValidation.isTheAssociatedFieldValid();
```

This is the basics you need to understand about this library! In the next topics you will see all types of Input Types supported by the library, an example code to validate each type of Input Type and <b>also all validation parameters available for you to use!</b>

# Supported Input Types

In the table below you can see all Input Types currently supported by this library. You should only attempt to link supported Input Types to `InputValidator` objects.

| Input Type     | Support       | Value Type   |
| -------------- | ------------- | ------------ |
| button         | Not Supported | -            |
| checkbox       | Not Supported | -            |
| color          | Not Supported | -            |
| date           | Supported     | STRING       |
| datetime-local | Supported     | STRING       |
| email          | Supported     | STRING       |
| file           | Supported     | FILE         |
| hidden         | Not Supported | -            |
| image          | Not Supported | -            |
| month          | Supported     | STRING       |
| number         | Supported     | INT or FLOAT |
| password       | Supported     | STRING       |
| radio          | Not Supported | -            |
| range          | Not Supported | -            |
| reset          | Not Supported | -            |
| search         | Supported     | STRING       |
| submit         | Not Supported | -            |
| tel            | Supported     | STRING       |
| text           | Supported     | STRING       |
| time           | Supported     | STRING       |
| url            | Supported     | STRING       |
| week           | Supported     | STRING       |
| TAG: Select    | Not Supported | -            |
| TAG: Text Area | Supported     | STRING       |

# Available Validation Parameters

These are all available validation parameters that you can enter when instantiating `InputValidator` objects and validating yours Input Fields.

| Parameter               | Works On Type | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowEmpty              | ALL           | Defines whether an empty Field should be allowed or not allowed. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| minChars                | STRING        | Defines the minimum amount of characters that the Field must have. Requires a `Int` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| maxChars                | STRING        | Defines the maximum amount of characters that the Field must have. Requires a `Int` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| allowNumbers            | STRING        | Defines if the Field can or cannot have numbers. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| allowLetters            | STRING        | Defines if the Field may or may not have letters. This includes letters from A to Z and also letters that have accents (eg Á, Ç, Ñ etc). Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                 |
| allowSpace              | STRING        | Defines if the Field can or cannot have spaces. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| allowLineBreak          | STRING        | Defines if the Field can or cannot have line breaks. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| specialCharsAllowed     | STRING        | Defines whether the Field should allow special characters, and if so, which characters will be allowed. You can use the value "none" to not allow any special characters, for example: { specialCharsAllowed: "none" }. If you only want to allow some special characters, you can enter them in a list using the character "," as a separator, for example { specialCharsAllowed: "@,#,&" }. If you want to include the "," character in this list of allowed characters, instead of typing the "," character, type the word "comma". Requires a `String` value. |
| minNumberValue          | INT or FLOAT  | Defines the minimum value (in numeral) that is allowed in the Field. Requires a `Int` or `Float` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| maxNumberValue          | INT or FLOAT  | Defines the maximum value (in numeral) that is allowed in the Field. Requires a `Int` or `Float` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| allowNumberZero         | INT or FLOAT  | Defines if the zero numeral should be allowed or not in the Field. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| allowNumberNegative     | INT or FLOAT  | Defines if negative numerals should be allowed in the Field. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| allowNumberPositive     | INT or FLOAT  | Defines if positive numerals should be allowed in the Field. Requires a `Bool` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| minFilesSelection       | FILE          | Defines the minimum number of files that the user must select in the Field. Requires a `Int` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| maxFilesSelection       | FILE          | Defines the maximum number of files that the user must select in the Field. Requires a `Int` value.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| requiredFilesExtensions | FILE          | Defines the allowed extensions for files selected in the Field. To inform the allowed extensions, you must pass a list that uses the character "," as a separator. For example: { requiredFilesExtensions: "mp4,txt,cs,mp3,png,jpg" }. Requires a `String` value.                                                                                                                                                                                                                                                                                                 |
| maxFilesSizeInKb        | FILE          | Defines the maximum size for files selected in the Field. The size is given in Kibibytes (bytes / 1024). Requires a `Int` value.                                                                                                                                                                                                                                                                                                                                                                                                                                  |

If you have a validation parameter suggestion, please send it through the "<b>Issues</b>" tab, your suggestion will be very welcome!

# Validating Fields with a Custom Regex

This library also supports validating Fields based on a Regex provided by you. If you are going to validate a field that expects inputs of type `STRING`, you can use method `SetCustomRegexForValidation()` to provide a custom Regex to the `InputValidator` object and then it will take your custom Regex into account to validate the Field. The field will only be considered valid if it complies with the validation parameters that you impose, and if it also complies with your custom Regex.

To provide a custom Regex to be taken into account for validation, just call the `SetCustomRegexForValidation()` method after instantiating your `InputValidator` type object. But remember that this will only work if you expect to get a `STRING` type value from the Field. See the code below for example...

```javascript
//On HTML side...
<input type="text" id="phoneNumberField" />

//On Javascript side...
var phoneNumberValidation = new InputValidator("phoneNumberField", "STRING", { allowEmpty: false });
phoneNumberValidation.SetCustomRegexForValidation(/^\([0-9]{3}\)[0-9]{3}-[0-9]{4}$/g); //<- Validate US numbers
phoneNumberValidation.SetOnValidateCallback(function(isInputValid){
    //on receive response from validation
});
```

# Code examples to validate each Input Type

Now let's see code examples to validate EVERY type of Input Field supported by this library.

<h2>Input Type: "date"</h2>

```javascript
//HTML
<input type="date" id="eventDate" />


//JAVASCRIPT
var fieldValidation = new InputValidator("eventDate", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/^\d{4}\-(0[1-9]|1[012])\-(0[1-9]|[12][0-9]|3[01])$/g); //<- Validate "YYYY-MM-DD" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "datetime-local"</h2>

```javascript
//HTML
<input type="datetime-local" id="eventDateTime" />


//JAVASCRIPT
var fieldValidation = new InputValidator("eventDateTime", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/(19|20)[0-9][0-9]-(0[0-9]|1[0-2])-(0[1-9]|([12][0-9]|3[01]))T([01][0-9]|2[0-3]):[0-5][0-9]/g); //<- Validate "YYYY-MM-DDTHH:MM" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "email"</h2>

```javascript
//HTML
<input type="email" id="emailAddress" />


//JAVASCRIPT
var fieldValidation = new InputValidator("emailAddress", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/g); //<- Validate "account@example.com" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "file"</h2>

```javascript
//HTML
<input type="file" id="filePicker" />


//JAVASCRIPT
var fieldValidation = new InputValidator("filePicker", "FILE", { allowEmpty: false, requiredFilesExtensions: "png,jpg,jpeg" });
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "month"</h2>

```javascript
//HTML
<input type="month" id="birthdayMonth" />


//JAVASCRIPT
var fieldValidation = new InputValidator("birthdayMonth", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/([12]\d{3}-(0[1-9]|1[0-2]))/g); //<- Validate "YYYY-MM" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "number"</h2>

```javascript
//HTML
<input type="number" id="houseNumber" />


//JAVASCRIPT
var fieldValidation = new InputValidator("houseNumber", "INT", { allowEmpty: false }); //<- You can use INT if you want an integer or FLOAT if you want an integer or decimal.
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "password"</h2>

```javascript
//HTML
<input type="password" id="accountPassword" />


//JAVASCRIPT
var fieldValidation = new InputValidator("accountPassword", "STRING", { allowEmpty: false });
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "search"</h2>

```javascript
//HTML
<input type="search" id="searchOnPage" />


//JAVASCRIPT
var fieldValidation = new InputValidator("searchOnPage", "STRING", { allowEmpty: false });
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "tel"</h2>

```javascript
//HTML
<input type="tel" id="userPhoneNumber" pattern="^(\([0-9]{3}\) |[0-9]{3}-)[0-9]{3}-[0-9]{4}$" />


//JAVASCRIPT
var fieldValidation = new InputValidator("userPhoneNumber", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/^(\([0-9]{3}\) |[0-9]{3}-)[0-9]{3}-[0-9]{4}$/g); //<- Validate "(123) 321-3456" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "text"</h2>

```javascript
//HTML
<input type="text" id="userStatus" />


//JAVASCRIPT
var fieldValidation = new InputValidator("userStatus", "STRING", { allowEmpty: false });
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "time"</h2>

```javascript
//HTML
<input type="time" id="eventTime" />


//JAVASCRIPT
var fieldValidation = new InputValidator("eventTime", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/^(0[0-9]|1[0-9]|2[0-3]):[0-5][0-9]$/g); //<- Validate "HH:MM" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "url"</h2>

```javascript
//HTML
<input type="url" id="portfolioUrl" />


//JAVASCRIPT
var fieldValidation = new InputValidator("portfolioUrl", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/((([A-Za-z]{3,9}:(?:\/\/)?)(?:[-;:&=\+\$,\w]+@)?[A-Za-z0-9.-]+|(?:www.|[-;:&=\+\$,\w]+@)[A-Za-z0-9.-]+)((?:\/[\+~%\/.\w-_]*)?\??(?:[-\+=&;%@.\w_]*)#?(?:[\w]*))?)/g); //<- Validate "https://domain.com/folder/page" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>Input Type: "week"</h2>

```javascript
//HTML
<input type="week" id="eventWeek" />


//JAVASCRIPT
var fieldValidation = new InputValidator("eventWeek", "STRING", { allowEmpty: false });
fieldValidation.SetCustomRegexForValidation(/^(\d{4})-W(0[1-9]|[1-4][0-9]|5[0-3])$/g); //<- Validate "YYYY-Www" format
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

<h2>TextArea</h2>

The `<textarea>` tag is also supported as a normal field to be validated! :)

```javascript
//HTML
<textarea id="userBiography"></textarea>


//JAVASCRIPT
var fieldValidation = new InputValidator("userBiography", "STRING", { allowEmpty: false });
fieldValidation.SetOnValidateCallback(function(isInputValid){
    if (isInputValid == true) { console.log("is valid!"); }
    if (isInputValid == false) { console.log("is invalid!"); }
});
```

# Support projects like this

If you liked this Library and found it useful for your projects, please consider making a donation (if possible). This would make it even more possible for me to create and continue to maintain projects like this, but if you cannot make a donation, it is still a pleasure for you to use it! Thanks! 😀

<br>

<p align="center">
    <a href="https://www.paypal.com/donate/?hosted_button_id=MVDJY3AXLL8T2" target="_blank">
        <img src="Frontend-Input-Validator-Source/Resources/paypal-donate.png" alt="Donate" />
    </a>
</p>

<br>

<p align="center">
Created with ❤ by Marcos Tomaz
</p>