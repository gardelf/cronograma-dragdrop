# Despliegue en Railway - Cronograma con Drag & Drop

## 📋 Repositorio

**GitHub:** https://github.com/gardelf/cronograma-dragdrop

## 🚀 Pasos para Desplegar en Railway

### 1. Crear Nuevo Proyecto en Railway

1. Ve a [Railway](https://railway.app/)
2. Click en "New Project"
3. Selecciona "Deploy from GitHub repo"
4. Busca y selecciona `gardelf/cronograma-dragdrop`

### 2. Configurar Variables de Entorno

En la configuración del proyecto en Railway, añade las siguientes variables:

```
TODOIST_API_TOKEN=tu_token_todoist
ICLOUD_USERNAME=tu_usuario_icloud
ICLOUD_APP_PASSWORD=tu_contraseña_app_icloud
FIREFLY_URL=tu_url_firefly
FIREFLY_TOKEN=tu_token_firefly
OPENAI_API_KEY=tu_api_key_openai
```

### 3. Configurar el Comando de Inicio

Railway debería detectar automáticamente el `Procfile`, pero si no:

**Start Command:**
```
python web_server.py
```

### 4. Configurar el Puerto

Railway asigna automáticamente el puerto, pero asegúrate de que el servidor escuche en `0.0.0.0`:

En `web_server.py` al final del archivo:
```python
if __name__ == '__main__':
    port = int(os.environ.get('PORT', 8080))
    app.run(host='0.0.0.0', port=port, debug=False)
```

### 5. Desplegar

Railway desplegará automáticamente después de conectar el repositorio.

## ✨ Nuevas Funcionalidades

### Drag & Drop con Recalculación Automática

- **Arrastra tareas** para reorganizarlas
- **Horarios recalculados** automáticamente
- **Botón "Guardar Orden"** flotante en la esquina inferior derecha
- **Endpoint `/save-order`** para persistir el nuevo orden

### Endpoints Añadidos

- `POST /save-order` - Guarda el nuevo orden de tareas con horarios recalculados

## 🔧 Verificación

Después del despliegue, verifica:

1. ✅ Página principal carga correctamente
2. ✅ Drag & drop funciona
3. ✅ Horarios se recalculan automáticamente
4. ✅ Botón "Guardar Orden" aparece
5. ✅ Todas las integraciones funcionan (BOE, Idealista, Firefly III)

## 📝 Notas

- El archivo `config.py` NO está en el repositorio por seguridad
- Todas las API keys deben configurarse como variables de entorno en Railway
- El cronograma se genera dinámicamente desde Todoist e iCloud Calendar
