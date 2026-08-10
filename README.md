# 🎓 Plataforma Web de Capacitación e Interactividad

Aplicación web interactiva desarrollada en **React (standalone)** y **Tailwind CSS**, diseñada para la evaluación continua, el aprendizaje estructurado en módulos y la certificación directa en formato PDF.

---

## 📌 Características Principales

* **Registro de Usuario:** Captura el nombre y correo del estudiante para personalizar la experiencia y el certificado final.
* **Módulo de Diagnóstico:** Evaluación inicial previa para conocer los conocimientos base del usuario.
* **15 Subcursos Interactivos:** Flujo ordenado con navegación paso a paso entre módulos.
* **Evaluación Final Proporcional:** Examen final compuesto por **15 preguntas independientes** (1 pregunta correspondiente a cada subcurso visto).
* **Generación Directa de Certificado (PDF):** Sistema de exportación nativo a `.pdf` optimizado para computadoras y dispositivos móviles (evita el cuadro de diálogo de impresión).

---

## 🛠️ Tecnologías Utilizadas

* **HTML5 / JavaScript (ES6+)**
* **React 18 & ReactDOM** (vía CDN con Babel)
* **Tailwind CSS** (vía CDN para estilos responsive)
* **html2canvas & jsPDF** (Librerías para captura DOM y exportación de archivos PDF)

---

## 🚀 Instalación y Uso Local

No requiere de un entorno Node.js o proceso de compilación (`build`). Puedes ejecutarlo de dos formas sencillas:

1. **Directo en el Navegador:**
   * Clona este repositorio o descarga el archivo `index.html`.
   * Abre `index.html` en cualquier navegador web moderno.

2. **Servidor Local (Opcional):**
   * Puedes usar extensiones como **Live Server** en VS Code para correrlo en un entorno local.

---

## 📄 Descarga del Certificado

Para garantizar que el certificado se descargue automáticamente como un archivo `.pdf` (sin llamar a la función `window.print()`):

```javascript
// Captura el elemento HTML del certificado y genera el documento PDF nativo
const descargarPDF = async () => {
  const { jsPDF } = window.jspdf;
  const elemento = document.getElementById('certificado');

  const canvas = await html2canvas(elemento, { scale: 2 });
  const imgData = canvas.toDataURL('image/png');

  const pdf = new jsPDF('p', 'mm', 'a4');
  const pdfWidth = pdf.internal.pageSize.getWidth();
  const pdfHeight = (canvas.height * pdfWidth) / canvas.width;

  pdf.addImage(imgData, 'PNG', 0, 0, pdfWidth, pdfHeight);
  pdf.save('Certificado.pdf');
};
