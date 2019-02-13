# HTML Forms
[Topics](../README.md)

## HTML Form Elements
- Text Input
    - button
    - checkbox
    - color
    - date
    - datetime-local
    - email
    - file
    - hidden
    - image
    - month
    - number
    - password
    - radio
    - range
    - reset
    - search
    - submit
    - tel
    - text
    - time
    - url
    - week
- Text Area
- Radio Buttons
- Checkboxes
- Dropdown
- Button

## Create HTML Form

HTML forms begin with the `<form>` element. The main attributes are **action** and **method**

```HTML
<form action='' method='get' class='example-form'>
</form>
```

The **action** attribute defines the URL that processes the form and it is where the input collected by the form is sent after the user clicks the **Submit** button. 

Common backend technologies for processing forms:
- Node.js
- PHP
- Ruby on Rails

The **method** attribute can either be *post* or *get*, which define how the form is submitted to the backend server. Generally,

Use **post** when you are *changing* data on the server

Use **get** when you are *getting* data

When you leave **action** blank, it will submit the form to the same URL. Combining this with the *get* method, will let us inspect the contents of the form.

## Text Input Fields

To collect user input, we need the `<input />` element

```HTML
<div class='form-row'>
    <label for='full-name'>Name</label>
    <input id='full-name' name='full-name' type='text' />
</div>
```

The outer `<div>` is to help with styling and for separating input elements. There is also a `<label>` tag, which must have a *for* attribute that matches the *id* attribute of the `<input>` 

    label.for === input.id

The `<input>` element also creates a text field, which can change appearance based on its *type* attribute.

The *id* attribute is ***only for*** connecting to a `<label>` element.

An `<input>` element represents a *variable* that gets sent to the backend server. The *name* attribute defines the name of this variable and the value is whatever the user entered in to the text field.

You can also pre-populate the value with a *value* attribute inside of `<input>`.

### Text Input Styling

You can style specific elements using a new type of CSS selector called an *attribute selector*.

```CSS
.form-row input[type='text']{
    /* Styling for text input goes here */
}
```

## Email Input Fields

`<input>`'s *type* attribute allows you to do basic input validation. 

```HTML
<div class='form-row'>
    <label for='email'>Email</label>
    <input id='email'
           name='email'
           type='email'
           placeholder='name@example.com' />
</div>
```

Using `type='email'` allows us to automatically check if a user entered an email address. It will also give the user a special email-specific keyboard if it sees that attribute.

*placeholder* allows us to display default text when the `<input>` element is empty. 

Similar to text input, we can style email inputs specifically using the CSS selector: `.form-row input[type='email']`


