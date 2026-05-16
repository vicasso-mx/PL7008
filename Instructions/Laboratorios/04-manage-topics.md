---
lab:
  title: Administrar temas
  module: Administrar temas en Microsoft Copilot Studio
  description: En este ejercicio, usará Copilot para crear un tema a partir de una descripción. Esto permite que la IA generativa redacte la estructura inicial, que luego podrá refinar.
  duration: 102 minutes
  level: 100
  islab: true
---

# Administrar temas

## Escenario

En este ejercicio, hará lo siguiente:

- Administrar temas (topics) existentes
- Crear y editar temas (topics) mediante Copilot
- Crear un tema (topic) manualmente y agregar frases desencadenadoras (trigger phrases)

Este ejercicio tardará aproximadamente **30** minutos en completarse.

## Lo que aprenderá

- Cómo los temas (topics) complementan las respuestas de la IA generativa
- Cuándo se usan los temas (topics) para aplicar conversaciones estructuradas
- Cómo crear y refinar temas (topics) mediante lenguaje natural

## Pasos generales del laboratorio

- Revisar y deshabilitar temas (topics) innecesarios
- Crear un tema (topic) mediante Copilot
- Editar el contenido del tema (topic) mediante lenguaje natural
- Probar el comportamiento del tema (topic) con la IA generativa habilitada
  
## Requisitos previos

- Debe haber completado **Lab: Build an initial agent**


## Concepto clave: Temas (Topics) e IA generativa
Cuando la IA generativa está habilitada, el agente puede responder preguntas dinámicamente sin activar un tema (topic). Este es el comportamiento esperado.

Los temas (topics) se usan cuando necesita:
- Recopilar información requerida paso a paso
- Controlar el orden de las preguntas
- Almacenar respuestas en variables
- Garantizar resultados predecibles

En laboratorios posteriores, usará temas (topics) junto con nodos (nodes), entidades (entities) y herramientas (tools) para aplicar el comportamiento de su agente.

## Pasos detallados

## Ejercicio 1 - Revisar y deshabilitar temas

En este ejercicio, revisará los temas (topics) existentes y deshabilitará uno que no sea necesario.

### Tarea 1.1 – Deshabilitar temas

1. Vaya al portal de Microsoft Copilot Studio `https://copilotstudio.microsoft.com` y asegúrese de estar en el entorno adecuado.

1. Seleccione **Agents** en el panel de navegación izquierdo.

1. Seleccione el agente **Real Estate Booking Service** que creó en el laboratorio anterior.

    ![Agents in Copilot Studio portal.](../media/copilot-studio-agents.png)

1. Seleccione la pestaña **Topics**.

1. Busque el tema **Start Over**.

1. Cambie **Enabled** a **Off** para el tema **Start Over**.

    ![Topics removed and disabled in Copilot Studio portal.](../media/topics-removed.png)

Deshabilitar temas (topics) que no se usan ayuda a reducir la ambigüedad cuando varios temas (topics) o respuestas generativas podrían atender la misma solicitud.

## Ejercicio 2 - Crear temas con lenguaje natural

En este ejercicio, usará Copilot para crear un tema (topic) a partir de una descripción. Esto permite que la IA generativa redacte la estructura inicial, que luego podrá refinar.

### Tarea 2.1 – Agregar un tema a partir de una descripción

1. Seleccione **+ Add a topic** y luego **Add from description with Copilot**. Aparecerá una nueva ventana.

    ![Create topic with copilot.](../media/topic-create-from-description-2.png)

    ![Create topic with copilot.](../media/topic-create-with-copilot.png)

1. En el cuadro de texto **Name your topic**, escriba **`Customer Details`**.

1. En el cuadro de texto **Create a topic to...**, escriba **`Preguntar al cliente por su nombre y dirección de correo electrónico`**.

1. Seleccione **Create**.

1. Seleccione **Save**.

### Tarea 2.2 – Editar el contenido del tema mediante lenguaje natural

1. Si el panel **Test your agent** está abierto, ciérrelo.

1. Si el panel **Edit with Copilot** no aparece en el lado derecho del panel **Customer Details**, seleccione el icono **Copilot** en la parte superior del lienzo de creación.

    ![Screenshot of the Edit with Copilot icon.](../media/edit-with-copilot.png)

