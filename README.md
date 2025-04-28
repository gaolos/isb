# API ISB Acceso a Artículos

## Descripción
Esta API permite la consulta de información en tiempo real sobre artículos de ISB, incluyendo stock disponible, características técnicas, precios oficiales y demás datos asociados.

El desarrollo y la gestión técnica de esta API es responsabilidad de **Gaolos Cloud S.L.**, mientras que la propiedad de los datos y la autorización para su uso pertenecen exclusivamente a **ISB**.

Esta documentación describe el funcionamiento y uso del primer endpoint disponible.

## Índice
- [Obtener Información de un Artículo](#obtener-información-de-un-artículo)
- [Estructura de Respuesta](#estructura-de-respuesta)
- [Manejo de Errores](#manejo-de-errores)
- [Restricciones](#restricciones)
- [Condiciones de Uso](#condiciones-de-uso)
- [Licencia](#licencia)

---

## Obtener Información de un Artículo

Para consultar la información de un artículo, se debe realizar una petición **POST** al siguiente endpoint:

```
https://isb.gaolos.com/xxx/apirestsibgetarticulo
```

> Nota: `xxx` representa una parte protegida de la URL para mayor seguridad.

### Parámetros de Entrada
La solicitud debe enviarse en formato **JSON** con la siguiente estructura:

```json
{
  "parameters": {
    "RefNeg": "Referencia del cliente",
    "ClaveSesion": "Token de autenticación",
    "ParamsKeys": ["codigo"],
    "ParamsValues": ["Código del artículo"]
  }
}
```

**Descripción de los campos:**
- `RefNeg`: Referencia del cliente.
- `ClaveSesion`: Token de sesión seguro.
- `ParamsKeys`: Clave de consulta (en este caso `"codigo"`).
- `ParamsValues`: Código del artículo a consultar.

**Ejemplo real de llamada:**

```json
{
  "parameters": {
    "RefNeg": "xxx",
    "ClaveSesion": "xxx",
    "ParamsKeys": ["codigo"],
    "ParamsValues": ["13501228"]
  }
}
```

---

## Estructura de Respuesta

### En caso de éxito (`eserror: false`)

```json
{
  "obj": {
    "articulo": "AH-24028  ISB",
    "codigo": "11422257",
    "marca": "ISB",
    "familia": "Rodamientos",
    "subfamilia": "Accesorios para rodamientos",
    "medidas": "(220.000     x250.000     x138.000     )",
    "unidadescaja": 1,
    "pedidominimo": 1,
    "stock": 1,
    "precio": 56.32,
    "dto": -20,
    "preciofinal": 45.06,
    "arancel": "84829900",
    "peso": 911,
    "imagen": null
  },
  "err": {
    "mensaje": null,
    "eserror": false
  }
}
```

### Campos relevantes de la respuesta
- `articulo`: Descripción completa del artículo.
- `codigo`: Código interno de identificación.
- `marca`: Marca del artículo.
- `familia`: Categoría principal.
- `subfamilia`: Categoría secundaria.
- `medidas`: Dimensiones principales del artículo.
- `unidadescaja`: Unidades por caja.
- `pedidominimo`: Pedido mínimo permitido.
- `stock`: Stock disponible en tiempo real.
- `precio`: Precio base (sin descuentos).
- `dto`: Descuento aplicado.
- `preciofinal`: Precio final tras aplicar descuento.
- `arancel`: Código arancelario.
- `peso`: Peso en gramos.
- `imagen`: Imagen en formato **Base64** (si existe).

---

## Manejo de Errores

En caso de error (por ejemplo, artículo no encontrado), la API devolverá:

```json
{
  "obj": null,
  "err": {
    "mensaje": "Artículo no localizado",
    "eserror": true
  }
}
```

### Descripción
- `obj`: Siempre `null` en caso de error.
- `err.mensaje`: Descripción del error.
- `err.eserror`: Bandera booleana (`true` en caso de error).

---

## Restricciones

- **Acceso restringido** mediante token de autenticación.
- **Seguridad de IP**: Se recomienda filtrar accesos por IP si fuera necesario.
- **Frecuencia de llamadas**: Consultar con Gaolos Cloud S.L. sobre límites de peticiones por minuto para evitar bloqueos automáticos.

---

## Condiciones de Uso

- El desarrollo, soporte y mantenimiento técnico de la API es responsabilidad de **Gaolos Cloud S.L.**.
- La propiedad de los datos servidos a través de esta API corresponde a **ISB**.
- El acceso a esta API y el uso de los datos está **autorizado exclusivamente por ISB**. 
- Cualquier uso no autorizado o fuera de los acuerdos establecidos con ISB será considerado incumplimiento de las condiciones legales de uso.

---

## Licencia

Esta API es de **uso restringido**. Su utilización está limitada a clientes o partners autorizados explícitamente por **ISB** bajo las condiciones establecidas por **Gaolos Cloud S.L.**.

---
