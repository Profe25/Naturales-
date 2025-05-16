<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Juego de Ciencias Naturales</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-color: #f0f8ff;
    }
    .pregunta {
      background: #ffffff;
      border: 1px solid #ccc;
      padding: 15px;
      margin-bottom: 20px;
      border-radius: 8px;
      box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
    }
    .feedback {
      margin-top: 10px;
      font-weight: bold;
    }
    button {
      margin-top: 10px;
    }
    #resultadoFinal {
      margin-top: 30px;
      font-size: 1.2em;
      font-weight: bold;
      color: #003366;
    }
  </style>
</head>
<body>
  <h1>Juego de Ciencias Naturales</h1>
  <div id="juego"></div>
  <div style="text-align:center; margin-top:20px;">
    <button onclick="mostrarResultadosFinales()">Finalizar juego y mostrar resultados</button>
  </div>
  <div id="resultadoFinal"></div>

  <script>
    const preguntas = [
      // Aquí deben ir las 14 preguntas completas con sus textos, opciones, correcta y explicación
    ];

    let puntuacion = 0;
    let respuestasDadas = 0;
    const totalPreguntas = preguntas.length;

    const contenedor = document.getElementById("juego");
    const resultadoFinal = document.getElementById("resultadoFinal");

    preguntas.forEach((pregunta, index) => {
      const div = document.createElement("div");
      div.className = "pregunta";

      const enunciado = document.createElement("p");
      enunciado.textContent = `${index + 1}. ${pregunta.texto}`;
      div.appendChild(enunciado);

      pregunta.opciones.forEach((opcion, i) => {
        const label = document.createElement("label");
        const radio = document.createElement("input");
        radio.type = "radio";
        radio.name = `pregunta${index}`;
        radio.value = i;
        label.appendChild(radio);
        label.append(` ${opcion}`);
        div.appendChild(label);
        div.appendChild(document.createElement("br"));
      });

      const boton = document.createElement("button");
      boton.textContent = "Verificar respuesta";
      boton.onclick = () => {
        const seleccion = div.querySelector(`input[name='pregunta${index}']:checked`);
        const feedback = div.querySelector(".feedback") || document.createElement("div");
        feedback.className = "feedback";
        if (!seleccion) {
          feedback.textContent = "Por favor, selecciona una opción.";
        } else {
          boton.disabled = true;
          if (parseInt(seleccion.value) === pregunta.correcta) {
            feedback.style.color = "green";
            feedback.textContent = "✅ ¡Correcto! " + pregunta.explicacion;
            puntuacion++;
          } else {
            feedback.style.color = "red";
            feedback.textContent = "❌ Incorrecto. " + pregunta.explicacion;
          }
          respuestasDadas++;
        }
        div.appendChild(feedback);
      };
      div.appendChild(boton);

      contenedor.appendChild(div);
    });

    function mostrarResultadosFinales() {
      if (respuestasDadas < totalPreguntas) {
        alert("Por favor, responde todas las preguntas antes de finalizar el juego.");
        return;
      }
      let mensaje = `Puntuación final: ${puntuacion} de ${totalPreguntas}.`;
      if (puntuacion >= 12) {
        mensaje += " ¡Excelente trabajo! 🌟";
      } else if (puntuacion >= 9) {
        mensaje += " ¡Muy bien! Sigue practicando. 👍";
      } else {
        mensaje += " Ánimo, puedes mejorar con más práctica. 💪";
      }
      resultadoFinal.textContent = mensaje;
    }
  </script>
</body>
</html>
