<div align="center">

# eｊｅｒｃｉｃｉｏｓ 
### ＡＰＩ

(𝙱á𝚜𝚒𝚌𝚘 – 𝙰𝙿𝙸 𝚍𝚎 𝚙𝚛𝚘𝚖𝚎𝚍𝚒𝚘)  
(𝙱á𝚜𝚒𝚌𝚘 – 𝙰𝙿𝙸 𝚌𝚘𝚗𝚟𝚎𝚛𝚜𝚘𝚛 𝚍𝚎 𝚞𝚗𝚒𝚍𝚊𝚍𝚎𝚜)

<img src="https://i.pinimg.com/1200x/52/1b/e6/521be64cdb53322907fda07fde262f19.jpg" width="400">

<br><br>

<img src="https://github.com/Vivian-14/Ejercicios-de-API/blob/main/Pruebas/prueba.png" width="700">
<img src="https://github.com/Vivian-14/Ejercicios-de-API/blob/main/Pruebas/METODOPOST.png" width="700">
<img src="https://github.com/Vivian-14/Ejercicios-de-API/blob/main/Pruebas/POST-TEMPERATURA.png" width="700">

</div>

###  API en Flask

```python
from flask import Flask, request, jsonify, render_template

app = Flask(__name__)

# Página principal
@app.route('/')
def inicio():
    return render_template('index.html')

# API promedio
@app.route('/promedio', methods=['POST'])
def calcular_promedio():
    datos = request.get_json()

    nombre = datos['nombre']
    calificaciones = datos['calificaciones']

    promedio = sum(calificaciones) / len(calificaciones)

    respuesta = {
        "nombre": nombre,
        "promedio": promedio
    }

    return jsonify(respuesta)

# API convertir temperatura
@app.route('/convertir-temperatura', methods=['POST'])
def convertir_temperatura():
    datos = request.get_json()

    valor = datos['valor']
    escala = datos['escala']

    if escala.lower() == "celsius":
        resultado = (valor * 9/5) + 32
        destino = "Fahrenheit"

    elif escala.lower() == "fahrenheit":
        resultado = (valor - 32) * 5/9
        destino = "Celsius"

    else:
        return jsonify({"error": "Escala no válida"}), 400

    respuesta = {
        "resultado": resultado,
        "escala_convertida": destino
    }

    return jsonify(respuesta)

if __name__ == '__main__':
    app.run(debug=True)
```
