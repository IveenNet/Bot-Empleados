# Chatbot de Registro de Empleados en AIML

Este proyecto es un chatbot conversacional desarrollado en AIML (Artificial Intelligence Markup Language) que permite registrar y consultar datos básicos de empleados. Este chatbot utiliza elementos de AIML como redireccionamiento (`<srai>`), condicionales (`<condition>`) y aprendizaje dinámico (`<learn>`), cumpliendo con los requisitos de un ejercicio práctico.

## Funcionalidades

El chatbot permite:
1. **Registrar un nuevo empleado**: Toma datos como el nombre, apellidos, edad y tecnologías utilizadas recientemente.
2. **Consultar los datos de un empleado registrado**: Permite verificar si un empleado está registrado y, de ser así, muestra sus datos.
3. **Cancelar el registro**: El usuario puede cancelar el proceso de registro en cualquier momento.

## Cómo Funciona

### 1. Comenzar el Registro
El flujo de registro se inicia con el comando `REGISTRAR EMPLEADO`. Esto activa una serie de preguntas al usuario para recopilar la información necesaria:
   - Nombre del empleado.
   - Apellidos del empleado.
   - Edad del empleado.
   - Tecnologías que ha utilizado recientemente.

Cada una de estas preguntas se realiza en pasos, utilizando el `<condition>` de AIML para avanzar por el flujo de manera secuencial.

### 2. Guardar los Datos con `<learn>`
Una vez completados los datos del empleado, el chatbot utiliza `<learn>` para crear una categoría dinámica y almacenar la información del empleado. Esto permite al chatbot recordar la información de cada empleado registrado de manera única y consultable.

#### Ejemplo:
Cuando el usuario finaliza el registro de un empleado llamado "Miguel Ángel", el chatbot crea dinámicamente una categoría:
```xml
<category>
    <pattern>DATOS DE MIGUEL ÁNGEL</pattern>
    <template>
        Nombre: Miguel Ángel.
        Edad: 30 años.
        Tecnologías utilizadas recientemente: Python, SQL.
    </template>
</category>
```
Este patrón específico se aprende en el momento y permite que, en el futuro, el usuario consulte los datos del empleado "Miguel Ángel" directamente escribiendo `DATOS DE MIGUEL ÁNGEL`.

### 3. Consultar los Datos de un Empleado
Para consultar si un empleado está registrado, el usuario simplemente usa el comando `DATOS DE [nombre] [apellidos]`. Si el empleado está registrado, el chatbot mostrará la información guardada. Si no está registrado, el chatbot le informará al usuario que no tiene esa información y ofrecerá la opción de registrar al empleado.

### 4. Cancelar el Registro
En cualquier momento, el usuario puede cancelar el proceso de registro utilizando el comando `CANCELAR`. Esto detiene el flujo de registro y limpia el estado actual del proceso.

## Ejemplo de Conversación

```plaintext
Usuario: REGISTRAR EMPLEADO  
Chatbot: Por favor, proporciona el nombre del empleado.  
Usuario: Miguel  
Chatbot: Por favor, proporciona los apellidos de Miguel.  
Usuario: Ángel  
Chatbot: ¿Cuál es la edad de Miguel Ángel?  
Usuario: 30  
Chatbot: ¿Qué tecnologías ha utilizado recientemente Miguel Ángel?  
Usuario: Python, SQL  
Chatbot: ¡Empleado Miguel Ángel ha sido registrado con éxito!

Usuario: DATOS DE MIGUEL ÁNGEL  
Chatbot:  
Nombre: Miguel Ángel.  
Edad: 30 años.  
Tecnologías utilizadas recientemente: Python, SQL.
```

## Estructura del Código

- **REGISTRAR EMPLEADO:** Inicia el flujo de registro de un nuevo empleado.
- **Redireccionamiento con `<srai>`:** Una vez que el registro de datos se completa, se llama a `GENERAR DATOS` mediante `<srai>`, lo cual activa la generación dinámica de una categoría aprendida.
- **Condicionales con `<condition>`:** Los pasos de registro usan `<condition>` para avanzar según el estado actual del proceso.
- **Aprendizaje dinámico con `<learn>` y `<eval>`:** Al finalizar el registro, se usa `<learn>` para crear categorías que almacenan los datos del empleado, con `<eval>` para guardar los valores estáticos en lugar de referencias a variables.

## Requisitos

Este proyecto requiere un motor AIML que soporte:
- Aprendizaje dinámico mediante `<learn>`.
- Condicionales (`<condition>`).
- Redireccionamientos (`<srai>`).
  
Asegúrate de que el motor AIML que utilices sea compatible con estos elementos para que el chatbot funcione correctamente.
