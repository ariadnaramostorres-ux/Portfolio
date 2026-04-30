# Testing: Portfolio App

## Overview
React + Vite portfolio app with 3 chatbot demos (Correos Express AI, SEUR Smart Logistics, Telefónica Neural Search) and an EmailJS-powered contact form.

## Setup

```bash
cd Portfolio_Bueno-main/Portfolio_Bueno-main
npm install
npm run dev  # defaults to port 3000
```

### Environment Variables
Create a `.env` file in the project root (`Portfolio_Bueno-main/Portfolio_Bueno-main/.env`):
```
VITE_EMAILJS_SERVICE_ID=<service_id>
VITE_EMAILJS_TEMPLATE_ID=<template_id>
VITE_EMAILJS_PUBLIC_KEY=<public_key>
```
Without these, the contact form will show an error alert on submission but won't crash.

## Devin Secrets Needed
- `VITE_EMAILJS_SERVICE_ID` — EmailJS service ID
- `VITE_EMAILJS_TEMPLATE_ID` — EmailJS template ID  
- `VITE_EMAILJS_PUBLIC_KEY` — EmailJS public key

## Lint / Typecheck
```bash
npm run lint   # runs tsc --noEmit
```
No test suite or pre-commit hooks configured.

## Key Testing Flows

### 1. Chatbot Independence
Each project has a "Lanzar Demo" (or "Iniciar Chat") button in the Proyectos section.
- Open chatbot A → send a message → close → open chatbot B
- **Verify**: Chatbot B shows only its own greeting (1 message), no messages from A
- **Verify**: Keyword responses match the correct chatbot (e.g., "paquete" → Correos, "ruta" → SEUR)

### 2. Contact Form (EmailJS)
Scroll to the Contacto section or click CONTACTO in the nav.
- Fill name, email, message → click "Enviar Propuesta"
- **Verify**: Button changes to "Enviando..." during submission
- **Verify**: Success alert appears ("¡Mensaje enviado correctamente!") or error alert if credentials missing
- **Verify**: Form fields reset after success

## Common Pitfalls
- **Chatbot selection bug**: The `chatWithAI()` function in `localAI.ts` matches chatbot identity by searching for keywords in its second parameter. If you pass the project *description* instead of the project *title*, all chatbots may default to Correos Express. Always pass the `title` prop (e.g., "SEUR Smart Logistics") not the `context` prop.
- **Port conflicts**: If port 3000 is in use, Vite auto-selects another port (e.g., 3001). Check terminal output.
- **Nested directory**: The actual app code is inside `Portfolio_Bueno-main/Portfolio_Bueno-main/` (double-nested), not at the repo root.
