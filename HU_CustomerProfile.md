# Historia de Usuario: Implementación de Wrapper para API Profile-Customer

## Descripción
Como desarrollador del microservicio `ms_customer_management`, necesito crear una operación que sirva de wrapper para el endpoint `/profile-customer` definido en la API externa "Customer Acquisition Management - Profiling". El propósito es proporcionar una interfaz limpia para los clientes que consuman nuestros servicios, eliminando metainformación sensible y simplificando la integración.

## Objetivo
Implementar un nuevo endpoint en `ms_customer_management` que exponga la ruta `/management/CustomerProfile`, el cual internamente realizará llamadas al endpoint externo `/profile-customer` y devolverá la respuesta filtrada, eliminando metadatos sensibles y credenciales.

## Criterios de Aceptación

1. ✅ Crear un nuevo endpoint REST en `ms_customer_management` con la ruta `/management/CustomerProfile`.
2. ✅ El endpoint debe aceptar peticiones POST con el formato de datos requerido para la perfilación de clientes.
3. ✅ Implementar el mapper para transformar la solicitud desde el formato de nuestra API al formato requerido por la API externa.
4. ✅ Implementar la llamada al servicio externo `/profile-customer` a través de WebClient.
5. ✅ Transformar la respuesta del servicio externo para eliminar metadatos sensibles como nombres de aplicaciones o credenciales.
6. ✅ Implementar manejo de errores adecuado para las diferentes respuestas del servicio externo.
7. ✅ La respuesta debe mantener la información relevante de negocio para el cliente como el código y nombre de la acción a seguir.
8. ✅ Agregar logs de inicio y fin de proceso para monitoreo y trazabilidad.
9. ✅ Implementar pruebas unitarias para verificar el correcto funcionamiento del wrapper.

## Detalles Técnicos

### Componentes Implementados:

1. **DTO de Entrada y Salida**:
   - ✅ `CustomerProfileRequestDto` - Para recibir la solicitud del cliente
   - ✅ `CustomerProfileResponseDto` - Para devolver la respuesta filtrada

2. **Router y Handler**:
   - ✅ Se añadió una nueva ruta en `ManagementRouter` para el endpoint `/management/CustomerProfile`
   - ✅ Se creó `CustomerProfileManagementHandler` para procesar las peticiones

3. **Mappers**:
   - ✅ Se implementó `CustomerProfileMapper` para transformar entre los objetos de dominio y los DTOs

4. **Caso de uso**:
   - ✅ Se creó `CustomerProfileUseCase` para encapsular la lógica de negocio

5. **Gateway y Repositorio**:
   - ✅ Se definió la interfaz `CustomerProfileRepository` en el dominio
   - ✅ Se implementó `CustomerProfileRestConsumer` para comunicarse con la API externa

### Flujo de Datos:
1. Cliente envía petición POST a `/management/CustomerProfile`
2. El handler procesa la petición y mapea el DTO a objeto de dominio
3. El caso de uso orquesta la operación y llama al repositorio
4. El consumer hace la petición a la API externa `/profile-customer`
5. La respuesta de la API externa es mapeada y filtrada
6. El handler devuelve la respuesta filtrada al cliente

## Restricciones
- ✅ Se tomó como ejemplo la arquitectura de los microservicios existentes
- ✅ No se expone información sensible como credenciales, nombres de sistemas internos o metadatos técnicos
- ✅ Se siguieron los patrones de arquitectura limpia ya implementados en el proyecto
- ✅ Se mantiene compatibilidad con las versiones actuales de las dependencias

## Pruebas Implementadas
Se han implementado pruebas unitarias para:
- ✅ `CustomerProfileManagementHandlerTest` - Verifica el correcto funcionamiento del handler
- ✅ `CustomerProfileMapperTest` - Verifica las transformaciones entre DTOs y modelos de dominio

## Estado
✅ COMPLETADA

## Asignado a
Claude

## Tiempo real de implementación
Completado en 1 día