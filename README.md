# Scroll Force - PWA para Magos

App profesional de forzaje de imágenes con autenticación y personalización.

## 📁 Estructura del Proyecto

```
emoji-force/
├── index.html          # Galería principal
├── config.html         # Configuración de imágenes
├── manifest.json       # PWA manifest
├── sw.js              # Service Worker
├── images/            # Imágenes por defecto
│   ├── 1.jpg
│   ├── 2.jpg
│   ├── 3.jpg
│   ├── 4.jpg (forzaje por defecto)
│   ├── 5.jpg
│   ├── 6.jpg
│   ├── 7.jpg
│   ├── 8.jpg
│   └── 9.jpg
├── icon-192.png       # Icono PWA 192x192
└── icon-512.png       # Icono PWA 512x512
```

## 🚀 Deploy en GitHub Pages

### Paso 1: Crear Repositorio

```bash
# Inicializar git
git init
git add .
git commit -m "Initial commit"

# Crear repo en GitHub y conectar
git remote add origin https://github.com/TU-USUARIO/emoji-force.git
git branch -M main
git push -u origin main
```

### Paso 2: Activar GitHub Pages

1. Ve a tu repositorio en GitHub
2. Settings → Pages
3. Source: Deploy from a branch
4. Branch: main → / (root)
5. Save

Tu app estará en: `https://TU-USUARIO.github.io/emoji-force/`

## 📸 Preparar Imágenes

### Opción A - Usar Imágenes Por Defecto

Coloca 9 imágenes en la carpeta `/images/`:
- Nombradas: 1.jpg, 2.jpg, 3.jpg ... 9.jpg
- Tamaño recomendado: 1080x1920 (vertical)
- Formato: JPG o PNG

### Opción B - Personalización por Usuario

Los usuarios pueden subir sus propias imágenes desde el botón ⚙️ en la app.
Las imágenes se guardan en IndexedDB (local, en su teléfono).

## 🔐 Sistema de Autenticación

### Crear Códigos Manualmente

En Supabase → Table Editor → `active_codes`:

```sql
INSERT INTO active_codes (code, is_activated) VALUES
('EMOJI-A7K9-M2P5', false),
('EMOJI-B3X2-N8Q1', false),
('EMOJI-C9R4-P7M3', false);
```

### Flujo de Usuario

1. **Primera vez:**
   - Usuario abre la app
   - Ingresa código de activación
   - Se valida con Supabase (`loginWithCode`)
   - Código queda activado

2. **Siguientes veces:**
   - Se valida automáticamente (`validate-session`)
   - Si otro dispositivo abrió con ese código, esta sesión queda inactiva

## ⚙️ Configuración

### Cambiar Imagen de Forzaje

En `index.html`, línea ~180:

```javascript
const FORCE_IMAGE_INDEX = 4; // Cambiar a 1-9
```

### Cambiar Cantidad de Toques

En `index.html`, línea ~182:

```javascript
const TOUCH_THRESHOLD = 10; // Cambiar a cualquier número
```

### Cambiar Total de Imágenes

En `index.html`, línea ~181:

```javascript
const TOTAL_IMAGES = 9; // Cambiar a 5, 7, 12, etc.
```

## 🎨 Personalización de Imágenes

Los usuarios pueden:

1. Tocar el botón ⚙️ en la app
2. Subir hasta 9 imágenes desde su galería
3. Seleccionar cuál será la imagen de forzaje
4. Todo se guarda localmente (no sube a servidor)

## 📱 Instalación como App

### iOS (Safari)
1. Abrir en Safari
2. Tocar botón compartir
3. "Agregar a pantalla de inicio"

### Android (Chrome)
1. Abrir en Chrome
2. Tocar el botón "Instalar App" que aparece
3. O menú → "Añadir a pantalla de inicio"

## 🔧 Testing Local

```bash
# Con Python
python -m http.server 8000

# Con Node.js
npx serve

# Luego abrir: http://localhost:8000
```

## ✅ Checklist Pre-Deploy

- [ ] 9 imágenes en carpeta `/images/` (1.jpg - 9.jpg)
- [ ] Iconos PWA (icon-192.png, icon-512.png)
- [ ] Códigos creados en Supabase
- [ ] Funciones edge desplegadas
- [ ] Testeado en móvil local

## 🎯 Uso en Show

1. Activar código (solo primera vez)
2. Opcional: Personalizar imágenes
3. Durante el show:
   - Funciona 100% offline
   - Después de 10 toques → muestra imagen forzada
   - Sin internet necesario

## 💡 Tips

- **Nunca compartas el código de GitHub** si tiene códigos hardcodeados
- Los códigos se crean manualmente en Supabase
- Las imágenes personalizadas NO se sincronizan entre dispositivos
- Si cambia de teléfono, solo ingresa su código nuevamente

## 📞 Soporte

Para problemas con:
- **Supabase:** Revisa las funciones Edge en Dashboard
- **GitHub Pages:** Verifica que esté en branch `main`
- **PWA:** Limpia caché del navegador

---

Creado con ❤️ para magos profesionales
