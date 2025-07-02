# 📩 Shopify Fix: Add First and Last Name to a Newsletter Form (Prestige Theme)

## 🧩 Problem

Prestige Theme default newsletter form only collects an email address, which limits personalization and segmentation. There's no built-in option for capturing first and last names — something most email marketing tools benefit from.

## ✅ Solution

We added two supported fields — `contact[first_name]` and `contact[last_name]` — directly to the newsletter form. These are recognized by Shopify and passed properly to connected apps like ActiveCampaign.

No JavaScript or apps required — just a simple Liquid update.

## 🛠 How I Did It (Prestige Theme)

### 1. Located the default form block in `newsletter.liquid`

Original code:
```
<div class="form-row">
  {%- assign input_label = 'general.newsletter.email' | t -%}
  {%- render 'input', name: 'contact[email]', label: input_label, label_hidden: true, type: 'email', required: true, autocomplete: 'email', enterkeyhint: 'send' -%}
  {%- render 'button', type: 'submit', content: section.settings.button_text -%}
</div>
```
### 2. Replaced it with:
```
<div class="form-row">
  {%- assign first_name_label = 'First Name' -%}
  {%- render 'input', name: 'contact[first_name]', label: first_name_label, label_hidden: true, type: 'text', autocomplete: 'given-name' -%}
</div>

<div class="form-row">
  {%- assign last_name_label = 'Last Name' -%}
  {%- render 'input', name: 'contact[last_name]', label: last_name_label, label_hidden: true, type: 'text', autocomplete: 'family-name' -%}
</div>

<div class="form-row">
  {%- assign input_label = 'general.newsletter.email' | t -%}
  {%- render 'input', name: 'contact[email]', label: input_label, label_hidden: true, type: 'email', required: true, autocomplete: 'email', enterkeyhint: 'send' -%}
</div>

<div class="form-row">
  {%- render 'button', type: 'submit', content: section.settings.button_text -%}
</div>
```

## 💾 Result
Visitors can now enter their first name, last name, and email in your newsletter form.

Shopify stores this information under the customer's profile.

Your email marketing tools (e.g., ActiveCampaign) receive full contact details without extra setup.

## 📌 Why This Matters
This small update improves personalization, supports better email segmentation, and makes your list far more useful — without requiring extra scripts or apps.

## ✨ Tools Used
Shopify (Prestige Theme)

Liquid templating

Native Shopify field support