1. Seleccione el segundo nodo **Question**: **What is your email address?**

    ![Screenshot of the Edit with Copilot icon.](../media/copilot-email-address-node.png)

1. En el panel **Edit with Copilot**, en el campo **What do you want to do?**, escriba el texto siguiente:

    `Cambie "What is your email address?" para agradecer a la variable Name del nodo anterior y, a continuación, continuar con la pregunta sobre la dirección de correo electrónico.`

1. Seleccione **Update**.

    ![Screenshot of the Edit with Copilot panel with prompt.](../media/edit-with-copilot-panel.png)

    ![Screenshot of the message updated to include the Name variable.](../media/message-updated-name-variable.png)

    > **Nota**: El mensaje debe actualizarse para incluir la variable *Name* del nodo anterior y debe tener un aspecto similar al de la captura de pantalla anterior. Si **Edit with Copilot** no actualizó correctamente el nodo de pregunta, seleccione **Undo** y vuelva a intentarlo con un prompt diferente.

1. Seleccione **Save**.

### Tarea 2.3 – Agregar un resumen mediante lenguaje natural

Además de actualizar nodos (nodes) existentes, puede usar Copilot para agregar nodos (nodes) nuevos.

1. Haga clic en un área vacía del lienzo de creación para que no haya ningún nodo seleccionado.

1. En el panel **Edit with Copilot**, en el campo **What do you want to do?**, escriba el texto siguiente:

    `Resuma la información recopilada en una tarjeta adaptable (Adaptive Card)`

1. Seleccione **Update**.

Se agrega un nodo de mensaje (message node) con una tarjeta adaptable (Adaptive Card) al final del tema (topic).

![Screenshot of the message node with an Adaptive Card.](../media/message-node-adaptive-card.png)

1. Seleccione el cuadro **Media** en la tarjeta adaptable (Adaptive Card). Las propiedades de la tarjeta adaptable (Adaptive Card) deberían aparecer a la derecha de la página.

    ![Screenshot of the Adaptive Card properties.](../media/adaptive-card-properties.png)

   La fórmula de la tarjeta adaptable (Adaptive Card) debería ser similar a la anterior. Si no lo es, puede pegar la fórmula siguiente:

    ```json
    {
    type: "AdaptiveCard", 
        body: 
        [
            {
                type: "TextBlock",
                size: "Medium",
                weight: "Bolder",
                text: "Summary"    
            },
            {
                type: "FactSet",
                facts: 
                [
                    {
                        title: "Full Name",
                        value: Text(Topic.Name)
                    },
                    {
                        title: "Email Address",
                        value: Text(Topic.EmailAddress)
                    }
                ]
            },
            {
                type: "TextBlock",
                text: "Thank you for providing the information."
            }
        ]
    }
    ```

1. Asegúrese de que no haya ningún nodo seleccionado; para ello, seleccione el espacio vacío del lienzo de creación.

1. Seleccione el icono **Copilot** para volver a abrir el panel **Edit with Copilot**.

1. En el campo **What do you want to do?**, escriba el texto siguiente:

    `Agregue una nueva pregunta de opción múltiple para preguntar al usuario si los detalles son correctos, con dos opciones: Yes o No`

1. Seleccione **Update**.

1. Se agrega un nuevo nodo de pregunta (question node) al final del tema (topic) con opciones para que el usuario seleccione.

    ![Screenshot of the new question node with yes and no options.](../media/new-question-node.png)

1. Seleccione **Save**.

En laboratorios posteriores, usará esta respuesta para controlar la lógica de ramificación (branching logic) y aplicar un comportamiento predecible.

## Ejercicio 3 - Probar el tema

1. Para volver a abrir el panel **Test**, seleccione el icono **Test** en la esquina superior derecha de la página.

1. Seleccione el icono **Start new test session** en la parte superior del panel de pruebas.

    ![Screenshot of the Testing panel options.](../media/copilot-test-pane-start-new-conversation.png)

1. En el cuadro de texto, escriba **`Customer information`**.

1. Proporcione un nombre y una dirección de correo electrónico cuando se le solicite.

1. Seleccione **Yes** cuando se le pida confirmar los detalles.

1. Seleccione **Save**

Observe cómo el agente usa el tema (topic) para controlar la conversación, recopila la información requerida paso a paso y reemplaza temporalmente las respuestas generativas de formato libre.