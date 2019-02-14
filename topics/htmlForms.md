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

### Styling Text Input

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

### Styling Email Input

Similar to text input, we can style email inputs specifically using the CSS selector: `.form-row input[type='email']`

## Radio Buttons

Using `<input type='radio'>` transforms the input field into a radio button. Radio buttons always work in groups, which means we need a label for each `<input>` and also a way to group the radio buttons and label the entire group.

This is where `<fieldset>` and `<legend>` elements come in.

For every radio button group you create, you shoud:

- Wrap in a `<fieldset>` and label with a `<legend>`
- Associate a `<label>` with each button
- Use the same *name* attribute for each radio button
- Use different *value* attributes for each radio

```HTML
<fieldset class='legacy-form-row'>
    <legend>Types of Talk</legend>
    <input id='talk-type-1'
           name='talk-type'
           type='radio'
           value='main-stage' />
    <label for='talk-type-1' class='radio-label'>Main Stage</label>
    <input id='talk-type-2'
           name='talk-type'
           type='radio'
           value='workshop'
           checked />
    <label for='talk-type-2' class='radio-label'>Workshop</label>
</fieldset>
```
Since we cannot enter customer values in to a radio button, each need an explicit *value* attribute. This is the value that will get sent to the server when the user submits the form. Again, each radio button must have the same *name* attibute for the form to know they were a part of the same group.

There is also the boolean attribute of *checked*

### Styling Radio Buttons

`<fieldset>` doesn't support flexbox, so an example of styling for mobile and desktop would be as follows:

```css
.legacy-form-row{
    border: none;
    margin-bottom: 40px;
}
.legacy-form-row legend{
    margin-bottom: 15px;
}
.legacy-form-row .radio-label{
    display: block;
    font-size: 14px;
    padding: 0 20px 0 10px;
}
.legacy-form-row input[type='radio']{
    margin-top: 2px;
}
.legacy-form-row .radio-label,
.legacy-form-row input[type='radio']{
    float: left;
}

@media only screen and (min-width: 700px){
    .legacy-form-row{
        margin-bottom: 10px;
    }
    .legacy-form-row legend{
        width: 120px;
        text-align: right;
        padding-right: 20px;
    }
    .legacy-form-row legend{
        float: left;
    }
}
```

## Select Elements (Dropdown Menus)

The `<select>` element represents the dropdown menu and each item is represented by the `<option>` element

```html
<div class='form-row'>
    <label for='t-shirt'>T-Shirt Size</label>
    <select id='t-shirt' name='t-shirt'>
        <option value='xs'>Extra Small</option>
        <option value='s'>Small</option>
        <option value='m'>Medium</option>
        <option value='l'>Large</option>
    </select>
</div>
```

Here the *name* and *value* attributes get passed to the backend but instead of being defined on a single element, they are spread across the `<select>` and `<option>` elements.

## Textareas

`<textarea>` creates a multi-line text field

```html
<div class='form-row'>
    <label for='abstract'>Abstract</label>
    <textarea id='abstract' name='abstract'></textarea>
    <div class='instructions'>Describe your...</div>
</div>
```

Note: You *always* need a closing `</textarea>` tag. Also, to add any default text, it must be placed inbetween the tags as opposed to a *value* attribute.

### Styling Textareas

```css
.form-row textarea{
    font-family: "Helvetica", "Arial", sans-serif;
    font-size: 14px;

    border: 1px solid #D6D9DC;
    border-radius: 3px;

    min-height: 200px;
    margin-bottom: 10px;
    padding: 7px;
    resize: none;
    /* browsers by default allows the user to resize the textarea, to disable this we add the line  `resize: none;`  */
}
.form-row .instrcutions{
    color: #999999;
    font-size: 14px;
    margin-bottom: 30px;
}
```

## Checkboxes

Checkboxes allow users to select as many options as they want, as opposed to radio buttons

```html
<div class='form-row'>
    <label class='checkbox-label' for='available'>
    <input id='availble'
           name='available'
           type='checkbox'
           value='is-available' />
    <span>I'm actually available the date of the talk</span>
    </label>
</div>
```

Note: We use `<label>` here to wrap the `<input>` element instead of making it a separate element.

## Submit Buttons

```html
<div class='form-row'>
    <button>Submit</button>
</div>
```

Clicking the button tells the browser to validate all of the `<input />` elements in the form and submit it to the action URL

### Styling Buttons

```css
.form-row button{
    font-size: 16px;
    font-weight: bold;

    color: #FFFFFF;
    background-color: #5995DA;

    border: none;
    border-radius: 3px;

    padding: 10px 40px;
    cursor: pointer;
}
.form-row button:hover{
    background-color: #76AEED;
}
.form-row button:active{
    background-color: #407FC7;
}
```

`button:hover` and `button:active` should be two styles to incorporate in css

# Summary

The different types of form elements include:
- `<input type='text' />`
- `<input type='email' />`
- `<input type='radio' />`
- `<select>` & `<option>`
- `<textarea>`
- `<input type='checkbox' />`
- `<button>`

There are two ways generally to process forms:

- Use the `action` attribute to send the form data to a backend URL, which then redirects to a success or error page.
- Use AJAX queries to submit the form without leaving the page. Success or error messages are displayed on the same page by manipulating the HTML with JS

