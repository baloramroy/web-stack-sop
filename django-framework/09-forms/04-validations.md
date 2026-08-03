**Phase 8 — Forms**

# Step 4 — Validation

This is one of Django's biggest strengths. Instead of manually checking every field yourself, Django's form system performs validation for you.

---

## Learning Objective

By the end of this lesson, you'll understand:

* What validation means
* Why validation is necessary
* How Django validates forms
* What `is_valid()` does
* What happens when validation fails
* What `cleaned_data` is

> We will **not** save anything to a database yet. Our focus is understanding the validation process.

---

## What Is Validation?

Validation means checking whether the submitted data is acceptable before using it.

Imagine a user submits this form:

```text
Name: John
Email: john@gmail.com
```

Everything looks fine.

Now imagine another user submits:

```text
Name:
Email: abc
```

Problems:

* The name is empty.
* The email is not in a valid email format.

Without validation, your application could process incorrect or incomplete data.

---

## Real-Life Example

Think about opening a bank account.

The bank asks for:

* Full name
* National ID
* Phone number

If you leave the name blank or type letters instead of numbers for the phone number, the bank won't accept the application.

That's validation.

The same idea applies to web forms.

---

## Where Does Validation Happen?

Let's review the flow.

```text
Browser
    │
    ▼
User fills form
    │
    ▼
POST request
    │
    ▼
View
    │
    ▼
Create form with submitted data
    │
    ▼
Validation
    │
 ┌──────────────┐
 │              │
 │ Valid        │ Invalid
 │              │
 ▼              ▼
Process      Show errors
```

Notice that validation happens **after** Django receives the POST request.

---

## Creating a Form with Submitted Data

Previously, we created an empty form.

```python
form = ContactForm()
```

That is used for displaying the form.

When the user submits data, we instead pass the submitted data into the form.

```python
form = ContactForm(request.POST)
```

Now the form knows what the user entered.

---

## The Most Important Method

Django validates the form using:

```python
form.is_valid()
```

This is one of the most commonly used methods in Django.

Example:

```python
if form.is_valid():
    print("Everything is valid")
else:
    print("There are errors")
```

---

## What Does `is_valid()` Actually Do?

Suppose our form is:

```python
class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
```

The user submits:

```text
Name: John
Email: john@gmail.com
```

When Django runs:

```python
form.is_valid()
```

it checks things like:

* Is `name` present?
* Is `name` shorter than 100 characters?
* Is `email` present?
* Does `email` look like a valid email address?

If every check passes:

```python
True
```

Otherwise:

```python
False
```

---

## Valid Example

Submitted data:

```text
Name: Alice
Email: alice@example.com
```

```python
form.is_valid()
```

Result:

```python
True
```

---

## Invalid Example

Submitted data:

```text
Name:
Email: not-an-email
```

Checks:

* Name is missing ❌
* Email format is invalid ❌

Result:

```python
False
```

---

## Updating the View

Let's modify our view to validate the form.

```python
from django.shortcuts import render
from .forms import ContactForm


def contact(request):

    if request.method == "POST":

        form = ContactForm(request.POST)

        if form.is_valid():
            print("Valid form")
        else:
            print("Invalid form")

    else:
        form = ContactForm()

    return render(request, "contact.html", {
        "form": form
    })
```

Let's understand the flow.

---

## GET Request

User visits:

```text
/contact/
```

The browser sends:

```text
GET
```

The view executes:

```python
form = ContactForm()
```

The browser displays an empty form.

---

## POST Request

The user submits:

```text
Name: John
Email: john@gmail.com
```

Now the view executes:

```python
form = ContactForm(request.POST)
```

Then:

```python
form.is_valid()
```

If everything is correct:

```python
print("Valid form")
```

Otherwise:

```python
print("Invalid form")
```

---

## Why Don't We Create an Empty Form Again?

Notice the difference.

Incorrect:

```python
form = ContactForm()

if request.method == "POST":
    form.is_valid()
```

This form contains **no submitted data**, so validation won't work as expected.

Correct:

```python
form = ContactForm(request.POST)
```

Now the form contains the user's submitted values.

---

## What Is `cleaned_data`?

When validation succeeds:

```python
if form.is_valid():
```

Django creates a dictionary called:

```python
form.cleaned_data
```

This contains the validated values.

Example:

```python
{
    "name": "John",
    "email": "john@gmail.com"
}
```

You can access them like this:

```python
name = form.cleaned_data["name"]
email = form.cleaned_data["email"]
```

Think of it as:

```text
request.POST
        │
        ▼
Validation
        │
        ▼
cleaned_data
```

Only **validated** data appears in `cleaned_data`.

---

## Why Not Use `request.POST` Directly?

You might wonder:

> "If the data is already in `request.POST`, why use `cleaned_data`?"

Because `request.POST` contains the raw user input.

Example:

```text
Email: abc
```

`request.POST` still contains:

```python
{
    "email": "abc"
}
```

But if validation fails:

```python
form.is_valid()
```

returns:

```python
False
```

and `cleaned_data` is **not safe to use** for invalid fields.

This is why Django encourages you to work with `cleaned_data` after successful validation.

---

## Displaying Errors

If validation fails, Django stores the error messages in the form.

Because we're already sending the form back to the template:

```python
return render(request, "contact.html", {
    "form": form
})
```

the template can automatically display those errors.

For example, if the email is invalid, the page might show:

```text
Email:
[____________]

Enter a valid email address.
```

You don't need to manually create those messages—Django handles them for standard validations.

---

## Complete Validation Flow

```text
User opens page
        │
        ▼
GET
        │
        ▼
Empty ContactForm()
        │
        ▼
Template
        │
        ▼
User fills form
        │
        ▼
POST
        │
        ▼
ContactForm(request.POST)
        │
        ▼
form.is_valid()
        │
   ┌──────────────┐
   │              │
True           False
   │              │
   ▼              ▼
cleaned_data   form.errors
```

---

## Common Beginner Mistakes

### 1. Calling `is_valid()` on an empty form

❌ Wrong:

```python
form = ContactForm()
form.is_valid()
```

The form has no submitted data.

✔ Correct:

```python
form = ContactForm(request.POST)
```

#

### 2. Using `cleaned_data` before validation

❌ Wrong:

```python
name = form.cleaned_data["name"]
```

before calling:

```python
form.is_valid()
```

✔ Correct:

```python
if form.is_valid():
    name = form.cleaned_data["name"]
```

#

### 3. Using `request.POST` after validation

After validation succeeds, prefer:

```python
form.cleaned_data
```

instead of reading values from:

```python
request.POST
```

This keeps your code working with validated data.

---

## Step 4 Summary

You now understand the core of Django form validation:

* ✅ Validation checks whether submitted data is acceptable.
* ✅ Use `ContactForm(request.POST)` to create a form with submitted data.
* ✅ Call `form.is_valid()` to run Django's built-in validation.
* ✅ If validation succeeds, access the validated values through `form.cleaned_data`.
* ✅ If validation fails, Django stores the error messages in the form so they can be shown in the template.

At this point, you have learned the complete lifecycle of a basic Django form:

1. Create the form.
2. Display the form.
3. Submit the form.
4. Validate the submitted data.

