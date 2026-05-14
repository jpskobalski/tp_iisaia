Actuá como arquitecto de software backend experto en diseño de APIs REST y contratos OpenAPI.

Necesito que generes un archivo llamado `openapi.yaml` siguiendo estrictamente el estándar OpenAPI 3.1, en formato YAML válido.

El objetivo es definir el contrato de una API REST para un sistema CRM simple, centrado en la gestión de clientes y sus contactos asociados.

Importante:
- No generes implementación, base de datos, autenticación, frontend, deploy ni código backend.
- Solo generá el contrato OpenAPI como archivo editable.
- La API debe modelar recursos, no acciones.
- Usá nombres de recursos en plural y en español.
- El YAML debe ser compatible con Swagger UI.
- La respuesta final debe contener únicamente el contenido del archivo `openapi.yaml`, sin explicaciones adicionales.

Requisitos funcionales mínimos:

1. Recurso principal:
   - `/clientes`
   - Representa clientes del CRM.

2. Recurso individual:
   - `/clientes/{clienteId}`
   - Permite obtener o eliminar un cliente específico.

3. Recurso anidado:
   - `/clientes/{clienteId}/contactos`
   - Representa contactos asociados a un cliente.
   - Debe quedar clara la jerarquía entre clientes y contactos.

4. Recurso anidado individual:
   - `/clientes/{clienteId}/contactos/{contactoId}`
   - Permite obtener o eliminar un contacto específico de un cliente.

Métodos HTTP obligatorios:

- `GET /clientes`
  - Lista clientes.
  - Debe permitir parámetros opcionales de query como `limit`, `offset` y `estado`.

- `POST /clientes`
  - Crea un nuevo cliente.

- `GET /clientes/{clienteId}`
  - Obtiene el detalle de un cliente.

- `DELETE /clientes/{clienteId}`
  - Elimina un cliente.

- `GET /clientes/{clienteId}/contactos`
  - Lista los contactos de un cliente.

- `POST /clientes/{clienteId}/contactos`
  - Crea un contacto asociado a un cliente.

- `GET /clientes/{clienteId}/contactos/{contactoId}`
  - Obtiene el detalle de un contacto específico.

- `DELETE /clientes/{clienteId}/contactos/{contactoId}`
  - Elimina un contacto específico.

Requisitos de OpenAPI:

1. Usar:
   - `openapi: 3.1.0`
   - `info`
   - `servers`
   - `paths`
   - `components/schemas`

2. Cada endpoint debe incluir:
   - `summary`
   - `description`
   - `operationId`
   - `tags`
   - parámetros si corresponde
   - `requestBody` cuando corresponda
   - respuestas de éxito
   - respuestas de error

3. Respuestas de éxito:
   - `200 OK` para operaciones GET.
   - `201 Created` para operaciones POST.
   - `204 No Content` para operaciones DELETE.

4. Respuestas de error:
   - Documentar al menos:
     - `400 Bad Request` para datos inválidos.
     - `404 Not Found` para cliente o contacto inexistente.
   - Usar un schema común de error llamado `ErrorResponse`.

5. Definir schemas tipados en `components/schemas`, incluyendo como mínimo:

   - `Cliente`
   - `ClienteInput`
   - `Contacto`
   - `ContactoInput`
   - `ErrorResponse`

6. Los schemas deben usar tipos explícitos:
   - `string`
   - `integer`
   - `boolean`
   - `array`
   - `object`

7. Marcar campos obligatorios con `required`.

8. Incluir restricciones cuando aplique:
   - `format: email`
   - `format: date-time`
   - `enum`
   - `minLength`
   - `maxLength`
   - `minimum`
   - `maximum`

Modelo sugerido:

Cliente:
- `id`: string, requerido, solo lectura.
- `nombre`: string, requerido.
- `email`: string, requerido, formato email.
- `telefono`: string, opcional.
- `empresa`: string, opcional.
- `estado`: string, requerido, enum: `activo`, `inactivo`, `prospecto`.
- `fechaCreacion`: string, formato date-time, solo lectura.

ClienteInput:
- `nombre`
- `email`
- `telefono`
- `empresa`
- `estado`

Contacto:
- `id`: string, requerido, solo lectura.
- `clienteId`: string, requerido, solo lectura.
- `nombre`: string, requerido.
- `email`: string, requerido, formato email.
- `cargo`: string, opcional.
- `principal`: boolean, requerido.
- `fechaCreacion`: string, formato date-time, solo lectura.

ContactoInput:
- `nombre`
- `email`
- `cargo`
- `principal`

ErrorResponse:
- `codigo`: string, requerido.
- `mensaje`: string, requerido.
- `detalles`: array de strings, opcional.

También agregá ejemplos realistas en:
- request bodies
- responses exitosas
- responses de error

Validá mentalmente que el YAML sea consistente, esté bien indentado y no tenga referencias rotas en `$ref`.

Generá directamente el contenido completo del archivo `openapi.yaml`.