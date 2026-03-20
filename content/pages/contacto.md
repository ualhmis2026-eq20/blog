---
title: "Contacto"
date: 2026-03-20
type: "pages"
menu:
  main:
    name: "CONTACTO"
    identifier: "contacto"
    weight: 3
_build:
  list: never
  render: always
---

¿Tienes alguna pregunta o sugerencia? ¡Escríbenos!

<form action="https://formspree.io/f/xvzwyqyl" method="POST" style="max-width:520px; margin:2rem auto;">

  <div style="margin-bottom:1rem;">
    <label style="display:block; margin-bottom:4px; font-weight:600;">Nombre</label>
    <input type="text" name="nombre" required
      style="width:100%; padding:10px; border:1px solid #ccc; border-radius:8px; font-size:1rem;">
  </div>

  <div style="margin-bottom:1rem;">
    <label style="display:block; margin-bottom:4px; font-weight:600;">Email</label>
    <input type="email" name="email" required
      style="width:100%; padding:10px; border:1px solid #ccc; border-radius:8px; font-size:1rem;">
  </div>

  <div style="margin-bottom:1rem;">
    <label style="display:block; margin-bottom:4px; font-weight:600;">Asunto</label>
    <input type="text" name="asunto" required
      style="width:100%; padding:10px; border:1px solid #ccc; border-radius:8px; font-size:1rem;">
  </div>

  <div style="margin-bottom:1.5rem;">
    <label style="display:block; margin-bottom:4px; font-weight:600;">Mensaje</label>
    <textarea name="mensaje" rows="5" required
      style="width:100%; padding:10px; border:1px solid #ccc; border-radius:8px; font-size:1rem; resize:vertical;"></textarea>
  </div>

  <button type="submit"
    style="width:100%; padding:12px; background:#0066cc; color:white; border:none; border-radius:8px; font-size:1rem; cursor:pointer; font-weight:600;">
    ✉️ Enviar mensaje
  </button>

</form>