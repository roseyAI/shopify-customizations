# **📩 Shopify Fix: Add "Full Name" to a Newsletter Form (Prestige Theme)**

## 🧩 Problem:
 Shopify's built-in newsletter forms only support a limited set of fields — like contact[email], contact[first_name], and contact[tags].

When I added a custom Full Name field using contact[full_name], it looked great on the front-end, but neither Shopify nor ActiveCampaign saved the name. Only the email got submitted.

Turns out, Shopify ignores unrecognized form fields, including contact[full_name].

## ✅ Solution:

I kept the single “Full Name” input on the front end, and used JavaScript to split the name into first and last just before the form submits — so Shopify stores it correctly.

## 🛠 How I did it (Prestige Theme) 

 1. Added a new input to the form:
> {%- render 'input', name: 'contact[full_name]', label: 'Full Name',
> type: 'text', autocomplete: 'name' -%}

 2. Inserted this script at the bottom of the newsletter section (before {% schema %}):

```
<script>
  document.addEventListener('DOMContentLoaded', function () {
    const form = document.querySelector('#{{ newsletter_form_id }}');
    const fullNameInput = form?.querySelector('[name="contact[full_name]"]');

    if (form && fullNameInput) {
      const firstNameField = document.createElement('input');
      firstNameField.type = 'hidden';
      firstNameField.name = 'contact[first_name]';

      const lastNameField = document.createElement('input');
      lastNameField.type = 'hidden';
      lastNameField.name = 'contact[last_name]';

      form.appendChild(firstNameField);
      form.appendChild(lastNameField);

      form.addEventListener('submit', function () {
        const fullName = fullNameInput.value.trim();
        const nameParts = fullName.split(' ');
        firstNameField.value = nameParts[0] || '';
        lastNameField.value = nameParts.slice(1).join(' ') || '';
      });
    }
  });
</script>
```


## 💾 Result

-   Customers enter their full name in one field.
    
-   On submit, it splits into `first_name` and `last_name`.
    
-   Shopify now stores the name correctly.
    
-   My ActiveCampaign integration (connected to Shopify) now gets the full name too!
    
----------

### 📌 Why this matters

This is a simple example of how Shopify's form handling can be extended with just a bit of JavaScript — no apps or workarounds needed.

----------

### ✨ Tools used

-   Shopify (Prestige Theme)
    
-   Liquid templating
    
-   Vanilla JavaScript

